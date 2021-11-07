## 查看请求
利用网页浏览器的开发者工具，一般F12就可进入，然后在Network选项卡可以观察浏览器的请求和服务器返回的内容等。  
Ajax有特殊的请求类型，xhr  
点击查看更多的信息，可以看见Response headers和Request headers等，在Request headers里有一个X-Requested-With:XMLHttpRequest，这就标记了请求为Ajax请求。  
点击Preview就可查看响应内容，Response可查看真实的响应内容  

## 过滤请求
通过network选项卡下方的过滤功能，选择类型为xhr就可观察所有Ajax请求  