title:HTTP请求报文和HTTP响应报文
---
　HTTP是一个应用层协议，由请求和响应构成，是一个标准的客户端服务器模型。HTTP是一个无状态的协议。
<!--more-->

### 一次完整的HTTP请求所经历的7个步骤
HTTP通信机制是在一次完整的HTTP通信过程中，Web浏览器与Web服务器之间将完成下列7个步骤：
##### 1. 建立TCP连接
在HTTP工作开始之前，Web浏览器首先要通过网络与Web服务器建立连接，该连接是通过TCP来完成的，该协议与IP协议共同构建 Internet，即著名的TCP/IP协议族，因此Internet又被称作是TCP/IP网络。HTTP是比TCP更高层次的应用层协议，根据规则， 只有低层协议建立之后才能，才能进行更层协议的连接，因此，首先要建立TCP连接，一般TCP连接的端口号是80
##### 2. Web浏览器向Web服务器发送请求命令
一旦建立了TCP连接，Web浏览器就会向Web服务器发送请求命令。例如：GET/sample/hello.jsp HTTP/1.1。
##### 3. Web浏览器发送请求头信息
浏览器发送其请求命令之后，还要以头信息的形式向Web服务器发送一些别的信息，之后浏览器发送了一空白行来通知服务器，它已经结束了该头信息的发送。
##### 4. Web服务器应答
客户机向服务器发出请求后，服务器会客户机回送应答， HTTP/1.1 200 OK ，应答的第一部分是协议的版本号和应答状态码。
##### 5. Web服务器发送应答头信息
正如客户端会随同请求发送关于自身的信息一样，服务器也会随同应答向用户发送关于它自己的数据及被请求的文档。
##### 6. Web服务器向浏览器发送数据
Web服务器向浏览器发送头信息后，它会发送一个空白行来表示头信息的发送到此为结束，接着，它就以Content-Type应答头信息所描述的格式发送用户所请求的实际数据。
##### 7. Web服务器关闭TCP连接
一般情况下，一旦Web服务器向浏览器发送了请求数据，它就要关闭TCP连接，然后如果浏览器或者服务器在其头信息加入了这行代码：
`Connection:keep-alive`
TCP连接在发送后将仍然保持打开状态，于是，浏览器可以继续通过相同的连接发送请求。保持连接节省了为每个请求建立新连接所需的时间，还节约了网络带宽。

### HTTP请求报文
一个HTTP请求报文由请求行（request line）、请求头部（header）、空行和请求数据4个部分组成。
```
<request-line> 请求行
<headers> 请求头
<blank line> 空格
<request-body> 请求数据
```
#### 请求行
请求行由请求方法字段、URL字段和HTTP协议版本字段3个字段组成，它们用空格分隔。例如，GET /index.html HTTP/1.1。

HTTP协议的请求方法有GET、POST、HEAD、PUT、DELETE、OPTIONS、TRACE、CONNECT。

例子：
```
Request URL:https://www.baidu.com/
Request Method:GET
Status Code:200 OK
Remote Address:172.31.1.246:8080
```

#### 请求头部
请求头部由关键字/值对组成，每行一对，关键字和值用英文冒号“:”分隔。请求头部通知服务器有关于客户端请求的信息。

常用的请求头有：

字段|说明
-|-
Accept|表示浏览器支持的 MIME 类型
Accept—Charset|指定客户端接受的字符集
Accept-Encoding|浏览器支持的压缩类型
Accept-Language|浏览器支持的语言类型，并且优先支持靠前的语言类型
Authorization|用于证明客户端有权查看某个资源
Cache-Control|指定请求和响应遵循的缓存机制
Connection|当浏览器与服务器通信时对于长连接如何进行处理：close/keep-alive
Cookie|向服务器返回cookie，这些cookie是之前服务器发给浏览器的
Host|请求的服务器URL
Referer|该页面的来源URL
User-Agent|用户客户端的一些必要信息

#### 空行
最后一个请求头之后是一个空行，发送回车符和换行符，通知服务器以下不再有请求头。

#### 请求数据
请求数据不在GET方法中使用，而是在POST方法中使用。POST方法适用于需要客户填写表单的场合。与请求数据相关的最常使用的请求头是Content-Type和Content-Length。

### HTTP响应报文
HTTP响应也由三个部分组成，分别是：状态行、响应报头、响应正文。
```
<status-line> 状态行
<headers> 响应报头
<blank line> 空行
<response-body> 响应正文
```
#### 状态行
状态行（status line）通过提供一个状态码来说明所请求的资源情况。

状态行格式如下：
```
HTTP-Version Status-Code Reason-Phrase CRLF
```
其中，HTTP-Version表示服务器HTTP协议的版本；Status-Code表示服务器发回的响应状态代码；Reason-Phrase表示状态代码的文本描述。状态代码由三位数字组成，第一个数字定义了响应的类别，且有五种可能取值。

状态代码的具体意义在我的上一篇博客中有详细的介绍，各位可以移步查阅。

#### 响应报头
下面是一些常用的响应报头：

字段|说明
-|-
Cache-Control|告诉浏览器或者其他客户，什么环境可以安全地缓存文档
Connection|当client和server通信时对于长链接如何进行处理
Content-Encoding| 数据在传输过程中所使用的压缩编码方式
Content-Type|数据的类型
Date|数据从服务器发送的时间
Expires|应该在什么时候认为文档已经过期，从而不再缓存它？
Location|用于重定向接受者到一个新德位置。如当域名更换时。
Server|服务器名字。Servlet一般不设置这个值，而是由Web服务器自己设置
Set-Cookie|设置和页面关联的cookie
Transfer-Encoding|数据传输的方式

例子：
```
HTTP/1.1 200 OK
Date: Sat, 31 Dec 2005 23:59:59 GMT
Content-Type: text/html;
charset=ISO-8859-1
Content-Length: 122

<html><head><title>Wrox Homepage</title></head><body><!-- body goes here --></body></html>
```
