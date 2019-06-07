Cloudflare Workers 是一种类似于无服务器函数的功能，它让开发人员能够进行边缘计算。

什么是边缘计算呢？大家都知道，传统的网站就是浏览器和服务器，服务器负责处理逻辑程序，例如条件判断、数据库操作、用户数据读取写入等；浏览器负责将服务器返回的 HTML、Css、JavaScript 代码进行计算、执行、渲染，然后网页的最终效果就呈现在用户面前了。

而边缘计算呢，它是一个处于浏览器和服务器中间的一个位置，充当一个中间人，浏览器的流量首先到达 Workers，由 Workers 对请求进行一部分的逻辑处理，例如根据请求者的 IP 地址判断对方是哪个国家的用户，然后将用户导向对应语言的站点，当然这只是最基础的功能。再高级一点，通过边缘计算，可以实现网站防火墙，阻止含有危险内容的数据上传到服务器，起到服务器的挡箭牌作用。

那么如何使用 Workers 进行边缘计算呢？其实很简单，Workers 基于 JavaScript，使用 JavaScript v8 引擎，通过 Cloudflare 分布在全球的成百上千个节点，每个节点在接收到请求之后会在该节点上进行计算，将服务器的计算负担均衡到全球的各个节点，大大节省了服务器的性能开支。

想要编写一个简单的 Workers 非常简单，下面是一个例子，用于输出 Hello world

```javascript
addEventListener("fetch", event => {
  event.respondWith(handleRequest(event.request))
})

/**
 * Fetch and log a request
 * @param {Request} request
 */
async function handleRequest(request) {
  return new Response("Hello world!", {status: 200})
}
```

其中 addEventListener 是绑定事件监听器，当有用户请求 Workers 时，将会触发 fetch 事件，然后会交给 handleRequest 函数处理。

handleRequest 函数在处理完之后，返回一个 Response，也叫响应，内容是 Hello world!，状态码是 200。

最终，呈现在网页上的就是 Hello world! 这几个字。

想了解更多关于 Workers 的内容，欢迎阅读 Cloudflare 官方文档：https://workers.cloudflare.com/docs/quickstart/

