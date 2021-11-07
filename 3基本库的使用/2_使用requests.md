通过requests库，我们可以更方便的处理Cookie、登录验证、代理设置等   

## 基本用法
### 准备工作
得把requests库安装了  

### 实例引入
``` python
import requests

r = requests.get('https://www.baidu.com/')
print(type(r))
print(r.status_code)
print(type(r.text))
print(r.text)
print(r.cookies)
```
通过requests里的get函数来提交GET请求   
其余请求方式   
``` python 
requests.post()
requests.put()
requests.delete()
requests.head()
requests.options()
...
```

### GET请求
- 基本实例  

``` python
from requests
r = requests.get('http://httpbin.org/get')
print(r.text)

r = requests.get('http://httpbin.org/get?name=tao&age=20')

data = {
    'name':'tao',
    'age':20
}

r = requests.get('http://httpbin.org/get',params=data)

print(type(r.text))
print(r.json)
print(type(r.json()))
```
- 爬取网页  
 
``` python
import requests,re

headers = {
    'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.54 Safari/537.36'
}
r = requests.get("https://www.zhihu.com/explore",headers=headers)
pattern = re.compile('explore-feed.*?question_link.*?>(.*?)</a>',re.S)
titles = re.findall(pattern,r.text)
print(titles)
```

- 抓取二进制数据  

``` python
import request

r = requests.get("https://github.com/favicon.ico")
with open('favicon.ico','wb') as f:
    f.write(r.content)
```

- 添加headers   

``` python
import requests

headers = {
    'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.54 Safari/537.36'
}
r = requests.get("https://www.zhihu.com/explore",headers=headers)
print(r.text)
```

- POST请求   

``` python
import request

data = {
    'name':'tao',
    'age':20
}

r = requests.post('http://httpbin.org/post',data=data)
print(r.text)
```

- 响应  

在我们请求了一个网页什么的，之后，我们就会得到响应，之前的text，content等都是响应的内容   

``` python
import requests

r = requests.get('http://www.jianshu.com')
print(type(r.status_code),r.status_code)
print(type(r.headers),r.headers)
print(type(r.cookies),r.cookies)
print(type(r.url),r.url)
print(type(r.history),r.history)
```

## 高级用法
文件上传、Cookies设置，代理设置   

### 文件上传

``` python
import requests

files = {
    'file':open('favicon.ico','rb')
}

r = request.post('http://httpbin.org/post',files=files)
print(r.text)
```

### Cookies设置
``` python
import requests

headers = {
    'Cookie':'',
    'Host':'www.zhihu.com',
    'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.54 Safari/537.36'
}

r = requests.get('https://www.zhihu.com',headers=headers)
print(r.text)
```

### 会话维持
使用get或者post方法，每请求一次，就会开始一个新的会话，如果使用Cookies时，得重复设置。   
这里就可以利用Session对象，来维持一个会话。   

``` python
import requests

requests.get('http://httpbin.org/cookies/set/number/123456789')
r = requests.get('http://httpbin.org/cookies')
print(r.text)
```
``` python
import requests

s = requests.Session()
s.get('http://httpbin.org/cookies/set/123456789')
r = s.get('http://httpbin.org/cookies')

print(r.text)
```

### SSL证书验证

``` python
import request

response = requests.get('https://www.12306.cn',verify=False)
print(response.status_code)
```
``` python
import request
from requests.packages import urllib3

urllib3.disable_warnings()
response = requests.get('https://www.12306.cn',verify=False)
print(response.status_code)
```
``` python
import request
import logging

logging.captureWarnings(True)
response = requests.get('https://www.12306.cn',verify=False)
print(response.status_code)
```
``` python
import request

response = requests.get('https://www.12306.cn',cert=('/path/server.crt','/path/key'))
print(response.status_code)
```

### 代理设置

``` python
import requests

proxies = {
    "http":"http://10.10.1.10:3128",
    "https":"http://10.10.1.10:1080"
}

requests.get("https://www.taobao.com",proxies=proxies)
```

代理使用HTTP Basic Auth时     
``` python
import requests

proxies = {
    "http":"http://user:password@10.10.1.10;3128/",
}
requests.get('https://www.taobao.com',proxies=proxies)
```

代理使用SOCKS协议的代理   
首先得安装相应的库   
pip install 'requests[socks]'
``` python
import requests

proxies = {
    "http":'socks5://user:password@host:port'
}
requests.get(url,proxies=proxies)
```

### 超时设置
实际，请求分为连接和读取两阶段   
可以通过设置超时来处理请求响应过慢，也即网不好的情况吧   

### 身份认证
自带身份认证   
``` python 
import requests
from requests.auth import HTTPBasicAuth

r = requests.get('http://localhost:5000',auth=HTTPBasicAuth('username','password'))
r = requests.get('http://localhost:5000',auth=('username','password')) //can pass a tuple
```
还有其他认证方式，比如OAuth   

### Prepared Request

``` python
from requests import Request,Session

url = 'http://httpbin.org/post'
data = {
    'name':'tao'
}
headers = {
    'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.54 Safari/537.36'
}
s = Session
req = Request('POST',url,data=data,headers=headers)
prepped = s.prepare_request(req)
r = s.send(prepped)
print(r.text)
```