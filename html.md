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

### iframe有什么缺点
1、页面样式调试麻烦，出现多个滚动条；
2、浏览器的后退按钮失效；
3、过多会增加服务器的HTTP请求；
4、小型的移动设备无法完全显示框架；
5、产生多个页面，不易管理；
6、不容易打印；
7、代码复杂，无法被一些搜索引擎解读。

### h1/title，b/strong，i/em 的区别
1. b/strong:两者虽然在网页中显示效果一样，但实际目的不同。 <b\>这个标签对应 bold，即文本加粗，其目的仅仅是为了加粗显示文本，是一种样式／风格需求；
<strong\>这个标签意思是加强字符的语气，表示该文本比较重要，提醒读者／终端注意。为了达到这个目的，浏览器等终端将其加粗显示；
总结：<b\>为了加粗而加粗，<strong\>为了标明重点而加粗，也可以用其它方式来强调，比如下划线，比如字体加大，比如红色，等等，可以通过css来改变strong的具体表现。
2. i/em:同样，I是Italic(斜体)，而em是emphasize(强调)。
3. h1/title 从网站角度看，title更重于网站信息。title可以直接告诉搜索引擎和用户这个网站是关于什么主题和内容的。
从文章角度看，h1则是用于概括文章主题。用户进入内容页，想看到的当然就是文章的内容，h1文章标题就是最重要的。文章标题最好只有一个，多个h1会导致搜索引擎不知道这个页面哪个标题内容最重要，导致淡化这个页面的标题和关键词，起不到突出主题的效果。
区别：
h1突出文章主题，面对用户，更突出其视觉效果，突出网站标题或关键字用title。一篇文章，一个页面最好只用一个h1，多个h1会稀释主题。一个网站可以有多个title,最好一个单页用一个title，以便突出网站页面主体信息，从seo看，title权重比h1高，适用性比h1广。标记了h1的文字页面给予的权重会比页面内其他权重高很多。一个好的网站是h1和title并存，既突出h1文章主题，又突出网站主题和关键字。达到双重优化网站的效果。

### HTML5的离线储存怎么使用，工作原理能不能解释一下？
>通过Manifest; Manifest是一个简单的 文本文件，它的扩展名是任意 的，定义需要缓存的文件、资源，当第一次打开时，浏览器会自动缓存相应的资源。 
#### Manifest 的特点： 
+ 离线浏览：即当网络断开时，可以继续访问你的页面。 
+ 访问速度快：将文件缓存到本地，不需每次都从网络上请求。 
+ 稳定性：做了Manifest缓存，遇到突发网络故障或者服务器故障，继续访问本地缓存。 
#### 使用： 
首先创建一个和html同名的manifest文件，比如页面为index.html，那么可以建一个index.manifest的文件，然后给index.html的html标签添加如下属性即可： 
或 
1. manifest 的引入可以使绝对路径也可以是相对路径 
2. manifest文件你可以保存为任意的扩展名，但mine-type 必须是 text/cache-manifest。 
3. manifest 标签应该包含到你需要缓存资源的页面，当第一次打开该页面时，浏览器会解析该页面中的mainfest，并缓存里面列举的资源，同时该页面也会自动会被浏览器缓存，即使该页面没有在Manifest中列出。 
4. HTML5缓存可以做到以下几点：1>实现图片存在客户端；2>实现跨域共享客户端缓存；3>做到真正的离线访问WEB应用；4>实现客户端的数据库。 
在H5之前，是由cookie实现客户端的缓存，将缓存信息带在HTTP请求头上，大小只有4k，会造成Domain污染.
#### H5的几种存储形式： 
1>本地存储(localstorage && sessionstorage)： 
存储形式：key–>value过期时间：永久存储，永不失效，除非手动删除 大小：官方给出的文档是每个域名5M，所以需要抛出异常处理 
浏览器支持情况：IE8+、Firefox、Safari3.2+、Chrome、Opera 
使用方法：localstorage API介绍,resource里面看,在console里面操作.
1.getItem:取 localstorage记录 setItem:设置 removeItem:移除key:去拿一个索引 clear:删掉，清除（这个是删除掉了全部） 
H5可以存储的东东：数组、json数据、图片、脚本、样式文件 
#### 原理： 
HTML5的离线存储是基于一个新建的.appcache文件的，通过这个文件上的解析清单离线存储资源，这些资源就会像cookie一样被存储了下来。之后当网络在处于离线状态下时，浏览器会通过被离线存储的数据进行页面展示。

### 页面可见性（Page Visibility API） 可以有哪些用途？
> 页面可见性： 就是对于用户来说，页面是显示还是隐藏, 所谓显示的页面，就是我们正在看的页面；隐藏的页面，就是我们没有看的页面。 因为，我们一次可以打开好多标签页面来回切换着，始终只有一个页面在我们眼前，其他页面就是隐藏的，还有一种就是.........，(把浏览器最小化，所有的页面就都不可见了)。
* API 很简单，document.hidden 就返回一个布尔值，如果是true, 表示页面可见，false 则表示，页面隐藏。  不同页面之间来回切换，触发visibilitychange事件。 还有一个document.visibilityState, 表示页面所处的状态，取值：visible, hidden 等四个。
<br/>
<pre> document.addEventListener("visibilitychange", function(){
    if(document.hidden){
        document.title ="hidden";
    }else {
        document.title = "visibile";
    }
})</pre>
