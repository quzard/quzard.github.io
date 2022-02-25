+++
title = "Python使用xpath爬取数据返回空列表解决方案"
date = "2019-03-28T13:27:29+08:00"
toc = true
tags = ["xpath"]
categories = ["爬虫"]
description = ""
+++


最近学了下xpath定位来爬虫

刚刚试了下学校的srtp网站，发现爬取的数据返回是空列表

<!--more-->





![](1.png)

直接获得的xpath是

//*[@id="table1"]/tbody/tr[16]/td[7]

通过查询资料获得，**是tbody问题造成的。浏览器会对html文本进行一定的规范化，所以会自动在路径中加入tbody，导致读取失败，在此处直接在路径中去除tbody即可。**

也就是

//*[@id="table1"]/tr[16]/td[7]

即可

源码

```python
# coding: utf-8
__author__ = "2019/3/27 22:02"
__time__ = "Quzard"
import requests
from lxml import etree


headers = {'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/72.0.3626.121 Safari/537.36'
                         'AppleWebKit/537.36 (KHTML, like Gecko)'
                         ' Chrome/63.0.3239.84 Safari/537.36',
           'Referer': 'http://www.baidu.com',
           'Connection': 'keep-alive'}
url = "http://10.1.30.98:8080/srtp2/USerPages/SRTP/Report3.aspx?Code=04016613"

data = requests.get(url, headers=headers)
data = data.text
s = etree.HTML(data)
print(s.xpath("//*[@id='table1']/tr[last()-1]/td[last()]/text()")[0])
```

