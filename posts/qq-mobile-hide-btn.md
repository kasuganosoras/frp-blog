有时候想要做一个网站，只允许用户在手机 QQ 浏览器访问的时候，如何不让用户跳转到外部浏览器是个问题。

当然，这个方法仅限于普通人，遇到专业点的改个 User Agent 也能绕过……

原理呢，就是调用了 QQ API，设置手机 QQ 浏览器右上角 + 的样式，我们这里设置为 12 就可以隐藏

```html
<script type="text/javascript" src="https://open.mobile.qq.com/sdk/qqapi.js?_bid=100"></script>
<script>
	mqq.ui.setTitleButtons({
		right: {
			iconID:12,
			callback:function(){
				return;
			}
		}
	});
</script>
```

设置之后的效果：

![img](https://i.natfrp.org/cb16b5abb34ca0340a00ac777a3d7e4e.png)

可以看到右上角的 + 没有了。

这里的 `iconID` 呢，是可以设置为其他的，例如 `3` 就是 `+` ，具体可以自己尝试。

还有个作用就是防举报……

```html
<script type="text/javascript" src="https://open.mobile.qq.com/sdk/qqapi.js?_bid=100"></script>
<script>
	mqq.ui.setTitleButtons({
		right: {
			iconID:3,
			callback:function(){
				alert("想举报？小伙子你路走窄了！");
				return;
			}
		}
	});
</script>
```

仅用于对付小白使用……如果人家真想举报的话用外部浏览器打开腾讯安全中心举报就完事了

QQ API 还是有很多东西可玩的，具体可以找一下相关文档来看看。


