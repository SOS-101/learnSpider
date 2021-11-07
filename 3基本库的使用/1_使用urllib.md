urllib是Python内置的http请求库，其包括下面几个模块  
request  
error   
parse   
robotparse   
可以通过httpbin.org来测试请求  

## 发送请求
使用request模块  
### urlopen()
``` python
request.urlopen(
    url,
    data=None,
    timeout=<object object at 0x000001E30907CCA0>,
    *,
    cafile=None,
    capath=None,
    cadefault=False,
    context=None,
)
```
简单的请求可以直接将url字符串传递给它，其他参数都有默认值  
该方法返回一个HTTPResponse对象，其有挺多方法和属性，用于获取返回的数据  


### Request
``` python
request.Request(
    url,
    data=None,
    headers={},
    origin_req_host=None,
    unverifiable=False,
    method=None,
)
```
可以利用这个类将更多的信息封装起来，然后通过 urlopen方法来请求，也只有url这个必须的参数，其他根据需要传递  

### 高级用法
Handler，用来处理验证登录，Cookies，代理设置等  
urllib.request 里的 BaseHandler是其他Handler的父类   

HTTPDefaultErrorHandler  
HTTPRedirectHandler  
HTTPCookieProcessor  
ProxyHandler  
HTTPPasswordMgr  
HTTPBasicAuthHandler  
...


Opener，用来请求资源,OpenerDirector  
urlopen就是提供的一个Opener  
Opener有一个open方法  
利用Handler来构建Opener  

``` python
from urllib.request import HTTPPasswordMgrWithDefaultRealm,HTTPBasicAuthHandler,build_opener
from urllib.error import URLError

username = 'username'
password = 'password'
url = 'http://localhost:5000/'

p = HTTPPasswordMgrWithDefaultRealm()
p.add_password(None,url,username,password)
auth_handler = HTTPBasicAuthHandler(p)
opener = build_opener(auth_handler)

try:
    result = opener.open(url)
    html = result.read().decode('utf-8')
    print(html)
except URLError as e:
    print(e.reason)
```

``` python
from urllib.error import URLError
from urllib.request import ProxyHandler, build_opener

proxy_handler = ProxyHandler({
    'http':'http://127.0.0.1:9743',
    'https':'https://127.0.0.1:9743'
})

opener = build_opener(proxy_handler)

try:
    response = opener.open('https://www.baidu.com')
    print(response.read().decode('utf-8'))
except URLError as e:
    print(e.reason)
```

``` python
import http.cookiejar,urllib.request

cookie = http.cookiejar.CookieJar()
handler = urllib.request.HTTPCookieProcessor(cookie)
opener = urllib.request.build_opener(handler)
response = opener.open('http://www.baidu.com')
for item in cookie:
    print(item.name+"="+item.value)

filename = 'cookies.txt'
cookie = http.cookiejar.MozillaCookieJar(filename)
handler = urllib.request.HTTPCookieProcessor(cookie)
opener = urllib.request.build_opener(handler)
response = opener.open('http://www.baidu.com')
cookie.save(ignore_discard=True,ignore_expires=True)
```

## 处理异常
urllib.error 定义了该包里的异常，可以通过其处理异常  

### URLError
URLError类继承自OSError类，是error模块里异常类的基类，一般request模块抛出的异常都可以通过该类捕获  

### HTTPError
HTTPError是HTTP请求异常类，是URLError的子类  
 
## 解析链接
### urlparse()
### urlunparse()
### urlsplit()
### urlunsplit()
### urljoin()
### urlencode()
### parse_qs()
### parse_qsl()
### quote()
### unquote()

## 分析Robots协议
利用urllib的robotparse模块解析   