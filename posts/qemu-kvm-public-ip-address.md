租了一个美国堪萨斯的 AMD 独服，16 个 IPv4，打算用来出租 VPS 服务器，因为之前自己造过一个 VPS 面板，于是就打算用自己的面板来开 VPS。

不过之前我的面板主要是用来开 NAT VPS 的，就是共享 IP，端口映射这种，如果要换成独立公网 IP，还得对面板进行一些改造。

一开始在网上找了很多文章，全都是关于 DHCP 分配局域网 IP 的，没讲到如何给虚拟机分配公网 IP，默认情况下，虚拟机只能分配到 `192.168.122.0` 这个网段的 IP，也就是 QEMU 默认的虚拟机 IP 段，但是如果要给虚拟机分配一个和物理机一样的，可以在全球任意位置访问的公网 IP，那就需要对配置文件进行修改。

这是原来的虚拟机网卡配置：

```xml
<interface type='bridge'>
	<mac address='0e:37:6a:3c:d8:45'/>
	<source network='default' bridge='enp2s0'/>
	<virtualport type='openvswitch'/>
	<target dev='vnet0'/>
	<model type='virtio'/>
	<alias name='net0'/>
	<address type='pci' domain='0x0000' bus='0x00' slot='0x03' function='0x0'/>
</interface>
```

可以看到，网卡类型是 bridge 桥接，然后所属网络是 default，桥接到 enp2s0 物理机网卡。

下面我们要进行一些修改，让虚拟机拥有直接连接物理机网卡的能力（direct）

```xml
<interface type='direct'>
	<mac address='0e:37:6a:3c:d8:45'/>
	<source dev='enp2s0' mode='bridge'/>
	<virtualport type='openvswitch'/>
	<target dev='macvtap0'/>
	<model type='virtio'/>
	<alias name='net0'/>
	<address type='pci' domain='0x0000' bus='0x00' slot='0x03' function='0x0'/>
</interface>
```

可以看到，interface 的类型已经改为了 direct，source 也进行了一些修改，绑定硬件是 enp2s0 物理机网卡，类型是桥接，这样虚拟机就不会桥接到虚拟网卡了，而是直接桥接到物理机网卡。

下面的 target 也改了，dev 的值改为了 `macvtap0` 。MacVlan 的功能是给同一个物理网卡配置多个 MAC 地址，可以在软件上配置多个以太网口，属于物理层的功能。MacVTap 是用来替代 TUN/TAP 和 Bridge 内核模块的。MacTap 是基于 MacVlan 这个模块，提供 TUN/TAP 中 TAP 设备使用的接口，使用 MACVTap 以太网口的虚拟机能够通过 TAP 设备接口，直接将数据传递到内核中对应的 MacVTap 以太网中。[[1]](<https://www.cnblogs.com/echo1937/p/7249812.html>)

最后，保存配置文件，将虚拟机关机，然后取消注册配置文件，再重新注册回去即可。

```shell
virsh undefine test_vm
virsh define test_vm.xml
```

完成，现在可以启动虚拟机，然后进入操作系统设置 IP 地址了。

