# HTTP
# What is HTTP?
> HTTP是万维网的基础，用于使用超文本链接加载网页。HTTP是一种应用层协议，旨在在联网设备之间传输信息，并在网络协议栈的其他层上运行。通过 HTTP 的典型流涉及客户端计算机向服务器发出请求，然后服务器发送响应消息。

![1.png](https://media.haochen.me/1.png)
它是一种通过 TCP 或 TLS 加密的 TCP 连接发送的应用层协议，但是理论上可以使用任何可靠的传输协议。由于其可扩展性，它不仅用于获取超文本文档，还用于获取图像和视频或将内容发布到服务器

### HTTP的系统组件

每个单独的请求都发送到服务器，服务器处理该请求并提供称为响应的答案。例如，在客户端和服务器之间有许多实体，统称为代理，它们执行不同的操作并充当网关或缓存。

![proxy.png](https://media.haochen.me/proxy.png)

- proxy代理服务器

  - 代理服务器是在通过互联网的不同网络导航时使用的中间程序或计算机。它们有助于访问万维网上的内容。代理拦截请求并提供回应;它可以转发请求，也可以不转发请求（例如在缓存的情况下），并且可以修改请求（例如，在两个网络之间的边界处更改其标头）。

代理可以位于用户的本地计算机上，也可以位于用户计算机与 Internet 上目标服务器之间的任何位置。通常，代理服务器主要有两种类型：

1. 转发代理，用于处理来自和发送到互联网上任何位置的请求。
2. 反向代理从 Internet 接收请求并将其转发到内部网络中的服务器。

# HTTP request
HTTP请求是互联网通信平台(如web浏览器)请求加载网页所需的信息的方式。

每个在互联网发出的HTTP请求都会携带一系列编码数据，这些数据携带不同类型的信息。一般HTTP请求包含下列：
1. 版本类型
2. 一个网址URL
3. 一个HTTP方法
4. HTTP请求标头header
5. 可选的HTTP正文body

### HTTP method
HTTP方法有时候指的是HTTP请求期望从查询的服务器执行的行为

eg:
- GET：get请求期望从服务器返回信息
- POST：post请求表明客户向服务器提交信息(例如表单信息、用户名密码)

### HTTP header
HTTP标头包含储存在键值对中(key-value)的文本信息，并且它们包含在每个 HTTP 请求中。这些标头传达核心信息：例如客户正在使用什么浏览器、正在请求什么数据。

来自谷歌浏览器网络标签的HTTP请求标头示例：
![header.png](https://media.haochen.me/header.png)

### HTTP request body
HTTP请求正文包含请求正在传输的正文信息，例如：用户名密码或者在表单中输入的任何其他数据。

# HTTP response
HTTP响应是web客户端从互联网服务器接收的响应HTTP请求。

一般HTTP响应包含：
1. HTTP状态代码
2. HTTP响应标头
3. 可选的HTTP正文

### HTTP status code
HTTP状态代码是3位数代码，最常用于指示 HTTP 请求是否已成功完成。状态代码分为以下5个块：

- 1xx Informational 信息响应
- 2xx Success       成功

  - 表示代码已成功，eg：在客户端请求网页后，最常见的响应的状态代码为"200 OK"，表示请求已正确完成。
- 3xx Redirection   重定向
- 4xx Client Error  客户端错误

    - 以"4"开头的状态代码表示客户端错误，eg：在 URL 中输入拼写错误时，状态代码显示"404 未找到"
- 5xx Server Error  服务器错误
  
### HTTP response header
与 HTTP 请求非常相似，HTTP 响应附带标头，这些标头传达重要信息，例如在响应正文中发送的数据的语言和格式。

来自谷歌浏览器网络标签的HTTP响应标头示例：
![alt ](../CSS与img引用/Internet/response%20header.png)

### HTTP response body
对"GET"请求的成功HTTP响应通常具有包含所请求信息的正文。在大多数Web请求中，这是Web浏览器将转换为Web页面的HTML数据。

# DoS攻击可以通过HTTP发起吗？
> 拒绝服务（DoS）攻击是一种网络攻击，恶意行为者通过中断设备的正常功能，使其目标用户无法使用计算机或其他设备。DoS 攻击通常通过请求压垮或淹没目标计算机，直到其无法处理正常流量，从而对其他用户造成拒绝服务。DoS 攻击的特征是使用一台计算机来发起攻击。
> 
> DoS 攻击的主要重点是使目标计算机的容量过饱和，从而对其他请求造成拒绝服务。DoS 攻击具有多种攻击途径，可通过它们的相似性来分组。


HTTP 是一种"无状态"协议，这意味着每个命令都独立于任何其他命令运行。在原始规范中，每个 HTTP 请求都创建并关闭了 TCP 连接。在较新版本的 HTTP 协议（HTTP 1.1 及更高版本）中，持久连接允许多个 HTTP 请求通过持久性 TCP 连接传递，从而改善资源消耗。在 DoS 或 DDoS 攻击的上下文中，大量 HTTP 请求可用于在目标设备上发起攻击，并被视为应用层攻击或第 7 层攻击的一部分。

# HTTP的基本方面
### HTTP是可扩展的
HTTP 标头使该协议易于扩展和试验。新功能甚至可以通过客户端和服务器之间关于新标头语义的简单协议来引入。

### HTTP的连接
HTTP依赖于基于连接的TCP标准。

# HTTP的消息
### 请求
![HTTP.png](https://media.haochen.me/HTTP.png)

### 响应
![HTTP1.png](https://media.haochen.me/HTTP1.png)