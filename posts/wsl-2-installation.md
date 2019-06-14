WSL 2 (Windows Subsystem for Linux 2.0) 是一个可以让你在 Windows 下运行 Linux 软件的应用，由微软官方推出，目前可以在 Windows 10 和 Windows Server 2016/2019 上使用。

本文主要介绍如何在已经安装了 WSL 的基础上升级为 WSL 2.0，具体的操作过程下面都会给出。

WSL 2 与 WSL 不同的地方是，WSL 2 采用了虚拟化的方式，它将 Linux 作为一个轻量级的 VM 来运行，启动速度是传统虚拟机的几十倍，只需要 1 秒即可启动，但是却拥有完整的 Linux 内核，这意味着你可以用 WSL 2 运行很多 WSL 无法运行的软件了。

### 准备工作

安装 WSL 2 之前，你需要做好以下准备：

1. 将 Windows 更新至 Windows 10 build 18917 或者更新的版本
2. 安装好 WSL，在控制面板 > 程序和功能 > 启用或关闭 Windows 功能 中选中 “适用于 Linux 的 Windows 子系统”
3. 在 Microsoft Store 中安装好 Ubuntu 子系统（直接搜索 Ubuntu 就有）
4. 关闭所有 VMware 的虚拟机（如果有）

### 转换子系统

确定系统已经更新到 18917 后，以管理员身份运行 PowerShell，输入以下命令启用虚拟机平台组件：

```text
Enable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform
```

输入完之后会出现一个进度条，稍等一会会输出三行提示，不用管它，此时重启电脑。

重启完后再次以管理员身份运行 PowerShell，输入以下命令查看你已经安装的 WSL 发行版：

```text
wsl -l
```

输出内容：

```text
适用于 Linux 的 Windows 子系统:
centos (默认)
```

可以看到我安装了一个 CentOS 的子系统，你们可能是 Ubuntu，具体根据自己的情况来。

接下来输入以下命令将你的子系统转换为 WSL 2.0 版本：

```text
wsl --set-version <发行版名字> 2
```

例如我的是 centos：

```text
wsl --set-version centos 2
```

这个过程需要很长时间，大概要 5~10 分钟，具体取决于你的硬盘性能，它需要将你原来的文件转换为 VHD 虚拟磁盘格式。

如果你想以后安装的所有 WSL 子系统都默认使用 2.0 版本，可以输入以下命令：

```text
wsl --set-default-version 2
```

### 验证转换结果

最后，输入以下命令查看你的 WSL 子系统版本是否是 2.0：

```text
wsl -l -v
```

输出结果：

```text
  NAME      STATE           VERSION
* centos    Running         2
```

然后你就可以输入 `wsl -d <发行版名字>` 启动对应的发行版了，或者直接输入 `bash` 启动。

### 关于 WSL 2

WSL 2 其实是基于 Hyper-V 的一个精简版虚拟机，但是它的启动速度极快，大概就 1 秒左右，已经和 Docker 差别不大了。

因为是虚拟机的原因，它会和 VMware 冲突，这意味着你在使用 WSL 2 以后将无法使用 VMware 虚拟机，但是官方已经在公告中说明会加快对虚拟机的兼容，解决冲突问题。

至于为什么安装了 Hyper-V 无法使用 VMware 呢？根据论坛大佬的说法是：Hyper-V 会直接取得宿主机的完全控制权，然后将宿主机的 Windows 操作系统变成 Hyper-V 的一个虚拟机，Hyper-V 和宿主机 Windows、虚拟机之间的关系大概像是父亲、哥哥和弟弟妹妹，Hyper-V 接管了最高控制权，Windows 则成为第二级权限系统，可以管理其他的虚拟机。因此在虚拟机里嵌套虚拟机就可能出现一些奇怪的问题，所以无法使用 VMware。

总体来说 WSL 2.0 可玩性还是很高的，期待微软进一步更新吧。

