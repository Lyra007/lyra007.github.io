---
layout: learn
title: 写一个简单的爬虫
date: 2017-11-01 14:24:29 +0800
categories: learning
tags: python
keywords: crawler
---

#写一个简单的爬虫

今天有尝试写了一个简单的爬虫 代码如下。
{% highlight python linenos %}
#使用以下两个modules     
import urllib.request
import re

#用于获取html的内容
def get_html(page_url):
    resp = urllib.request.urlopen(page_url)
    html = resp.read()
    return html

url = 'http://www.hi1718.com'
html = get_html(url)
#python3.5需要用decode 不然会报错
html = html.decode('utf-8')
#正则表达式最难 而且不太会
reg1 = '<span><a .*?_blank">(.*?)</a></span>'
cate = re.compile(reg1)
cat_list1 = re.findall(cate, html)
print(cat_list1)
    
{% endhighlight %}

返回结果如下 是一个数组
<mark>
['色谱分析仪', '光谱分析仪', '质谱', '电化学分析仪器', '元素分析仪', '水分测定仪', '样品处理设备', '其他分析仪器', '恒温/加热/干燥设备', '天平衡器', '离心机', '纯化设备']
</mark>

