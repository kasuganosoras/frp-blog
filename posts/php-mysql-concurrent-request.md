昨天在 UOvZ 的 Telegram 水群看到有人说 UOvZ 的服务器管理面板有个 bug，NAT 主机添加端口映射的页面，只要同时开两个页面，然后在手速够快的情况下在两个页面同时点添加映射，就可以超过上限（UOvZ 限制了每个 NAT 主机只能添加 5 个映射），超过 6 个以后就可以无限制添加了。

为什么会出现这个 bug 呢？这是一个很常见的 PHP 并发处理问题，通常都是因为业务代码逻辑顺序问题造成的 bug，也不是什么非常难修复的问题。

### 0x01 进行测试

想要摸清楚一个网站后端的逻辑，首先需要进行多次测试。例如本文的例子就是服务器面板，其实这种 bug 我相信接触网络多年的各位多少也遇到过类似的情况，造成这个 bug 的原因也就是代码逻辑处理的问题。

那么如何去测试呢？我们打开一个网站后，首先进行一些简单的点击、输入一些错误的值看看是否有错误输出，通过 GET 或 POST 提交一些错误的信息等，都可以进行测试。

然后就是并发测试，你可以选择人工进行，也可以写个程序来模拟请求，测试一下在同时请求某个页面，或者同时提交某个请求时，网站会做出何种反应，是否会报错等等。

### 0x02 代码分析

首先我们来看一段代码，简单的添加端口映射：

```php
$max = 5; // 最多 5 条映射
$rs = mysqli_query($conn, "SELECT * FROM `portmap` WHERE `username`='{$username}' AND `vm`='{$vm}'");
$currentPorts = mysqli_num_rows($rs);
if($currentPorts == $max) {
	echo "已达到映射的最大上限";
} else {
	$result = $PortMap->add($port, $intervalPort, $vm->primaryIp);
	if($result) {
		mysqli_query($conn, "INSERT INTO `portmap` (`id`, `username`, `ip`, `port`, `interval_port`) 
			VALUES (NULL, '{$username}', '{$vm->primaryIp}', '{$port}', '{$intervalPort}')");
		echo "添加成功！";
	} else {
		echo "添加失败！";
	}
}
```

表面上看起来很正常对吧？先是通过 `mysqli_query` 查数据表，获得已添加的所有映射，然后取结果数量来判断已经添加了多少个映射，如果等于 5 也就是已经达到最大条数，就拒绝添加。

但是这里实际上存在两个漏洞，首先我们注意这里：

```php
$result = $PortMap->add($port, $intervalPort, $vm->primaryIp);
```

如果这个操作需要消耗比较长的时间，那么在这段时间内用户就可以通过再次发起请求来实现多次添加映射。

为什么呢？因为写入数据库的操作，是在 `$PortMap->add` 这个操作之后才执行的，在执行完这个操作之前，数据库里还没写入这条记录，于是用户就可以多次发起请求，而程序去读取数据库时，没有取得这条记录，就认为你的记录还没到 5 条，于是再次往下执行，造成超过限制。

然后就是，判断 `$currentPorts` 是否等于 `$max` 时使用了 `==` 进行判断，这就会造成超过限制后就无上限任意添加了，如果改为 `>=` 就不会出现这个情况，顶多添加到 6 条，手速快的话可能 7 条。

### 0x03 漏洞修复

想要修复这个漏洞，也不是什么难事，首先要记住，我们始终应该把写入数据库的操作放在需要耗时比较长的事件前面，例如我们应该把写入数据库的操作放在发送邮件操作的前面，避免因为发信时间太长导致写入数据库延迟，就会出现上面的问题。

上面的这段代码，经过修复后应该是下面这个样子

```php
$max = 5; // 最多 5 条映射
$rs = mysqli_query($conn, "SELECT * FROM `portmap` WHERE `username`='{$username}' AND `vm`='{$vm}'");
$currentPorts = mysqli_num_rows($rs);
if($currentPorts >= $max) {
	echo "已达到映射的最大上限";
} else {
	mysqli_query($conn, "INSERT INTO `portmap` (`id`, `username`, `ip`, `port`, `interval_port`) 
			VALUES (NULL, '{$username}', '{$vm->primaryIp}', '{$port}', '{$intervalPort}')");
	$id = mysqli_insert_id($conn);
	$result = $PortMap->add($port, $intervalPort, $vm->primaryIp);
	if($result) {
		echo "添加成功！";
	} else {
		mysqli_query($conn, "DELETE FROM `portmap` WHERE `id`='{$id}'");
		echo "添加失败！";
	}
}
```

先执行 MySQL 写入操作，写完了之后再进行端口映射添加等需要较长时间的操作，最后再判断是否添加映射成功，如果失败，再将数据库中的记录删除。

### 0x04 文章总结

永远不要把写入数据库的操作放在需要长时间的操作后面（针对这种需要判断记录条数的）。

另外，高并发问题主要通过锁、限制请求速率来解决，具体可以学习一下 “锁” 机制。

