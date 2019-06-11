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

增加了翻页功能，每页显示 5 篇文章

```javascript
if(current_page > 1) {
    data += `<a href="/?p=${before_page}"><button class="btn btn-default">上一页</button></a>&nbsp; &nbsp;`;
}
if(update_i >= 5) {
    data += `<a href="/?p=${next_page}"><button class="btn btn-default">下一页</button></a>`;
}
```

关于本博客模板可访问 https://github.com/kasuganosoras/cloudflare-worker-blog/blob/master/workers-sakurafrp.js 查看。


