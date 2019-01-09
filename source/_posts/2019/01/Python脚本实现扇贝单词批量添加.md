---
title: Python脚本实现扇贝单词批量添加
date: 2019-01-06 13:08:39
tags: [脚本]
---


- - -
<!--more-->
Python脚本实现扇贝单词批量添加
---


# 获取单词&正则匹配

[获取单词](https://pan.baidu.com/s/1UDk57UdYbmGpyaR1NzdYgA)

```python
import re
# 单词写入文件
file = open("./EngWords.txt", 'w') 
lines = None
wordscount = 0
# 正则匹配 `［`之前的单词
compiled_pattern = re.compile((r'\w+(?=［)'))
with open('./四级词汇词根+联想记忆法-俞敏洪.txt') as f:
    lines = f.readlines()
for line in lines:
    #sub = re.search(r'\w+(?=［)', line)
    sub = compiled_pattern.search(line)
    if sub is not None:
        wordscount +=1
        file.write(sub.group(0) + '\n')
file.close() 
print(wordscount)
```
# 批量上传单词

```python
# 批量上传函数
def uploadWords(words):
    # words = "status%0Asteady%0Ainclude%0Aresistance%0Aprime%0Aambassador"
    words = words[:-2]
    url = "https://www.shanbay.com/bdc/vocabulary/add/batch/?words="
    url = url + words + '&_=15467'
    #querystring = {"words": words}
    headers = {
        'cookie': "183787513; csrftoken=NbOu8iDgk7CSU5erpzJ80wdKoD3eBgF2; _ga=GA1.2.2039615932.1546739762; language_code=zh-CN; locale=zh-cn; sessionid=e30%3A1gfxi6%3A6",
        }
    
    response = requests.request("GET", url, headers=headers, params=querystring)
    if response.ok is not True:
        print("添加错误")
    return response

# 读取单词并上传
with open('./EngWords.txt') as f:
   lines = f.readlines()
words= ""
wordscount = 0
requestcount = 0
for line in lines:
    words += line + '%0'
    wordscount +=1
    if wordscount == 10:
        uploadWords(words)
        time.sleep(0.5)
        words = ""
        wordscount = 0
        requestcount +=1
```


# 参考
1.[正则表达式操作](https://docs.python.org/zh-cn/3.7/library/re.html#match-objects)