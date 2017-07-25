---
layout: post
title:  "Python爬虫之利用正则表达式抓取猫眼top100电影"
date:   2017-07-25 12:00:00
categories: Python
tags:  正则表达式
author: Humy
---
* content
{:toc}

>本篇文章主要介绍的是利用正则表达式抓取猫眼top100电影，源程序放出，仅供大家参考学习
(ps:这是Python静觅录的视频上的代码)




```py
import json
import re
import requests
from multiprocessing import Pool
from requests.exceptions import RequestException


def get_one_page(url):
    try:
        response=requests.get(url)
        if response.status_code==200:
            return response.text
        else:
            return None
    except RequestException:
        print("出错了")

def parse_one_page(html):
    pattern=re.compile('<dd>.*?board-index.*?>(\d+)</i>.*?data-src="(.*?)".*?name"><a.*?>(.*?)</a>.*?star">(.*?)</p>.*?releasetime">(.*?)</p>.*?integer">(.*?)</i>.*?fraction">(.*?)</i>.*?</dd>',re.S)
    items=re.findall(pattern, html)
    for item in items:#将解析的数据转换为字典格式
        yield{
            'index':item[0],
            'image':item[1],
            'title':item[2],
            'actor':item[3].strip()[3:],
            'time':item[4].strip()[5:],
            'score':item[5]+item[6]
        }
def write_to_file(item):
    with open('movies.txt','a',encoding='utf-8') as f:
        f.write(json.dumps(item,ensure_ascii=False)+'\n')#将字典格式转换为字符串
def main(offset):
    url="http://maoyan.com/board/4?offset="+str(offset)
    html=get_one_page(url)
    items=parse_one_page(html)
    for item in items:
        print(item)
        write_to_file(item)

if __name__=='__main__':
    #for i in range(10):
        #main(i*10)
    pool=Pool()#进程池
    pool.map(main,[i*10 for i in range(10)])
 
```
