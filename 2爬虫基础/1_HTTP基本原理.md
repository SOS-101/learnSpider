## URI 和 URL
URL 是 URI的子集  
还有个 URN也是URI的子集  

## 超文本
HTML就属于超文本，其里面除了文字还可以包含图片，音频，视频等多媒体资源  

## HTTP和HTTPS
http和https都是应用层协议，其他应用层协议还有ftp，sftp...  
http一般明文传输  
https的安全基础是ssl，及通过ssl加密传输，也会检查CA证书，有时请求的网页显示警告，可能是因为它们的CA证书是自行签发的。  

## http请求过程
当我们输入网址，并访问时，浏览器就会对服务器发出http请求，服务器根据请求信息做出相关响应，通常可以根据返回的信息判断请求是否成功，以及未成功的大致原因  
可以通过浏览器的开发工具的网络工具来观察  

## 请求
请求主要分为4个部分  
### 请求方法
常用的请求方法有GET和POST  
其主要区别；1、GET请求的参数通常包含在URL中，POST通过请求体传递参数。2、GET请求传递参数通常有大小限制，而POST没有  
其他请求方法还有HEAD、PUT、DELETE、CONNECT、OPTIONS、TRACE等  
 
### 请求地址
即URL，来唯一确定要访问的资源  

### 请求头
用来说明服务器所需要的附加信息，比较重要的信息有Cookies、Refer、User-Agent等  
Accept：请求报头域，用来说明客户端接收什么类型的资源信息  
Accept-Language：用来说明客户端可接受的语言类型  
Accept-Encoding；用来说明客户端接收的编码类型  
Host；用来指定请求资源主机的ip和端口，为请求资源主机ip或者网关ip  
Cookie：常用复数形式Cookies，网站用来辨识用户用来跟踪会话而存储的本地数据  
Refer；表示请求从哪个页面发来的  
User-Agent；爬虫里用来伪装成浏览器  
Content-Type；用来表示请求的具体媒体类型信息，MIME类型  

### 请求体
请求体通常用来承载POST请求的表单数据等  
也可以用来传输json数据或者上传文件  
  
## 响应
响应内容大致分为3个部分  
### 响应状态码
用来表示服务器的响应状态  
200 成功      
404 未找到  
504 网关超时  

### 响应头
包含了服务器对请求的应答信息  
Date：标识产生时间  
Last-Modified：指定资源最后修改的时间  
Content-Encoding：指定响应内容的编码  
Server：一些关于服务器的信息    
Content-Type：文档类型    
Expires：指定响应的过期时间，与代理服务器和缓存资源有关   

### 响应体
响应体包含了我们最想要的信息吧，比如HTML文档、图片二进制数据、json等等  

