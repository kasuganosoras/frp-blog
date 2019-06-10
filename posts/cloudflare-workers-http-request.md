如果想要在 Cloudflare Workers 中发起 http 请求，则需要用到 Fetch API。

> **注意**：Fetch API 仅能在 Request 中使用。

首先我们来看看 fetch 的基本使用方法：

```javascript
const response = await fetch(url, init);
```

其中 response 是返回数据的储存变量，url 是需要请求的地址，init 是请求的参数设定（可选的）。

init 有以下几个选项：

- method：请求的方法，例如 GET 或者 POST
- headers：请求时需要发送的 headers，它是一个对象
- body：请求时需要发送的内容，注意，这个选项不能在 GET / HEAD 方法下使用
- redirect：重定向的处理方式，可选值：follow 跟随跳转，error 抛出错误，manual 手动处理

await 在异步函数内使用时必须要添加。

我们得到了 response 后，就可以开始对其进行处理，如果要获取返回的内容，可以这样写：

```javascript
const data = await response.text();
```

然后你就可以对 data 变量进行任何处理了。

下面是一段演示代码，用于获取访问者 IP 的地理位置：

```javascript
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request))
})

/**
 * Respond to the request
 * @param {Request} request
 */
async function handleRequest(request) {
  // 取得访问者的 IP 地址
  const ip_raw = request.headers.get("cf-connecting-ip");
  // 设置请求参数
  const init = {
    method: 'GET'
  }
  // 发起 http 请求 API，获取 IP 的归属地
  const response = await fetch(`https://api.tcotp.cn:4443/ip/?ip=${ip_raw}`, init);
  // 取得返回内容
  const ip_area = await response.text();
  // 输出到浏览器
  return new Response(ip_area, {status: 200})
}
```

以上就是 Cloudflare workers 发起 http 请求的教程，感谢阅读。

