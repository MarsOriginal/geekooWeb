# 爬虫

# Urllib

|名称|用途|
|:----|:----|
|Request |发起请求|
|Error   |当Request用错时，进行异常处理|
|Parse   |解析URL地址|
|Robotparser|解析网站的robot.txt|

## Request

首先我们先从使用率最多的**Request库**，它的主要用途便是发起请求，利用Python取代浏览器的访问对服务器发起请求。

通常在使用浏览器查阅网站源代码时，我们需要在浏览器的地址栏输入网站的地址，而要查看其的源代码还需要按**F12**进行查阅。

但对于Python的Urllib库而言，便只需要几行代码就可以完成：

```python
//导入urllib库的request模块
import urlib.request

//利用request模块打开目标网站
r = urllib.request.urlopen('http://www.geekoo.org')

//以utf-8读取网站源代码
print(r.read().decode('utf-8'))
```

这里面的**urlopen函数**非常重要，在一般情况下仅靠一个url便可以进行爬取，而urlopen函数提供了三个parameters：

```python
urllib.request.urlopen(url, data=None, [timeout, ]*)
```

- ***url***：目标网站的链接
- ***data***：为post请求提供封装后的参数，
- ***timeout***：最长请求时间，超时将不再请求

但有时我们需要隐瞒服务器，让服务器认为我们是浏览器或移动端，那**request header**就非常重要了。

urilib库中提供了Request函数，具体的参数如下：

```python
urllib.request.Request(url, data=None, headers={}, method=None)
```

其中添加了可自定义的header信息，操作如下：

- url与header的定义

```python
from urllib import request,parse
import ssl

url = 'https://ddrk.me/ddrklogin/'
headers = {
    #假装自己是浏览器
    'User-Agent':' Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36',
}
```

- 请求参数

```python
dict = {
    'return_url':'https://ddrk.me/ddrklogin/',
    'user_name':'mars16x@gmail.com',
    'password':'---------',
    '_post_type':'ajax',
}
```

- 后续操作

```python
data = bytes(parse.urlencode(dict),'utf-8')
req = request.Request(url,data=data,headers=headers,method='POST')
response = request.urlopen(req,context=context)
print(response.read().decode('utf-8'))
```