在 GTA5 里面，低底盘车有一个很好玩的功能，就是液压装置，可以通过按 X 键来控制车轮弹跳。

而对于普通车来说，是没有这个功能的，那么如果想要给普通载具也加上这个功能的话，则需要修改一些文件。

首先找到需要修改的载具的数据文件，这里需要修改 vehicle.meta 和 carcols.meta 文件。

首先我们来看 vehicle.meta 文件，在这里我们可以找到一个 flags 项，它的值由空格隔开，每个 flag 对应的都是载具的一种特性，这里我们需要为它加入液压装置系统的特性，假如原来的 flag 是这样的：

```xml
<flags>FLAG_SPORTS FLAG_AVERAGE_CAR FLAG_HAS_LIVERY</flags>
```

那么我们修改一下，加入 `FLAG_HAS_LOWRIDER_HYDRAULICS` 这个选项。

```xml
<flags>FLAG_SPORTS FLAG_AVERAGE_CAR FLAG_HAS_LIVERY FLAG_HAS_LOWRIDER_HYDRAULICS</flags>
```

接着来修改 carcols.meta 文件，在 `<statMods>` 和 `</statMods>` 之间加上以下内容：

```xml
<Item>
    <identifier />
    <modifier value="25" />
    <audioApply value="1.000000" />
    <weight value="0" />
    <type>VMT_WHEELS_REAR_OR_HYDRAULICS</type>
</Item>
<Item>
    <identifier />
    <modifier value="50" />
    <audioApply value="1.000000" />
    <weight value="0" />
    <type>VMT_WHEELS_REAR_OR_HYDRAULICS</type>
</Item>
<Item>
    <identifier />
    <modifier value="75" />
    <audioApply value="1.000000" />
    <weight value="0" />
    <type>VMT_WHEELS_REAR_OR_HYDRAULICS</type>
</Item>
<Item>
    <identifier />
    <modifier value="100" />
    <audioApply value="1.000000" />
    <weight value="0" />
    <type>VMT_WHEELS_REAR_OR_HYDRAULICS</type>
</Item>
```

保存这两个文件，然后进入游戏即可按 X 使用低底盘液压装置。
