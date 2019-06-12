Cloudflare 默认会给你一个 workers.dev 域名，对于没有域名的小伙伴来说是个福利。

不过如果你已经有一个域名了，想要作为博客使用怎么办呢？我们一起来看。

### 0x01 创建项目

开始之前，我们检查一下自己是否已经安装了 Wrangler，一般来说是没有的。

那么我们就需要先安装 Wrangler，首先是配置 Rust 运行时：

```shell
curl https://sh.rustup.rs -sSf | sh
```

然后安装 Wrangler：

```shell
cargo install wrangler
```

安装完成之后要加入到环境变量，编辑 `/etc/profile`，找到 `export PATH=` 这一行，在结尾的 `:$PATH` 前面增加以下内容

```shell
:$HOME/.cargo/bin
```

然后看起来应该像是这样：

```shell
export PATH=/usr/local/php/bin:/usr/local/nginx/sbin:/usr/local/mariadb/bin:$HOME/.cargo/bin:$PATH
```

最后输入 `source /etc/profile` 即可。

接着我们创建一个项目，名字就叫 test-worker：

```shell
cd ~
wrangler generate test-worker
cd test-worker
```

然后列出目录文件，你会看到一个 index.js，编辑它：

```shell
vim index.js
```

修改完之后保存。

### 0x02 发布项目

你需要配置你的 Cloudflare 账户信息，首先我们打开 Cloudflare 官网：https://www.cloudflare.com/

登录到 dashboard 后，右上角的头像那里点一下，然后点击 My Profile，接着会进入个人资料页。

底部有一个 API Keys，点击 Global API Key 那一栏右边的 View 按钮查看你的 API Key，接着会要求你输入密码并进行人机验证，有个谷歌验证码。

![img](https://i.natfrp.org/caa043463ddf373ba06721c36c6a2072.png)

确认后就会显示出你的 API Key，将其复制并保管好，它和你的密码一样重要。

回到 Shell，输入以下命令进行配置：

```shell
wrangler config <你的账户邮箱> <你的 api key>
```

然后我们修改 wrangler.toml，这个是项目的配置文件，里面记录了一些关于这个 Worker 的选项：

```
# 你的 Worker 名字
name = "test-worker"

# 你的 Cloudflare 账户 ID
# 在域名的 Overview 页面的右下角可以查看到 Account ID
account_id = "1234567890abcdefghijklmn"

# 你的 Cloudflare 域名 ID
# 同样是在域名的 Overview 页面右下角可以看到 Zone ID
zone_id = "abcdefghijklmn1234567890"

# 你想要绑定的域名
# 记得结尾加个 /*
route = "blog.natfrp.org/*"

# 设置应用程序的类型，默认是 webpack，无需更改
type = "webpack"
```

然后将项目构建并发布到 Cloudflare：

```shell
wrangler build
wrangler publish --release
```

### 0x03 设置解析

最后一步，增加 DNS 解析，将你设置的域名前缀解析到你的 workers.dev 域名。

例如我绑定了 blog.natfrp.org，我的 workers.dev 域名是 zerodream.workers.dev，那么就将 blog 前缀解析到 zerodream.workers.dev，类型 CNAME，并打开 CDN 模式（点亮黄色的云）。

![img](https://i.natfrp.org/f074eead5507d5144a5fca7f67427317.png)

完成，现在你可以访问你的域名查看效果了。

