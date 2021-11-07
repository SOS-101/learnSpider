## 初始化
pyquery初始化需要HTML文本来初始化pyquery对象  
初始化方式有几种，比如直接传入字符串、URL、文件名等等  

- 字符串初始化  
  ``` python
  from pyquery import PyQuery as pq

  html = '''
  '''
  doc = pq(html)
  print(doc('li'))
  ```

- URL初始化
  ``` python
  from pyquery import PyQuery as pq
  doc = pq(url='https://cuiqingcai.com')
  print(doc('title'))
  ```
  ``` python
  from pyquery import PyQuery as pq
  import requests

  doc = pq(requests.get('https://cuiqingcai.com'.text))
  print(doc('title'))
  ```
- 文件初始化
  ``` python
  from pyquery import PyQuery as pq

  doc = pq(filename='demo.html')
  print(doc('li'))
  ```

## 基本CSS选择器
``` python
from pyquery import PyQuery

html = '''
'''
doc = pq(html)
print(doc('#container .list li'))
print(type(doc('#container .list li')))
```

## 查找节点
- 子节点
  find()方法查找所有子孙节点  
  children()查找所有直接子节点  
  都是可传入CSS选择器

- 父节点
  parent()方法查找直接父节点
  parents()方法查找祖先节点，可传入CSS选择器

- 兄弟节点
  siblings()方法返回兄弟节点，可传入CSS选择器

- 遍历
  ``` python
  from pyquery import PyQuery as pq

  doc = pq(html)
  lis = doc('li').items()
  print(type(lis))
  for li in lis:
      print(li,type(li))
  ```
- 获取信息
  - 获取属性
  节点属性利用attr方法获取或者通过attr属性获取  
  这些只能获取对象第一个节点属性，当对象包含多个节点时，利用遍历

  - 获取文本
  text()返回文本内容，返回对象所有节点的文本  
  html()返回HTML文本，只返回对象第一个节点的HTML文本，其余需要遍历

## 节点操作
- addClass removeClass
  动态改变节点属性

- attr text html
  修改节点属性、文本、HTML

- remove

## 伪类选择器

``` python
from pyquery import PyQuery as pq

html = '''
'''
doc = pq(html)
li = doc('li:first-child')
print(li)
li = doc('li:last-child')
print(li)
li = doc('li:nth-child(2)')
print(li)
li = doc('li:gt(2)')
print(li)
li = doc('li:nth-child(2n)')
print(li)
li = doc('li:contains(second')
print(li)
```


