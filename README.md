# 爬虫的简单使用

* [爬虫的简介](#爬虫的简介)
* [URL管理器](#URL管理器)
* [网页下载器](#网页下载器)
* [网页解析器](#网页解析器)

## 爬虫的简介
爬虫：一段自动抓取互联网信息的程序  
爬虫模块：URL管理器，网页下载器，网页解析器  

## URL管理器
URL管理器：管理待抓取URL集合和已抓取URL集合
作用：防止重复抓取，防止循环抓取  
1. 添加新URL到待爬取集合中
2. 判断待添加URL是否在容器中
3. 获取待爬取URL
4. 判断是否还有待爬取的URL
5. 将URL从待爬取移动到已爬取

实现方式：
1. 内存
2. 关系数据库
3. 缓存数据库

## 网页下载器
网页下载器：将互联网上URL对应的网页下载到本地的工具
下载器类型：
1. urllib2  Python官方基础模块
2. requests 第三方插件
urllib2下载网页方法：
1. urllib2.urlopen(url)
2. 添加data，http header
3. 添加特殊情景的处理器，例如HTTPCookieProcessor ProxyHandler HTTPSHandler HTTPRedirectHandler
```
import urllib2

# 直接请求
response = urllib2.urlopen('http://www.baidu.com')

# 获取状态码，如果是200表示获取成功
print response.getcode()

# 读取内容
cont = response.read()
```
```
import urllib2

# 创建Request对象
request = urllib2.Request(url)

# 添加数据
request.add_data('a', '1')
# 添加http的header
request.add_header('User-Agent', 'Mozilla/5.0')

# 发送请求获取结果
response = urllib2.urlopen(request)
```
```
import urllib2, cookielib

# 创建cookie容器
cj = cookielib.CookieJar()

# 创建1个opener
opener = urllib2.build_opener(urllib2.HTTPCookieProcessor(cj))

# 给urllib2安装opener
urllib2.install_opener(opener)

# 使用带有cookie的urllib2访问网页
response = urllib2.urlopen('http://www.baidu.com')
```

## 网页解析器
网页解析器：从网页中提取有价值的数据的工具
1. 正则表达式 模糊匹配
2. html.parser 结构化解析
3. Beautiful Soup 结构化解析
4. lxml 结构化解析
结构化解析-DOM（Document Object Model）树