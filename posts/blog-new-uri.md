RT，已经完成了伪静态改造，主要修改的地方就是路由。

将原来的首页判断改为了以下内容：

```javascript
if(urls.pathname == "/")
```

将请求的 URL 字符串转为 URL 对象

```javascript
var urls = new URL(request.url);
```

重新填充路径，不再从 GET 参数获取

```javascript
var uname = unescape("posts" + urls.pathname + ".md");
```

从新的 URL 获取 Markdown 内容

```javascript
var url = "https://raw.githubusercontent.com/" + github_base + "/master/posts" + urls.pathname + ".md";
const init = {
    method: "GET"
};
const response = await fetch(url, init);
```

关于本博客模板可访问 https://github.com/kasuganosoras/cloudflare-worker-blog/blob/master/workers-sakurafrp.js 查看。


