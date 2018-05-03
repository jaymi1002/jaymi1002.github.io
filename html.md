# HTML 知识点
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
