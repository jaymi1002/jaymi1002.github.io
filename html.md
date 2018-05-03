# HTML 浏览器相关 知识点
## !DOCTYPE html
+ document type HyperText Mark-up Language。指定当前文本类型，以严格模式去解析展示HTML。好处：避免浏览器的怪异模式。怪异模式：浏览器向后兼容。
## SGML
+ 是标准通用标记语言，简单来说，就是比XML和HTML更早的标准，XML和HTML都是由SGML发展而来的。但是HTML5不是。
## DTD
+ 规定XML和HTML的特定版本中允许有什么，不允许有什么。文档类型定义，是一套关于标记性语言的语法规则，对文档规范声明。Strict（严格型）、transitional（兼容型）、frameset（框架型）。
## H5为什么只需要添加DOCTYPE html
+ html4.0.1中的doctype需要对DTD进行引用，因为html4.0.1是基于SGML。HTML5 不是基于SGML，因此不需要对DTD进行引用，但是需要doctype来规范浏览器的行为。
## Cookie和Session
+ Cookie：存储在客户端。指某些网站为了辨别用户身份，进行session跟踪而存储在用户本地存储中上的数据（通常经过加密），是实现session的一种方式。一般用途：登录或者注册之后，服务端通过setCookies来把信息放到浏览器的cookie中，每次请求，http header中都会把cookie带过去，进行验证。
+ Session：是存储在服务端的一种数据结构，是保存用户会话，第一次创建session时，会把把sessionID，种到浏览器的cookie中，每次请求时，都会通过cookie把sessionID带给服务端，因此可以进行身份识别。

## Cookie、localStorge、sessionStorge的区别：
+ Cookie数据始终都会在http中携带，即使你不需要。即会在浏览器中来回传递，cookie存储大小不能超过4k，因为每次HTTP请求都会携带Cookie。
+ SessionStorage和localstorage不会把数据发给服务端，仅本地保存，sessionStorage和localStorage存储大小是5M。
+ 数据有效期不同，sessionStorage：仅在当前浏览器未关闭时有效，不能长久保存。LocalStorage：始终有效，浏览器窗口关闭也能一直保存。可以作为持久数据；cookie只在设置过期的时间之前一直有效，即使浏览器关闭。
+ 作用域不同，sessionStorage不在不同的浏览器窗口共享数据，即时是同一个页面；localStorage在所有同源窗口中是共享的；cookie也是在同源窗口是共享的。
+ Web Storage API能够支持监听机制，可以实现同源多窗口数据通信。

## 浏览器内核
+ 浏览器内核又可以分成两部分：渲染引擎(layout engineer 或者 Rendering Engine)和 JS 引擎。它负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入 CSS 等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。所有网页浏览器、电子邮件客户端以及其它需要编辑、显示网络内容的应用程序都需要内核。JS 引擎则是解析 Javascript 语言，执行 javascript 语言来实现网页的动态效果。最开始渲染引擎和 JS 引擎并没有区分的很明确，后来 JS 引擎越来越独立，内核就倾向于只指渲染引擎。有一个网页标准计划小组制作了一个 ACID 来测试引擎的兼容性和性能。内核的种类很多，如加上没什么人使用的非商业的免费内核，可能会有 10 多种，但是常见的浏览器内核可以分这四种：Trident、Gecko、Blink、Webkit。
### 主流浏览器内核
1. IE浏览器内核：Trident内核，也是俗称的IE内核；
2. Chrome浏览器内核：统称为Chromium内核或Chrome内核，以前是Webkit内核，现在是Blink内核；
3. Firefox浏览器内核：Gecko内核，俗称Firefox内核；
4. Safari浏览器内核：Webkit内核；
5. Opera浏览器内核：最初是自己的Presto内核，后来加入谷歌大军，从Webkit又到了Blink内核；
6. 360浏览器、猎豹浏览器内核：IE+Chrome双内核；
7. 搜狗、遨游、QQ浏览器内核：Trident（兼容模式）+Webkit（高速模式）；
8. 百度浏览器、世界之窗内核：IE内核；
9. 2345浏览器内核：好像以前是IE内核，现在也是IE+Chrome双内核了；
10. UC浏览器内核：这个众口不一，UC说是他们自己研发的U3内核，但好像还是基于Webkit和Trident，还有说是基于火狐内核。。

## link和import
+ 区别1：link是XHTML标签，除了加载CSS外，还可以定义RSS等其他事务；@import属于CSS范畴，只能加载CSS。
+ 区别2：link引用CSS时，在页面载入时同时加载；@import需要页面网页完全载入以后加载。
+ 区别3：link是XHTML标签，无兼容问题；@import是在CSS2.1提出的，低版本的浏览器不支持。
+ 区别4：link支持使用Javascript控制DOM去改变样式；而@import不支持。

## WebSocket解释及如何兼容低版本浏览器
> 相比较HTTP协议只能单向的从客户端发起，websocket可以实现双向推送消息。
#### 特点包括：
（1）建立在 TCP 协议之上，服务器端的实现比较容易。
（2）与 HTTP 协议有着良好的兼容性。默认端口也是80和443，并且握手阶段采用 HTTP 协议，因此握手时不容易屏蔽，能通过各种 HTTP 代理服务器。
（3）数据格式比较轻量，性能开销小，通信高效。
（4）可以发送文本，也可以发送二进制数据。
（5）没有同源限制，客户端可以与任意服务器通信。
（6）协议标识符是ws（如果加密，则为wss），服务器网址就是 URL。
### 如何处理低版本不兼容问题：
> 由于websocket是H5的新特性，不支持H5的低版本浏览器可以使用一下方法来代替。
1. 使用轮询或者长连接实现伪websocket的。
2. 使用flash实现一个websock客服端。
