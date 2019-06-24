这两天有人问到了关于没有 Root 在 Android 下运行 Sakura Frp 客户端的问题，为此我专门进行了一次实验，测试到底能不能在没有 Root 的情况下运行客户端。

首先测试设备就是我的华为 Mate9，未 Root 系统，Android 9.0，测试使用软件 JuiceSSH。

__第一步，下载客户端到手机储存根目录并解压。__

众所周知手机 CPU 是 ARM 架构的，因此我们就下载 ARM 版本的客户端即可，下载到储存根目录即 /storage/emulated/0：

```bash
https://cdn.tcotp.cn:4443/client/Sakura_frpc_linux_arm.tar.gz
```

下载完之后，使用 RE 文件管理器解压出客户端，放在手机储存目录。

__第二步，将客户端复制到终端软件目录。__

首先我们查询一下终端软件的包名，最简单的方法是在谷歌应用商店搜索这个应用，点进去之后，地址栏就有软件的包名，复制即可。

![img](https://i.natfrp.org/1b88e392e74a0ac510ab69d3a76b625f.png)

接着在终端输入以下命令进入数据储存目录

```bash
cd /data/data/com.sonelli.juicessh/
```

为什么要写进这个目录呢？因为 Android 的安全设定，每个应用只有在自己的 data 目录内拥有可执行权限，所以我们可以将客户端下载到这个目录里执行。

进入目录后，将客户端复制进来：

```
cp /storage/emulated/0/Sakura_frpc_linux_arm ./
```

然后设置可执行权限：

```bash
chmod +x Sakura_frpc_linux_arm
```

接着尝试运行客户端：

```bash
./Sakura_frpc_linux_arm
```

可以运行了，效果如下：

![img](https://i.natfrp.org/210b3b03a30ce6d374744eca1d2596a6.png)

很奇怪是不是？解析域名居然出现了 Connection refused 错误，可是为什么呢？

因为 Android 并不是一个完整的 Linux 系统，它默认没有设置 DNS 服务器，因此在软件运行时，软件会去尝试解析域名，而由于没有设置 DNS 服务器，它就默认使用 localhost 作为 DNS 服务器来进行解析，而 localhost 上并没有 DNS 服务器在运行，最终导致域名解析失败，出现上面的错误。

那你可能会问，我可以给手机指定一个 DNS 服务器啊？很遗憾的是，Android 在没有 Root 的情况下，你不可能对 /etc/resolve.conf 进行任何读写操作，没有办法添加 DNS 服务器。

你还可能会问，我可以在手机上运行一个 DNS 服务器呀，不是有一个 DNS Server 软件吗？

是的，为此我也专门下载了这个软件进行测试，结果发现……

![img](https://i.natfrp.org/e58992189018a4f7cf167af2616a2c54.png)

哦豁，为什么会出现这个问题？

原因很简单，Linux 不允许非 root 用户监听 1024 以下的端口，53 端口自然不能监听，所以无法运行。

至此，在非 Root 的 Android 上尝试运行客户端到此结束，结论是：没有 Root 的情况下无法正常运行客户端。

