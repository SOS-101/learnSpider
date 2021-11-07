Selenium是一个自动化测试工具，可以驱动浏览器。  
## 基本使用

``` python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.support.wait import WebDriverWait

brower = webdriver.Chrome()
try:
    brower.get('https://www.baidu.com')
    input = brower.find_element_by_id('kw')
    input.send_keys('Python')
    input.send_keys(Keys.ENTER)
    wait = WebDriverWait(brower,10)
    wait.until(EC.presence_of_element_located((By.ID,'content_left')))
    print(brower.current_url)
    print(brower.get_cookies())
    print(brower.page_source)
finally:
    brower.close()
```

## 声明浏览器对象
``` python
from selenium import webdriver

brower = webdriver.Chrome()
brower = webdriver.Firefox()
brower = webdriver.Edge()
brower = webdriver.PhantomJS()
brower = webdriver.Safari()
```

## 访问页面
``` python
from selenium import webdriver

brower = webdriver.Chrome()
brower.get("https://www.taobao.com")
print(brower.page_source)
brower.close()
```

## 查找节点
- 单个节点
  ``` python
  from selenium import webdriver

  brower = webdriver.Chrome()
  brower.get('https://www.taobao.com')
  input_first = brower.find_element_by_id('q')
  input_second = brower.find_element_by_css_selector('#')
  input_third = brower.find_element_by_xpath('//*[@id="q"]')
  print(input_first,input_second,input_third)
  brower.close()
  ```
  ``` python
  from selenium import webdriver
  from selenium.webdriver.common.by import By

  brower = webdriver.Chrome()
  brower.get('https://www.taobao.com')
  input_first = brower.find_element(By.ID,'q')
  print(input_first)
  brower.close()
  ```
- 多个节点
  ``` python
  from selenium import webdriver

  brower = webdriver.Chrome()
  brower.get('https://www.taobao.com')
  lis = brower.find_elements_by_css_selector('.service-bd li')
  print(lis)
  brower.close()
  ```

## 节点交互
``` python
from selenium import webdriver

brower = webdriver.Chrome()
brower.get('https://www.taobao.com')
input = brower.find_element_by_id('q')
input.send_keys('iPhone')
time.sleep(1)
input.clear()
input.send_keys('iPad')
button = brower.find_element_by_class_name('btn-search')
button.click()
```
## 动作链
``` python
from selenium import webdriver
from selenium.webdriver import ActionChains

brower = webdriver.Chrome()
url = 'http://www.runoob.com/try/try.php?filename=jqueryui-api-droppable'
brower.get(url)
brower.switch_to_frame('iframeResult')
source = brower.find_element_by_css_selector('#draggable')
target = brower.find_element_by_css_selector('#droppable')
actions = ActionChains(brower)
actions.drag_and_drop(source,target)
actions.perform()
```

## 执行JavaScript
``` python
from selenium import webdriver

brower = webdriver.Chrome()
brower.get('https://www.zhihu.com/explore')
brower.execute_script('window.scrollTo(0,document.body.scrollHeight)')
brower.execute_script('alert("To buttom")')
```

## 获取节点信息
- 获取属性
  ``` python
  from selenium import webdriver

  brower = webdriver.Chrome()
  url = 'https://www.zhihu.com/explore'
  brower.get(url)
  logo = brower.find_element_by_id('zh-top-link-logo')
  print(logo)
  print(logo.get_attribute('class'))
  ```
- 获取文本
  ``` python
 
  ```
- 获取id、位置、标签名和大小
  ``` python
   from selenium import webdriver

  brower = webdriver.Chrome()
  url = 'https://www.zhihu.com/explore'
  brower.get(url)
  input = brower.find_element_by_class_name('zu-top-add-question')
  print(input.id)
  print(input.location)
  print(input.tag_name)
  print(input.size)
  ```

## 切换Frame
``` python
import time
from selenium import webdriver
from selenium.common.exceptions import NoSuchElementException

brower = webdriver.Chrome()
url = 'http://www.runoob.com/try/try.php?filename=jqueryui-api-droppable'
brower.get(url)
brower.switch_to.frame('iframeResult')
try:
  logo = brower.find_element_by_class_name('logo')
except NoSuchElementException:
  print('No LOGO')
brower.switch_to.parent_frame()
logo = brower.find_element_by_class_name('logo')
print(logo)
print(logo.text)
```

## 延时等待

- 隐式等待
  ``` python
  from selenium import webdriver

  brower = webdriver.Chrome()
  brower.implicitly_wait(10)
  url = 'https://www.zhihu.com/explore'
  brower.get(url)
  input = brower.find_element_by_class_name('zu-top-add-question')
  print(input)
  ```
- 显式等待
  ``` python
  from selenium import webdriver
  from selenium.webdriver.common.by import By
  from selenium.webdriver.support.ui import WebDriverWait
  from selenium.webdriver.support import expected_conditions as EC

  brower = webdriver.Chrome()
  brower.get('https://www.taobao.com/')
  wait = WebDriverWait(brower,10)
  input = wait.until(EC.presence_of_element_located((By.ID,'q')))
  button = wait.until(EC.element_to_be_clickable((By.CSS_SELECTOR,'.btn-search')))
  print(input,button)
  ```

## 前进后退

``` python
import time
from selenium import webdriver

brower = webdriver.Chrome()
brower.get('https://www.baidu.com/')
brower.get('https://www.taobao.com/')
brower.get('https://www.python.com/')

brower.back()
time.sleep(1)
brower.forward()
brower.close()
```
## Cookies
``` python
from selenium import webdriver

brower = webdriver.Chrome()
brower.get('https://www.zhihu.com/explore')
print(brower.get_cookies())
brower.add_cookie({'name':'name','domain':'www.zhihu.com','value':'germey'})
print(brower.get_cookies())
brower.delete_all_cookies()
print(brower.get_cookies())
```
## 选项卡管理
``` python
import time
from selenium import webdriver

brower = webdriver.Chrome()
brower.get('https://www.baidu.com')
brower.execute_script('window.open()')
print(brower.window_handles)
brower.switch_to_window(brower.window_handles[1])
brower.get('https://www.taobao.com')
time.sleep(1)
brower.switch_to_window('brower.window_handles[0])
brower.get('https://python.org')
```
## 异常处理
``` python
from selenium import webdriver
from selenium.common.exceptions import TimeoutException,NoSuchElementException

brower = webdriver.Chrome()
try:
  brower.get('https://www.baidu.com')
except TimeoutException:
  print('Time Out')
try:
  brower.fine_element_by_id('hello')
except NoSuchElementException:
  print('No Element')
finally:
  brower.close()
```