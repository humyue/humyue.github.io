---
layout: post
title:  "Python爬虫之Selenium的使用"
date:   2018-09-05 8:00:54
categories: Python
tags: Python爬虫 Python
author: Humy
---
* content
{:toc}






*本文为笔者根据Python静觅教程记录笔记，仅供学习使用*
>Selenium是自动化测试工具，支持多种浏览器，爬虫中主要用来解决JavaScript渲染的问题

### 1.基本使用

```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.support.wait import WebDriverWait
browser=webdriver.Chrome()
try:
    browser.get('http://www.baidu.com')
    input=browser.find_element_by_id('kw')
    input.send_keys('Python')
    input.send_keys(Keys.ENTER)
    wait=WebDriverWait(browser,10)
    wait.until(EC.presence_of_element_located((By.ID,'content_left')))
    print(browser.current_url)
    print(browser.get_cookies())
    print(browser.page_source)
finally:
    browser.close()
```

运行结果：

![运行结果图]({{ "/asserts/img/post/2018-9-05/01.png" | prepend: site.baseurl }})

### 2.声明浏览器对象

```
from selenium import webdriver
browser=webdriver.Chrome()
browser=webdriver.Firefox()
browser=webdriver.Edge()
browser=webdriver.PhantomJS()
browser=webdriver.Safari()
```

### 3.访问页面

```
from selenium import webdriver
browser=webdriver.Chrome()
browser.get('https://www.taobao.com')
print(browser.page_source)
browser.close()
```
### 4.单个元素

**查找方式有以下几种**

* find_element_by_name
* find_element_by_xpath
* find_element_by_link_text
* find_element_by_partial_link_text
* find_element_by_tag_name
* find_element_by_class_name
* find_element_by_css_selector

```
from selenium import webdriver
browser=webdriver.Chrome()
browser.get('https://www.taobao.com')
input_first=browser.find_element_by_id('q')
input_second=browser.find_element_by_css_selector('#q')
input_third=browser.find_element_by_xpath('//*[@id="q"]')
print(input_first,input_second,input_third)
browser.close()
```

输出：

![运行结果图]({{ "/asserts/img/post/2018-9-05/02.png" | prepend: site.baseurl }})

也可以这样写：

```
from selenium import webdriver
browser=webdriver.Chrome()
browser.get('https://www.taobao.com')
input_first=browser.find_element(By.ID,'q')
print(input_first)
browser.close()
```

### 5.多个元素

**查找方式有以下几种**

* find_elements_by_name
* find_elements_by_xpath
* find_elements_by_link_text
* find_elements_by_partial_link_text
* find_elements_by_tag_name
* find_elements_by_class_name
* find_elements_by_css_selector

```
from selenium import webdriver
browser=webdriver.Chrome()
browser.get('https://www.taobao.com')
lis=browser.find_elements_by_css_selector('.service-bd li')
print(lis)
browser.close()
```

同样的，也可以这样写：

```
from selenium import webdriver
browser=webdriver.Chrome()
browser.get('https://www.taobao.com')
lis=browser.find_elements(By.CSS_SELECTOR,'.service-bd li')
print(lis)
browser.close()
```

### 6.元素交互操作

```
from selenium import webdriver
import time
browser=webdriver.Chrome()
browser.get('https://www.taobao.com')
input=browser.find_element_by_id('q')
input.send_keys('iPhone')
time.sleep(1)
input.clear()
input.send_keys('iPad')
btn=browser.find_element_by_class_name('btn-search')
btn.click()
```

### 7.交互动作

```
from selenium import webdriver
from selenium.webdriver import ActionChains
browser=webdriver.Chrome()
url='http://www.runoob.com/try/try.php?filename=jqueryui-api-droppable'
browser.get(url)
browser.switch_to.frame('iframeResult')
source=browser.find_element_by_css_selector('#draggable')
target=browser.find_element_by_css_selector('#droppable')
actions=ActionChains(browser)
actions.drag_and_drop(source,target)
actions.perform()
```

### 8.执行JavaScript

```
from selenium import webdriver
browser=webdriver.Chrome()
browser.get('https://www.zhihu.com/explore')
browser.execute_script('window.scroll(0,document.body.scrollHeight)')
browser.execute_script('alert("To Button")')
```

### 9.获取元素信息

* 获取属性

```
from selenium import webdriver
browser=webdriver.Chrome()
browser.get('https://www.zhihu.com/explore')
logo=browser.find_element_by_id('zh-top-link-logo')
print(logo)
print(logo.get_attribute('class'))
```

运行结果：

![运行结果图]({{ "/asserts/img/post/2018-9-05/03.png" | prepend: site.baseurl }})

* 获取文本值

```
from selenium import webdriver
browser=webdriver.Chrome()
browser.get('https://www.zhihu.com/explore')
btn=browser.find_element_by_class_name('zu-top-add-question')
print(btn.text)
```

输出：`>>>提问`

* 获取ID,位置，标签名，大小

```
from selenium import webdriver
browser=webdriver.Chrome()
browser.get('https://www.zhihu.com/explore')
btn=browser.find_element_by_class_name('zu-top-add-question')
print(btn.id)
print(btn.location)
print(btn.tag_name)
print(btn.size)
```

输出：

```
>>>0.12090135319150486-1
>>>{'x': 758, 'y': 7}
>>>button
>>>{'height': 32, 'width': 66}
```

### 10.Frame

```
from selenium import webdriver
from selenium.common.exceptions import NoSuchElementException
browser=webdriver.Chrome()
url='http://www.runoob.com/try/try.php?filename=jqueryui-api-droppable'
browser.get(url)
browser.switch_to.frame('iframeResult')
source=browser.find_element_by_css_selector('#draggable')
print(source)
try:
    logo=browser.find_element_by_class_name('logo')
except NoSuchElementException:
    print('NO LOGO')
browser.switch_to.parent_frame()
logo=browser.find_element_by_class_name('logo')
print(logo)
print(logo.text)

```
输出：

![运行结果图]({{ "/asserts/img/post/2018-9-05/04.png" | prepend: site.baseurl }})

### 11.等待

* 隐式等待

>当时用了隐式等待执行测试的时候，如果webdriver没有在DOM中找到元素，将继续等待，超出设定时间后则抛出找不到元素的异常，换句话说，当查找元素或元素没有立即出现的时候，隐式等待将等待一段时间再查找DOM,默认时间是0秒

```
from selenium import webdriver
browser=webdriver.Chrome()
browser.implicitly_wait(10)
browser.get('https://www.zhihu.com/explore')
input=browser.find_element_by_class_name('zu-top-add-question')
print(input)
```

输出：

`>>><selenium.webdriver.remote.webelement.WebElement (session="0d00cb4aef1e538b402c41f34215e5df", element="0.36948754945206397-1")>`

* 显式等待

等待条件：

* title_is 标题是某内容
* title_contains 标题包含某内容
* presence_of_element_located 元素加载出，传入定位元组，如（By.ID,'p'）
* visibility_of_element_located 元素可见，传入定位元组
* visibility_of 可见，传入元素对象
* presence_of_all_element_located 所有元素加载出
* text_to_be_present_in_element 某个元素文本包含某文字
* text_to_be_present_in_element_value 某个元素值包含某文字
* frame_to_be_avaliable_and_switch_to_it_frame 加载并切换
* invisibility_of_element_located 元素不可见
* element_to_be_clickable 元素可点击
* staleness_of 判断一个元素是否仍在DOM,可判断页面是否已经刷新
* element_to_be_selected 元素可选择，传元素对象
* element_located_to_be_selected 元素可选择，传入定位元组
* element_selection_state_to_be 传入元素对象以及状态，相等返回True,否则返回Fasle
* element_located_selection_state_to_be 传入定位元组以及状态，相等返回True，否则返回False
* alert_is_present 是否出现Alert

```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.support.wait import WebDriverWait
browser=webdriver.Chrome()
browser.get('http://www.taobao.com')
wait=WebDriverWait(browser,10)
input=wait.until(EC.presence_of_element_located((By.ID,'q')))
button=wait.until(EC.element_to_be_clickable((By.CSS_SELECTOR,'.btn-search')))
print(input,button)
```

输出：

![运行结果图]({{ "/asserts/img/post/2018-9-05/05.png" | prepend: site.baseurl }})

### 12.前进后退

```
import time
from selenium import webdriver
browser=webdriver.Chrome()
browser.get('https://www.baidu.com/')
browser.get('https://www.taobao.com/')
browser.get('https://www.python.org/')
browser.back()
time.sleep(1)
browser.forward()
browser.close()
```

### 13.Cookies

```
from selenium import webdriver
browser=webdriver.Chrome()
browser.get('https://www.zhihu.com/explore')
print(browser.get_cookies())
browser.add_cookie({‘name’:'name','domian':'www.zhihu.com','value':'germey'})
print(browser.get_cookies())
browser.delete_all_cookies()
print(browser.get_cookies())
```

### 14.选项卡管理

```
import time
from selenium import webdriver
browser=webdriver.Chrome()
browser.get('https://www.baidu.com/')
browser.execute_script('window.open()')
print(browser.window_handles)
browser.switch_to_window(browser.window_handles(1))
browser.get('https://www.taobao.com')
time.sleep(1)
browser.switch_to_window(browser.window_handles(0))
browser.get('https://python.org')
```

### 15.异常处理

```
from selenium import webdriver
browser=webdriver.Chrome()
browser.get('https://www.baidu.com')
browser.find_element_by_id('hello')
```

```
from selenium import webdriver
from selenium.common.exceptions import TimeoutException,NoSuchElementException
browser=webdriver.Chrome()
try:
  browser.get('https://www.baidu.com')
except:
  print('TIME OUT')
try:
  browser.find_element_by_id('hello')
except NoSuchElementException:
  print('No Element')
finally:
  browser.close()
```

输出：`>>>No Element`

