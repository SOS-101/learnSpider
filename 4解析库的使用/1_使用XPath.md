## XPath常用规则
nodename        选取此节点的所有子节点  
/               从当前节点选取子节点  
//              从当前节点选取子孙节点  
.               选取当前节点  
..              选取当前节点的父节点  
@               选取属性  


//title[@lang='eng']    选取所有title节点，且lang属性值为eng  


## 实例引入
``` python
from lxml import etree

#html text
text = '''

html = etree.HTML(text)
result = etree.tostring(html)
print(result.decode('utf-8'))
'''
```
``` python
from lxml import etree

html = etree.parse('./html.txt',etree.HTMLParser())
result = etree.tostring(html)
print(result.decode('utf-8'))
```

## 所有节点
一般以//开头的XPath规则来选取符合要求的节点  

``` python
from lxml import etree

html = etree.parse('./html.txt',etree.HTMLParser())
result = html.xpath('//*')
print(result)
```

``` python
from lxml import etree

html = etree.parse('./html.txt',etree.HTMLParser())
result = html.xpath('//li')
print(result)
print(result[0])
```

## 子节点

利用/或//来查找元素的子节点或者子孙节点  
``` python
from lxml import etree

html = etree.parse('./html.txt',etree.HTMLParser())
result = html.xpath('//li/a')
print(result)
```

``` python
from lxml import etree

html = etree.parse('./html.txt',etree.HTMLParser())
result = html.xpath('//ui//a')
print(result)
```

## 父节点
通过..或parent::来获取父节点  
``` python
from lxml import etree

html = etree.parse('./html.txt',etree.HTMLParser())
result = html.xpath('//a[@href="link4.html"]/../@class')
print(result)
```
``` python
from lxml import etree

html = etree.parse('./html.txt',etree.HTMLParser())
result = html.xpath('//a[@href="link4.html"]/parent::*/@class')
print(result)
```
## 属性匹配
可以用@来进行过滤  
 
``` python
from lxml import etree

html = etree.parse('./html.txt',etree.HTMLParser())
result = html.xpath('//li[@class="item-0"]')
print(result)
```

## 文本获取

用XPath的text()方法获取节点的文本  
``` python
from lxml import etree

html = etree.parse('./html.txt',etree.HTMLParser())
result = html.xpath('//li[@class="item-0"]/a/text()')
print(result)
```

``` python
from lxml import etree

html = etree.parse('./html.txt',etree.HTMLParser())
result = html.xpath('//li[@class="item-0"]//text()')
print(result)
```

## 属性获取
还可以利用@来获取属性值  

``` python
from lxml import etree

html = etree.parse('./html.txt',etree.HTMLParser())
result = html.xpath('//li/a/@href')
print(result)
```

## 属性多值匹配
有时候节点属性值有多个，这时用@就不行了，可以用contains函数  

``` python
from lxml import etree

text = '''
<li class="li li-first"><a href="link.html">first item</a></li>
'''

html = etree.HTML(text)
result = html.xpath('//li[contains(@class,"li")]/a/text())
```

## 多属性匹配
有时候需要通过多个属性值来确定一个节点，这是可以利用and运算符  
``` python
from lxml import etree

text = '''
<li class="li li-first" name="item"><a href="link.html">first item</a></li>
'''

html = etree.HTML(text)
result = html.xpath('//li[contains(@class,"li" and @name="item")]/a/text())
```

XPath中的一些运算符  
or          或  
and         与  
mod         计算除法的余数  
|           计算两个节点集  
\+          加法  
\-          减法  
\*          乘法  
div         除法  
=           等于  
!=          不等于  
<           小于  
<=          小于等于  
\>          大于  
\>=         大于等于

## 按序选择
我们可以通过[]来选择匹配节点里的特定节点，里面可以是从1开始的值，或者函数，或不等式  

## 节点轴选择
前面的parent::就属于节点轴选择  
其余轴还有ancestor:: child:: following-sibling:: following::  attribute:: 等轴  




