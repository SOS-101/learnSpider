Ajax，全称Asynchronous JavaScript and XML，即异步的JavaScript和XML。不是一门编程语言，而是利用JavaScript在保证页面不被刷新、页面链接不改变的情况下与服务器交换数据并更新部分网页的技术  

## 实例引入
在浏览一些网页的是否，我们往下浏览，会发现会有加载的动画等，这里就有Ajax的应用  

## 基本原理
发送Ajax请求到更新网页的过程一般为3步  
1. 发送请求  
   ``` JavaScript
   var xmlhttp;
   if (window.XMLHttpRequest){
       xmlhttp = new XMLHttpRequest();
   } else {
       xmlhttp = new ActionXObject("Microsoft.XMLHTTP");
   }
   xmlhttp.onreadystatechange=function(){
       if (xmlhttp.readyState==4 && xmlhttp.status==200){
           document.getElementById("myDiv").innerHTML = xmlhttp.responseText;
       }
   }
   xmlhttp.open("POST","/ajax",true);
   xmlhttp.send();
   ```
2. 解析内容
   获取服务器响应的数据后，可以利用JavaScript来解析数据等  
3. 渲染网页
   解析完数据内容等，利用JavaScript就可以渲染页面了  


