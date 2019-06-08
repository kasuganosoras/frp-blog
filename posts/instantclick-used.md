> InstantClick 是一个 JavaScript 库，可以显着加快你的网站速度，在大多数情况下可以有效地实现导航。

### 为什么使用 InstantClick

尽管现代互联网的带宽很大，但网站的速度并不快，这是因为加载网页的最大瓶颈就是延迟。

### 它是如何工作的

今天的互联网架构延迟是不可避免的，所以 InstantClick 通过预加载你可能点击的链接来尽可能缩短所需要的时间。

InstantClick 会将你鼠标下的链接预先载入，当你点击链接时就会感到无比顺滑，瞬间打开。

在访问者点击链接之前，他们将鼠标悬停在该链接上。在这两个事件之间，通常持续 200 毫秒到 300 毫秒。InstantClick 利用该时间来预加载页面，以便在用户单击时页面立即显示。

在移动设备上，预加载从 “touchstart” 开始，Android 上的延迟是 300 毫秒，IOS 上的延迟是 450 毫秒。

### 如何使用 InstantClick

首先我们下载 http://instantclick.io/v3.1.0/instantclick.min.js 这个文件，然后放入自己网站合适的目录内。

接着我们在网页的 `</body>` 之前的位置这样写，引入 InstantClick：

```html
······
<!-- 引入 InstantClick -->
<script src="instantclick.min.js" data-no-instant></script>
<script data-no-instant>InstantClick.init();</script>
<!-- 到这里结束 -->
</body>
</html>
```

然后就可以开始体验超快的网站访问速度了。

不过要注意，在使用了 InstantClick 之后，`window.onload` 之类的函数在点击链接后将不在起作用。

取而代之的是 `InstantClick.on('xxx', callback)`，举个例子：

```javascript
InstantClick.on('change', function() {
    console.log("你点击了一个新链接");
});
```

原来的 Onload 也不必删除，在页面首次加载时依然会执行。


