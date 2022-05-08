---
title: Scrapy爬虫框架
date: 2022-05-08 17:23:24
tags:
 - python爬虫
---

# 爬虫Scrapy框架课件说明

![img](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/zhishitu.png)



# Scrapy的概念和流程

## 一、为什么学习Scrapy？

1. Scrapy不能解决的10%的剩余爬行虫需求
2. 让开发过程方便、快速
3. Scrapy框架能够让我们的爬虫效率更高

## 二、什么是scrapy？

文档地址：

V2.3中文版：https://www.osgeo.cn/scrapy/intro/install.html

V最新版（中文）：https://docs.scrapy.org/en/latest/index.html

Scrapy 使用了Twisted['twɪstɪd]异步网络框架，可以魔梯的下载速度。

**Scrapy是一个为了爬取数据，提取性结构数据而编写的框架**，我们只需最快速的应用程序代码，就能够获取。

### 1. Scrapy框架的作用

少量的代码，就能够快速的抓取

### 2. 异步和非阻尼的区别

前面说Twisted是一个我们比较喜欢的框架，我们也经常听到一个非网络名词定义呢，他们有什么区别？

![图像](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/%E5%90%8C%E6%AD%A5%E5%92%8C%E5%BC%82%E6%AD%A5.png)

**异步**：调用在发出，这个调用就，不管有无结果；直接返回是过程之后。

**非违约**：违约是程序在等待请求的结果消息（返回值）时的，在不能得到之前，该调用不会出现当前的违约结果。

## 三、Scrapy的工作流程

### 1. 回顾之前的爬虫流程

![img](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/1.3.1.%E7%88%AC%E8%99%AB%E6%B5%81%E7%A8%8B-1.png)

### 2 你的流程可以改写为

![img](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/1.3.2.%E7%88%AC%E8%99%AB%E6%B5%81%E7%A8%8B-2.png)

### 3. Scrapy的流程

![img](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/1.3.3.scrapy%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%A8%8B.png)

#### 其流程可以描述为：

1. 爬虫对象的请求--url构造请求--> 爬虫对象--> 引擎-- 调度器
2. 调度器把请求-->引擎-->下载中间件--->下载器
3. 下载器发送，获取响应请求---->下载中间件---->引擎--->爬虫中间件--->爬虫
4. 爬虫提取url地址，组装成request对象---->爬虫中间件--->引擎--->调度器，重复步骤2
5. 爬虫提取数据--->引擎--->管道处理和保存数据

#### 注意：

- 图中中文是为了方便理解后加上去的
- 图中绿色线条表示数据的传递
- 注意图中中间件的位置，决定了其作用
- 注意其中引擎的位置，所有的模块之前相互独立，只和引擎进行交互

### 4. Scrapy的三个内置对象

- request请求对象：由url method post_data headers等构成
- response响应对象：由url body status headers等构成
- item数据对象：本质是个字典

### 5. Scrapy中每个模块的具体作用

![img](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/1.3.4.scrapy%E7%BB%84%E4%BB%B6.png)

##### 注意：

- 爬虫中间件和下载中间件只是运行逻辑的位置不同，作用是重复的：如替换UA等

## 四、总结

1. Scrapy的概念：Scrapy是一个为了爬取网站数据，提取结构性数据而编写的应用框架

2. Scrapy框架的运行流程以及数据传递过程：

   1. 爬虫中起始的url构造成request对象-->爬虫中间件-->引擎-->调度器
   2. 调度器把request-->引擎-->下载中间件--->下载器
   3. 下载器发送请求，获取response响应---->下载中间件---->引擎--->爬虫中间件--->爬虫
   4. 爬虫提取url地址，组装成request对象---->爬虫中间件--->引擎--->调度器，重复步骤2
   5. 爬虫提取数据--->引擎--->管道处理和保存数据

3. Scrapy框架的作用：通过少量代码实现快速抓取

4. 掌握Scrapy中每个模块的作用：

   引擎(engine)：负责数据和信号在不同模块间的传递

   调度器(scheduler)：实现一个队列，存放引擎发过来的request请求对象

   下载器(downloader)：发送引擎发过来的request请求，获取响应，并将响应交给引擎

   爬虫(spider)：处理引擎发过来的response，提取数据，提取url，并交给引擎

   管道(pipeline)：处理引擎传递过来的数据，比如存储

   下载中间件(downloader middleware)：可以自定义的下载扩展，比如设置代理ip

   爬虫中间件（spider middleware）：可以自定义请求请求和进行响应过滤，与下载中间件作用重复



# Scrapy的安装

## 一、安装Scrapy

安装命令：

```
pip install scrapy -i https://pypi.tuna.tsinghua.edu.cn/simple复制错误复制成功...
```

效果

![image-20201129184933459](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129184933459.png)

## 二、测试安装是否成功

在终端中输入`scrapy`，如果能看到如下效果，说明安装成功

![image-20201129185220812](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129185220812.png)



# Scrapy的入门使用

下面以爬取百度首页为例，讲解我们如果快速创建第1个Scrapy项目

## 一、创建Scrapy项目结构

### 创建 Scrapy 项目的命令示例

创建scrapy项目的命令

```python
scrapy startproject 项目名字复制错误复制成功...
```

译文：

```
scrapy startproject myspider复制错误复制成功...
```

### 创建第1个项目

打开终端，进入`035-Scrapy框架`你可以改为自己的文件夹到()

![image-20201129185650440](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129185650440.png)

此时文件夹是空的，变成效果

![image-20201129185629466](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129185629466.png)

输入如下命令，创建 Scrapy 项目

```
scrapy startproject myspider复制错误复制成功...
```

效果如下

![image-20201129185825429](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129185825429.png)

查看当前目录，发现有很多文件，如下图所示

![image-20201129185942239](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129185942239.png)

## 二、创建爬虫

创建爬虫的命令如下：

```
scrapy genspider 爬虫名 允许爬取的域名复制错误复制成功...
```

例如

```
scrapy genspider baidu baidu.com复制错误复制成功...
```

![image-20201129190228712](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129190228712.png)

效果如下：

![image-20201129190403029](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129190403029.png)

打开`baidu.py`，发现它的默认代码如下：

![image-20201129190529126](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129190529126.png)

## 三、运行爬虫

运行爬虫命令：在项目目录下执行`scrapy crawl 爬虫名字`

终端中输入命令：

```
scrapy crawl baidu复制错误复制成功...
```

效果如下：

![image-20201129191154070](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129191154070.png)

注意：

> 这个并没有对采集到的数据进行任何操作，如何提取数据等后续讲解
>
> 本案例就是让大家对scrapy的使用大体了解认识

## 小结

1. 用crapy来爬虫，命令我们通过实现这个目标的那样创建一个`.py`然后在中`import`导入，改变`scrapy`命令来创建相关的目录结构，最终来开启scrapy
2. ，Scrapy使用的流程如下：
   1. 创建Scrapy项目，命令是`scrapy startproject 项目名称`
   2. 进入到创建出来的Scrapy项目文件夹
   3. 创建爬虫，命令是`scrapy genspider 爬虫名 允许爬取的域名`
   4. 运行Scrapy，命令是`scrapy crawl 爬虫名`



# Scrapy的使用流程

想要使用 Scrapy 来实现爬虫项目，需要遵循以下流程

1. 创建一个Scrapy项目：`scrapy startproject mySpider`
2. 进入到刚刚创建的mySpider文件夹：`cd mySpider`
3. 生成一个爬虫：`scrapy genspider baidu baidu.com`
4. 提取数据：完善蜘蛛，使用xpath等方法
5. 保存数据：管道中保存数据

### 提示

![image-20190722132332684](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20190722132332684.png)



# 提取爬到的数据

## 一、明确目标

我们爬取蜻蜓排行榜FM以示例数据进行学习如何使用Scrapy

![image-20201129211724376](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129211724376.png)

## 二、创建Scrapy项目

创建项目的命令：

```
scrapy startproject fm复制错误复制成功...
```

效果如下：

![image-20201129211949270](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129211949270.png)

## 三、创建爬虫

创建爬虫命令：

```
scrapy genspider qingting qingting.fm复制错误复制成功...
```

效果如下：

![image-20201129212236830](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129212236830.png)

创建好的爬虫代码如下：

![image-20201129212328484](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129212328484.png)

## 四、抽取数据

### 1.具体在哪里进行提取数据

我们为了能够对获取到的数据进行操作，需要在`parse`函数中对数据的提取等操作

为了进行下一步对`parse`函数的编辑，给添加了一些注释，详细如下图所示

![image-20201129212700966](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129212700966.png)

在`parse`函数中，添加如下代码

![image-20201129213148543](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129213148543.png)

我们通过命令运行爬虫`scrapy crawl qingting`，展示产品

![image-20201129213129501](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129213129501.png)

通过上面的结果能够说明，`parese`函数已经被调用了，也执行了我们的`print`代码

### 2. parse函数中到底该做什么？

通过上图，`parse`函数是scrapy运行时，自动调用的，并且从默认生成的`parse`函数的参数名是可以正常被调用的函数`response`，`parese`对函数应该是scrapy`start_urls`的URL获取之后，携带者http请求调用的

我们只需要在`parse`作业中使用之前学习所以过的抽取数据的抽取数据的方式，比如正则表达式、Xpath等

### 3. response响应对象的常用属性

为了下一步在`parse`函数中进行操作，对下面列出的常用响应属性进行操作

- response.url：当前响应的url地址
- response.request.url：当前地址响应的请求的url
- response.headers：响应头
- response.request.headers：当前响应的请求头
- response.body：响应体，也就是html代码，字节类型
- response.status：响应状态码

关于response的详细说明，请参考：https://www.osgeo.cn/scrapy/topics/request-response.html#scrapy.http.Response

```python
import scrapy


class QingtingSpider(scrapy.Spider):
    name = 'qingting'  # 爬虫的名字
    allowed_domains = ['qingting.fm']  # 允许的域名
    start_urls = ['https://m.qingting.fm/rank/']  # 开始爬取的URL

    def parse(self, response):
        """对start_urls中的URL爬取之后，回调的函数"""
        print("----->", response)
        print("---1-->", response.url)
        print("---2-->", response.headers)
        print("---3-->", response.status)
        print("---4-->", response.body)
        print("---5-->", response.request.url)
        print("---6-->", response.request.headers)
复制错误复制成功...
```

运行脚本取命令`scrapy crawl qingting`之后的效果如下：

![image-20201129214528748](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129214528748.png)

### 3. 抽取蜻蜓FM中的数据

```python
import scrapy


class QingtingSpider(scrapy.Spider):
    name = 'qingting'  # 爬虫的名字
    allowed_domains = ['qingting.fm']  # 允许的域名
    start_urls = ['https://m.qingting.fm/rank/']  # 开始爬取的URL

    def parse(self, response):
        """对start_urls中的URL爬取之后，回调的函数"""
        # print("----->", response)
        # print("---1-->", response.url)
        # print("---2-->", response.headers)
        # print("---3-->", response.status)
        # print("---4-->", response.body)
        # print("---5-->", response.request.url)
        # print("---6-->", response.request.headers)

        # 提取30个需要的a标签对象
        a_list = response.xpath("//div[@class='rank-list']//a")
        print(type(a_list))  # <class 'scrapy.selector.unified.SelectorList'>

        # 遍历取到的数据，对每个单独提取需要的数据
        for a_temp in a_list:
            rank_number = a_temp.xpath("./div[@class='badge']//text()")  # 排名
            img_url = a_temp.xpath("./img/@src")  # 图片地址
            title = a_temp.xpath("./div[@class='content']/div[@class='title']/text()")  # 标题
            desc = a_temp.xpath("./div[@class='content']/div[@class='desc']/text()")  # 描述
            play_number = a_temp.xpath(".//div[@class='info-item'][1]/span/text()")  # 播放量
            print("--**-->", rank_number, img_url, title, desc, play_number)
复制错误复制成功...
```

运行效果：

![image-20201129215657446](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129215657446.png)

### 4. 注意

解析并获取`Scrapy`爬虫中的数据：使用`xpath`规则字符串进行定位和提取

1. `response.xpath`返回结果的方法是一个类似列表的类型，其中包含选择器对象，操作和列表一样，但是还有一些其他的方法
2. 其他方法`extract()`：返回一个包含有字符串的列表
3. 其他方法`extract_first()`：返回列表中的第一个字符串，列表为空没有返回None

使用`extract`方法的代码

```python
import scrapy


class QingtingSpider(scrapy.Spider):
    name = 'qingting'  # 爬虫的名字
    allowed_domains = ['qingting.fm']  # 允许的域名
    start_urls = ['https://m.qingting.fm/rank/']  # 开始爬取的URL

    def parse(self, response):
        """对start_urls中的URL爬取之后，回调的函数"""
        # print("----->", response)
        # print("---1-->", response.url)
        # print("---2-->", response.headers)
        # print("---3-->", response.status)
        # print("---4-->", response.body)
        # print("---5-->", response.request.url)
        # print("---6-->", response.request.headers)

        # 提取30个需要的a标签对象
        a_list = response.xpath("//div[@class='rank-list']//a")
        print(type(a_list))  # <class 'scrapy.selector.unified.SelectorList'>

        # 遍历取到的数据，对每个单独提取需要的数据
        for a_temp in a_list:
            rank_number = a_temp.xpath("./div[@class='badge']//text()").extract()  # 排名
            img_url = a_temp.xpath("./img/@src").extract()  # 图片地址
            title = a_temp.xpath("./div[@class='content']/div[@class='title']/text()").extract()  # 标题
            desc = a_temp.xpath("./div[@class='content']/div[@class='desc']/text()").extract()  # 描述
            play_number = a_temp.xpath(".//div[@class='info-item'][1]/span/text()").extract()  # 播放量
            print("--**-->", rank_number, img_url, title, desc, play_number)
复制错误复制成功...
```

效果如下：

![image-20201129220014588](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129220014588.png)

使用`extract_first`方法的代码：

```python
import scrapy


class QingtingSpider(scrapy.Spider):
    name = 'qingting'  # 爬虫的名字
    allowed_domains = ['qingting.fm']  # 允许的域名
    start_urls = ['https://m.qingting.fm/rank/']  # 开始爬取的URL

    def parse(self, response):
        """对start_urls中的URL爬取之后，回调的函数"""
        # print("----->", response)
        # print("---1-->", response.url)
        # print("---2-->", response.headers)
        # print("---3-->", response.status)
        # print("---4-->", response.body)
        # print("---5-->", response.request.url)
        # print("---6-->", response.request.headers)

        # 提取30个需要的a标签对象
        a_list = response.xpath("//div[@class='rank-list']//a")
        print(type(a_list))  # <class 'scrapy.selector.unified.SelectorList'>

        # 遍历取到的数据，对每个单独提取需要的数据
        for a_temp in a_list:
            rank_number = a_temp.xpath("./div[@class='badge']//text()").extract_first()  # 排名
            img_url = a_temp.xpath("./img/@src").extract_first()  # 图片地址
            title = a_temp.xpath("./div[@class='content']/div[@class='title']/text()").extract_first()  # 标题
            desc = a_temp.xpath("./div[@class='content']/div[@class='desc']/text()").extract_first()  # 描述
            play_number = a_temp.xpath(".//div[@class='info-item'][1]/span/text()").extract_first()  # 播放量
            print("--**-->", rank_number, img_url, title, desc, play_number)复制错误复制成功...
```

效果如下：

![image-20201129220150996](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129220150996.png)

## 五、总结

- `parse`函数就是 Scrapy 在 HTTP(s) 响应之后的正确函数
- `parse`函数中的参数将响应数据封装为字典的参数对象，这个对象可以直接使用xpath进行数据采集，在处理非异常数据（一般指html文件）时非常方便



# 管道的基本使用

## 一、目的

使用管道管道的目的：对`parse`功能中提取到的数据进一步处理的操作，例如保存到 csv、MongoDB 等

## 二、解析函数中返回数据

修改爬虫文件`qingting.py`中`parse()`功能

```python
import scrapy


class QingtingSpider(scrapy.Spider):
    name = 'qingting'  # 爬虫的名字
    allowed_domains = ['qingting.fm']  # 允许的域名
    start_urls = ['https://m.qingting.fm/rank/']  # 开始爬取的URL

    def parse(self, response):
        """对start_urls中的URL爬取之后，回调的函数"""
        # print("----->", response)
        # print("---1-->", response.url)
        # print("---2-->", response.headers)
        # print("---3-->", response.status)
        # print("---4-->", response.body)
        # print("---5-->", response.request.url)
        # print("---6-->", response.request.headers)

        # 提取30个需要的a标签对象
        a_list = response.xpath("//div[@class='rank-list']//a")
        print(type(a_list))  # <class 'scrapy.selector.unified.SelectorList'>

        # 遍历取到的数据，对每个单独提取需要的数据
        for a_temp in a_list:
            rank_number = a_temp.xpath("./div[@class='badge']//text()").extract_first()  # 排名
            img_url = a_temp.xpath("./img/@src").extract_first()  # 图片地址
            title = a_temp.xpath("./div[@class='content']/div[@class='title']/text()").extract_first()  # 标题
            desc = a_temp.xpath("./div[@class='content']/div[@class='desc']/text()").extract_first()  # 描述
            play_number = a_temp.xpath(".//div[@class='info-item'][1]/span/text()").extract_first()  # 播放量
            print("--**-->", rank_number, img_url, title, desc, play_number)

            # ----- 修改的代码---开始----
            temp_dict = {
                "rank_number": rank_number,
                "img_url": img_url,
                "title": title,
                "desc": desc,
                "play_number": play_number
            }
            yield temp_dict
            # ----- 修改的代码---结束----
复制错误复制成功...
```

##### [思考：为什么要使用产量？](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/06?id=思考：为什么要使用yield？)

让整个函数变成一个生成器

- 在遇到这个函数的返回值的时候，不会造成内存的数据瞬间占用过高，python3中的range和python2中的xrange同理
- Scrapy是能够异步爬取，所以通过`yield`将运行权限教给其他的协程任务去执行，这样整个程序的运行效果会更高

{% em color="#33CCCC" %}**注意：解析函数中的yield传递的对象只能是：BaseItem, Request, dict, None** {% endem %}

## 三、修改管道处理功能

### 1.修改pipelines.py文件

情况下此文件的性质如下：

![图像-20201129222029755](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129222029755.png)

修改为代码：

```python
class FmPipeline:
    def process_item(self, item, spider):
        # 爬虫文件中提取数据的方法每yield一次item，就会运行一次
        # 该方法为固定名称函数
        print("-----我是管道，接收到了数据--->", item, "----数据属于爬虫:--->", spider)
        return item复制错误复制成功...
```

### 2.在settings.py设置开启管道

情况如下：

![image-20201129222338020](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129222338020.png)

修改为代码：

```python
ITEM_PIPELINES = {
   'fm.pipelines.FmPipeline': 300,
}复制错误复制成功...
```

重新运行命令：

```
scrapy crawl qingting复制错误复制成功...
```

运行效果：

![image-20201129222457325](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201129222457325.png)

## 四、总结

- 如果提取想要的数据，我们应该在`parse`函数中
- 如果想要对提取的数据进行进一步处理，我们应该在`process_item`函数中
- `parse`函数中的数据是怎样传递到`process_item`函数中的呢？是通过`yield`返回给Scrapy内核代码，调用`process_item`时传递过去的
- 所有的数据都提取完成之后再使用将都给 Scrapy 内核数据，一次调用，只要函数中调用了之后，Scrapy 内核代码就可以马上调用`process_item`呢？的功能（单处理的多任务）减少内存占用`parse``yield``process_item`



![image-20201130090540613](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201130090540613.png)

上图的1~12序号，解释说明如下：

1. Scrapy 从蜘蛛子类中提取start_urls，然后构造为请求对象

   

2. 将请求对象传递给爬虫件

3. 将请求对象传递给Scrapy（就是内核）

4. 将请求对象提交给调度器（它负责对多个请求安排，好比交通管理员负责交通的指挥）

5. 将请求的请求引擎传递给Scrapy

6. Scrapy将请求请求对象传递给下载中间件（可以更换代理IP，更换Cookies，更换User-Agent，自动重试。等）

7. 请求请求对象传给它的下载器通过其他方式发送给对象HTTP（）请求），得到响应（响应为响应对象）

8. 将回复对象传递给下载件

9. 下载件将响应对象传递给Scrapy引擎

10. Scrapy引擎将响应对象传递给中间件（这里可以处理异常等情况）

11. 爬虫对象中的解析函数被调用（在这里可以对得到的状态码响应对象进行处理，例如用状态响应处理，xpath可以进行提取数据）

    

12. 将提取到的数据传递给Scrapy等引擎，数据再传递给管道（在管道中我们可以将数据存储到csv、MongoDB）



# 多数据的下载

## 一、目标

请求请求中的 URL，切从这样的 URL 也发送请求，然后提取它的数据

## 二、准备

1. 创建蜻蜓FM项目（`scrapy startproject fm`）

2. 进入到`fm`文件夹，创建清廷爬虫（`scrapy genspider qingting qingting.fm`）

3. 编辑`spiders/qingting.py`

   ```python
   import scrapy
   
   
   class QingtingSpider(scrapy.Spider):
       name = 'qingting'  # 爬虫的名字
       allowed_domains = ['qingting.fm']  # 允许的域名
       start_urls = ['https://m.qingting.fm/rank/']  # 开始爬取的URL
   
       def parse(self, response):
           """对start_urls中的URL爬取之后，回调的函数"""
           # 提取30个需要的a标签对象
           a_list = response.xpath("//div[@class='rank-list']//a")
           print(type(a_list))  # <class 'scrapy.selector.unified.SelectorList'>
   
           # 遍历取到的数据，对每个单独提取需要的数据
           for a_temp in a_list:
               rank_number = a_temp.xpath("./div[@class='badge']//text()").extract_first()  # 排名
               img_url = a_temp.xpath("./img/@src").extract_first()  # 图片地址
               title = a_temp.xpath("./div[@class='content']/div[@class='title']/text()").extract_first()  # 标题
               desc = a_temp.xpath("./div[@class='content']/div[@class='desc']/text()").extract_first()  # 描述
               play_number = a_temp.xpath(".//div[@class='info-item'][1]/span/text()").extract_first()  # 播放量
               print("--**-->", rank_number, img_url, title, desc, play_number)
   
               temp_dict = {
                   "rank_number": rank_number,
                   "img_url": img_url,
                   "title": title,
                   "desc": desc,
                   "play_number": play_number
               }
               yield temp_dict
   复制错误复制成功...
   ```

## 三、在解析中生成新的请求请求对象

如果在提取某个 URL 时想对它返回的数据中的数据，提取到新的 URL 继续提取，函数中`yield`的新`scrapy.Request`对象来实现

关于Request类的具体说明，请参考：[https ://www.osgeo.cn/scrapy/topics/request-response.html](https://www.osgeo.cn/scrapy/topics/request-response.html)

```python
import scrapy


class QingtingSpider(scrapy.Spider):
    name = 'qingting'  # 爬虫的名字
    allowed_domains = ['qingting.fm']  # 允许的域名
    start_urls = ['https://m.qingting.fm/rank/']  # 开始爬取的URL

    def parse(self, response):
        """对start_urls中的URL爬取之后，回调的函数"""
        # 提取30个需要的a标签对象
        a_list = response.xpath("//div[@class='rank-list']//a")
        print(type(a_list))  # <class 'scrapy.selector.unified.SelectorList'>

        # 遍历取到的数据，对每个单独提取需要的数据
        for a_temp in a_list:
            rank_number = a_temp.xpath("./div[@class='badge']//text()").extract_first()  # 排名
            img_url = a_temp.xpath("./img/@src").extract_first()  # 图片地址
            title = a_temp.xpath("./div[@class='content']/div[@class='title']/text()").extract_first()  # 标题
            desc = a_temp.xpath("./div[@class='content']/div[@class='desc']/text()").extract_first()  # 描述
            play_number = a_temp.xpath(".//div[@class='info-item'][1]/span/text()").extract_first()  # 播放量
            print("--**-->", rank_number, img_url, title, desc, play_number)

            temp_dict = {
                "rank_number": rank_number,
                "img_url": img_url,
                "title": title,
                "desc": desc,
                "play_number": play_number
            }
            yield temp_dict

            # ------ 新代码------开始-------
            # 生成新的request请求对象
            yield scrapy.Request(url=img_url, callback=self.parse_img)
            # ------ 新代码------结束-------

    # ------ 新代码------开始-------
    def parse_img(self, response):
        print("-----parse_img函数-1-->", response)
        print("-----parse_img函数-2-->", response.url)
        # print("-----parse_img函数-3-->", response.body)
    # ------ 新代码------结束-------
复制错误复制成功...
```

运行效果：

![image-20201130101819921](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201130101819921.png)

## [四、保存图片](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/08?id=四、保存img图片)

想要在fmScrapy中存储中，我们需要在自定义的`parse_img`函数中，`yield`生成一个管道中的图片，在管道中进行数据采集，然后在管道中进行爬虫，然后

### [1.`parse_img`函数中`yield`图片](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/08?id=_1-parse_img函数中yield图片)

```python
import scrapy


class QingtingSpider(scrapy.Spider):
    name = 'qingting'  # 爬虫的名字
    allowed_domains = ['qingting.fm']  # 允许的域名
    start_urls = ['https://m.qingting.fm/rank/']  # 开始爬取的URL

    def parse(self, response):
        """对start_urls中的URL爬取之后，回调的函数"""
        # 提取30个需要的a标签对象
        a_list = response.xpath("//div[@class='rank-list']//a")
        print(type(a_list))  # <class 'scrapy.selector.unified.SelectorList'>

        # 遍历取到的数据，对每个单独提取需要的数据
        for a_temp in a_list:
            rank_number = a_temp.xpath("./div[@class='badge']//text()").extract_first()  # 排名
            img_url = a_temp.xpath("./img/@src").extract_first()  # 图片地址
            title = a_temp.xpath("./div[@class='content']/div[@class='title']/text()").extract_first()  # 标题
            desc = a_temp.xpath("./div[@class='content']/div[@class='desc']/text()").extract_first()  # 描述
            play_number = a_temp.xpath(".//div[@class='info-item'][1]/span/text()").extract_first()  # 播放量
            print("--**-->", rank_number, img_url, title, desc, play_number)

            temp_dict = {
                "rank_number": rank_number,
                "img_url": img_url,
                "title": title,
                "desc": desc,
                "play_number": play_number
            }
            yield temp_dict

            # 生成新的request请求对象
            yield scrapy.Request(url=img_url, callback=self.parse_img, cb_kwargs={"img_name": title})

    def parse_img(self, response, img_name):
        print("-----parse_img函数-1-->", response)
        print("-----parse_img函数-2-->", response.url)
        # print("-----parse_img函数-3-->", response.body)
        print("-----parse_img函数-4-->", img_name)  # 这是在parse函数中创建Request请求时设定的给新URL回调函数的参数
        yield {
            "img_name": img_name + ".png",
            "img_byte": response.body
        }
复制错误复制成功...
```

### [2. 管道中保存图片](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/08?id=_2-管道中保存图片)

```python
from itemadapter import ItemAdapter


class FmPipeline:
    def process_item(self, item, spider):
        # 将图片保存
        img_name = item.get("img_name")
        img_byte = item.get("img_byte")
        if img_name:
            with open(img_name, "wb") as f:
                f.write(img_byte)
                print("保存图片%s完成....ok" % img_name)
复制错误复制成功...
```

### [3. 开启管道](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/08?id=_3-开启管道)

![image-20201130103811524](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201130103811524.png)

### [4. 设置日志的最低等级](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/08?id=_4-设置日志的最低级别)

就可以在终端中不用看这样的信息，只看重要的信息

![image-20201130103846938](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201130103846938.png)

### [5. 运行测试](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/08?id=_5-运行测试)

运行效果如下：

![image-20201130104307629](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201130104307629.png)

## [五、保存图片的同时保存信息](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/08?id=五、保存图片的同时也保存信息)

在`process_item`函数中，我们可以将图片保存到文件中，那么如果既想保存图片，又想保存在`parse`函数中提取的信息改怎么办呢？

问：在`process_item`函数中，判断数据是图片还是信息，如果是图片就保存到文件，是信息就保存到csv文件（当然保存到数据库也是可以的）

修改`pipeline.py`为代码：

```python
# Define your item pipelines here
#
# Don't forget to add your pipeline to the ITEM_PIPELINES setting
# See: https://docs.scrapy.org/en/latest/topics/item-pipeline.html


# useful for handling different item types with a single interface
import csv
import os

from itemadapter import ItemAdapter


class FmPipeline:
    def process_item(self, item, spider):
        # 判断是否存在download文件夹，如果没有则创建
        download_path = os.getcwd() + '/download/'  # 当前文件夹下的download文件夹
        if not os.path.exists(download_path):  # 判断文件夹或文件
            os.makedirs(download_path)

        # 将图片保存
        img_name = item.get("img_name")
        img_byte = item.get("img_byte")
        if img_name:
            with open(download_path + img_name, "wb") as f:
                f.write(img_byte)
                print("保存图片%s完成....ok" % img_name)
            return

        title = item.get("title")
        rank_number = item.get("rank_number")
        img_url = item.get("img_url")
        desc = item.get("desc")
        play_number = item.get("play_number")
        if title:
            # 如果是信息，就保存到csv文件
            with open(download_path + '蜻蜓FM.csv', 'a') as f:
                # 创建一个csv的DictWriter对象，这样才能够将写入csv格式数据到这个文件
                f_csv = csv.DictWriter(f, ['title', 'rank_number', 'img_url', 'desc', 'play_number'])
                # 写入多行行（当做数据）
                f_csv.writerows([item])
                print("保存信息到CSV....ok")复制错误复制成功...
```

的运行效果：

![image-20201130110010757](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201130110010757.png)

## [六、总结](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/08?id=六、总结)

案例到底说明了什么呢？本请大家思考5分钟，再继续

![image-20201130110446842](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201130110446842.png)

到现在为止，我们通过Scrapy实现获取数据，学习了2种方式

1. 可以爬取存储数据，如上图蓝色序号1、2、3、4、5
2. 可以重复提取数据存储数据，如上图所示的数字1、2、3、3重复执行次数，当某次想要存储数据就在其功能`parse`中的`yield`数据可以顺序



# [案例：豆瓣电影TOP250](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/09?id=案例：豆瓣电影top250)

## [一、要求](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/09?id=一、要求)

练习Scrapy框架，能够取豆瓣爬到中，通过Scrapy250个电影、Top250等电影的详细评论（包括标题评分、数据库图片）

网址：https://movie.douban.com/top250?start=0&filter=

![image-20201130114311025](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201130114311025.png)

## [二、代码参考地址](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/09?id=二、代码参考地址)

[https://gitee.com/dong4716138/Python19/tree/master/035-Scrapy%E6%A1%86%E6%9E%B6/05-%E8%B1%86%E7%93%A3TOP250/douban](https://gitee.com/dong4716138/Python19/tree/master/035-Scrapy框架/05-豆瓣TOP250/douban)

## [三、说明](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/09?id=三、说明)

本案例在`settings.py`中配置的信息有

- `ROBOTSTXT_OBEY = False` 其作用：关闭robots.txt验证

- `LOG_LEVEL = "WARNING"`其作用：更改Scrapy默认的等级日志

- `DOWNLOAD_DELAY = 3`其作用：scrapy爬取同一个域名下的时间间隔，不是固定时间，详情参考：https://www.osgeo.cn/scrapy/topics/settings.html?highlight=download_delay#std-setting-DOWNLOAD_DELAY

- `DOWNLOADER_MIDDLEWARES`其作用：下载中间件，分数越先执行小权重击射击，越过执行

  

# [Scrapy中间件的使用](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/10?id=scrapy中间件的使用)

## [一、Scrapy中间件的分类和作用](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/10?id=一、scrapy中间件的分类和作用)

### [1. Scrapy中间件的分类](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/10?id=_1-scrapy中间件的分类)

根据scrapy运行流程中的位置不同分为：

1. 下载中间件
2. 爬虫中间件

### [2. Scrapy中间件的作用](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/10?id=_2-scrapy中间件的作用)

请求和响应对象

1. 如对非200响应的重试（重新构造请求对象yield给引擎）
2. 也可以对header以及cookie进行更换和处理
3. 使用代理ip等

但在 Scrapy 之间的默认情况下，每个文件都在`middlewares.py`一个文件中

爬虫中间件使用方法和下载中间件相同，且经常使用下载中间件功能重复

## [二、下载中间件的使用方法：](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/10?id=二、下载中间件的使用方法：)

![image-20190723200548953](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20190723200548953.png)

下载器中间件默认的方法：

- ```
  process_request(self, request, spider)
  ```

  ：

  1. 当每个请求通过下载中间件时，该方法被调用
  2. 返回无值：没有返回也无返回值，该请求对象给下载器，或通过引擎传递给其他重权低的过程_请求方法
  3. 返回响应对象：不再请求，把响应返回给引擎
  4. 返回请求对象通过引擎传递委托：请求对象，此时将不会其他重权低的过程请求方法

- ```
  process_response(self, request, response, spider)
  ```

  ：

  1. 当下载器完成http请求，传递响应给引擎的时候调用
  2. 返回响应的处理方式或通过重载的方式处理其他请求的处理方式：其他请求
  3. 返回请求对象：通过引擎调取器继续请求，将不会通过其他重权重的进程_request

- 在`settings.py`中配置开启中间件，**权重值越小越优先执行**

## [三、下载中间件示例（实现随时User-Agent）](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/10?id=三、下载中间件示例（实现随机user-agent）)

### [1.在`middlewares.py`中完善代码](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/10?id=_1-在middlewarespy中完善代码)

```python
import random


class UserAgentMiddleware(object):
    USER_AGENTS_LIST = [
        "Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Win64; x64; Trident/5.0; .NET CLR 3.5.30729; .NET CLR 3.0.30729; .NET CLR 2.0.50727; Media Center PC 6.0)",
        "Mozilla/5.0 (compatible; MSIE 8.0; Windows NT 6.0; Trident/4.0; WOW64; Trident/4.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; .NET CLR 1.0.3705; .NET CLR 1.1.4322)",
        "Mozilla/4.0 (compatible; MSIE 7.0b; Windows NT 5.2; .NET CLR 1.1.4322; .NET CLR 2.0.50727; InfoPath.2; .NET CLR 3.0.04506.30)",
        "Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-CN) AppleWebKit/523.15 (KHTML, like Gecko, Safari/419.3) Arora/0.3 (Change: 287 c9dfb30)",
        "Mozilla/5.0 (X11; U; Linux; en-US) AppleWebKit/527+ (KHTML, like Gecko, Safari/419.3) Arora/0.6",
        "Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.8.1.2pre) Gecko/20070215 K-Ninja/2.1.1",
        "Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-CN; rv:1.9) Gecko/20080705 Firefox/3.0 Kapiko/3.0",
        "Mozilla/5.0 (X11; Linux i686; U;) Gecko/20070322 Kazehakase/0.4.5"
    ]

    def process_request(self, request, spider):
        print("------下载中间件----")
        # 随机挑选一个UA
        user_agent = random.choice(self.USER_AGENTS_LIST)
        request.headers['User-Agent'] = user_agent
        # 不写return
复制错误复制成功...
```

### [2.在`settings.py`中设置开启自定义的下载中间件](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/10?id=_2-在settingspy中设置开启自定义的下载中间件)

```python
DOWNLOADER_MIDDLEWARES = {
    'douban.middlewares.UserAgentMiddleware': 400,  # 400是权重值（值越小越先被执行）
    'douban.middlewares.DoubanDownloaderMiddleware': 543,
}复制错误复制成功...
```

![image-20201130211550790](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201130211550790.png)

## [四、下载中间件示例（使用代理ip）](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/10?id=四、下载中间件示例（使用代理ip）)

### [一、思路分析](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/10?id=_1-思路分析)

1. 代理添加的位置：request.meta中增加`proxy`字段

2. 获取一个代理ip，给予给予

   ```
   request.meta['proxy']
   ```

   - 代理池中随时选择代理ip
   - 代理ip的webapi发送请求获取一个代理ip

### [2.具体实现](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/10?id=_2-具体实现)

#### [免费代理ip：](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/10?id=免费代理ip：)

```python
class ProxyMiddleware(object):
    def process_request(self, request, spider):
        # proxies可以在settings.py中，也可以来源于代理ip的webapi
        # proxy = random.choice(proxies)

        # 免费的会失效，报 111 connection refused 信息！重找一个代理ip再试
        request.meta['proxy'] = 'https://1.71.188.37:3128'
        return None  # 可以不写return复制错误复制成功...
```

#### [收费代理ip：](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/10?id=收费代理ip：)

```python
# 人民币玩家的代码(使用abuyun提供的代理ip)
import base64

# 代理隧道验证信息  这个是在那个网站上申请的
proxyServer = 'http://proxy.abuyun.com:9010' # 收费的代理ip服务器地址，这里是abuyun
proxyUser = 用户名
proxyPass = 密码
proxyAuth = "Basic " + base64.b64encode(proxyUser + ":" + proxyPass)

class ProxyMiddleware(object):
    def process_request(self, request, spider):
        # 设置代理
        request.meta["proxy"] = proxyServer
        # 设置认证
        request.headers["Proxy-Authorization"] = proxyAuth复制错误复制成功...
```

### [3.检测代理ip是否可用](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/10?id=_3-检测代理ip是否可用)

在使用了代理ip的情况下可以在下载中间件的`process_response()`方法中处理代理ip的使用情况，如果该代理ip使用可以替换其他代理ip

```python
class ProxyMiddleware(object):
    ......
    def process_response(self, request, response, spider):
        print("-----下载中间件-reponse----", response.status)
        if response.status != 200:
            request.dont_filter = True  # 重新发送的请求对象能够再次进入队列
            return request
        return response复制错误复制成功...
```



# [在中间使用Selenium、Pyppeteer](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/11?id=在中间件中使用selenium、pyppeteer)

示例如下，可以将get_cookies函数中的代码改为Selenium或者Pyppeteers的代码，然后实现驱动请求浏览器获取cookie，然后将获取到的cookie添加到Request对象中，然后实现阻止反爬

```
python
# -*- coding: utf-8 -*-

# Define here the models for your spider middleware
#
# See documentation in:
# https://docs.scrapy.org/en/latest/topics/spider-middleware.html

import time
from selenium import webdriver


def get_cookies():
    # 使用Selenium模拟登陆，获取并返回cookie
    # 这里还可以是Pyppeteer代码 道理都是相同的，只是代码不同而已
    username = input('输入renren账号:')
    password = input('输入renren密码:')
    options = webdriver.ChromeOptions()
    options.add_argument('--headless')
    options.add_argument('--disable-gpu')
    driver = webdriver.Chrome(chrome_options=options)
    driver.get('http://www.renren.com')
    time.sleep(2)
    driver.find_element_by_xpath("//input[@name='email']").send_keys(username)
    time.sleep(1)
    driver.find_element_by_xpath("//input[@name='password']").send_keys(password)
    time.sleep(1)
    driver.find_element_by_xpath("//input[@id='login']").click()
    time.sleep(2)
    print("selenium get cookie:", driver.get_cookies())
    cookies_dict = {cookie['name']: cookie['value'] for cookie in driver.get_cookies()}
    driver.quit()
    return cookies_dict


class LoginDownloaderMiddleware(object):
    
    def process_request(self, request, spider):
        # 调用Selenium，完成cookie的获取
        cookies_dict = get_cookies()
        print(">>>cookie>>>", cookies_dict)
        request.cookies = cookies_dict  # 对请求对象的cookies属性进行替换
```



# 练习

请把Scrapy爬取如下3个网站数据

## 一、瓜子二手车

提取瓜子二手车的信息

1. 爬取10页
2. 要抽取页的信息（见下图的红框圈中的信息）
3. 使用请求模块 爬取
4. 存储到CSV文件
5. 给对象的方式

![作业1](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/%E4%BD%9C%E4%B8%9A1.png)

## [二、Q房](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/12?id=二、q房)

爬取Q房网的二手房信息

1. 爬取10页
2. 每页需要的内容见下图红框圈中的信息（顶部URL地址栏不算）
3. 使用aiohttp爬取（要发挥异步的威力，即多页一起爬取）
4. 存储到MongoDB数据库
5. 给对象的礼物

![作业2](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/%E4%BD%9C%E4%B8%9A2.png)

## [三、安居客](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/12?id=三、安居客)

### [1. 功能要求](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/12?id=_1-功能要求)

编写代码实现“安居客”网站“沭阳”的属性信息提取，并存储到CSV文件，提取最多为120条

### [2. 提交要求](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/12?id=_2-提交要求)

新建pycharm，并且用git进行管理，将最后写的代码+csv文件都使用git管理后推送到远程项目仓库

且将远程仓库权限改为“公有”，将网址以及自己的姓名添加到文档中

https://shimo.im/sheets/QYcRPPtxQQPrcDPW/MODOC/

### [3.详细描述](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/12?id=_3-详细描述)

安居客网址：https://shuyang.anjuke.com/map/sale/

1.下图可以上加载更多

![Xnip2020-11-05_21-20-11](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/Xnip2020-11-05_21-20-11.png)

2.仔细分析能够找到加载更多的时间的URL，以及响应

![Xnip2020-11-05_21-23-18](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/Xnip2020-11-05_21-23-18.png)

![Xnip2020-11-05_21-22-24](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/Xnip2020-11-05_21-22-24.png)

3.从下载的信息中提取下图标签的数据

![Xnip2020-11-05_21-27-19](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/Xnip2020-11-05_21-27-19.png)

根据上图描述，存储到合适的cvs文件

### [4.最后的效果](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/12?id=_4-最后效果)

![Xnip2020-11-05_21-44-02](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/Xnip2020-11-05_21-44-02.png)



# [管道的使用](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/13?id=管道的使用)

## [一、目的](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/13?id=一、目的)

在前面学习 Scrapy 的时候，我们用过管道，它其实就是一个类，这个类的`process_item`方法，在这个方法中，可以实现将数据存储到 CSV 文件中

但来了一个爬虫存储的项目，它需要在存储数据，先进行清洗数据再办（之前清除就是删除不符合要求的数据），然后如何改数据。此时怎么改呢？

问：多个管道

## [二、自定义管道注意点](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/13?id=二、自定义管道注意点)

如果我们需要自定义管道（pipeline），那么现在要注意在管道类中可以写的方法如下：

1. ```
   process_item(self,item,spider)
   ```

   ：

   - 管道类中必须有的职能
   - 实现对项目数据的处理
   - 一般情况下`return item`，如果没有回报，那么，将不会传递给权重低的`process_item`

2. ```
   open_spider(self, spider)
   ```

   ：

   - 在爬虫开启的时候只执行一次
   - 在这里可以连接数据库、打开文件等

3. ```
   close_spider(self, spider):
   ```

   - 在爬虫关闭的时候只执行一次
   - 在这里可以关闭数据库，关闭文件等

## [三、管道文件的修改](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/13?id=三、管道文件的修改)

具体的操作，请在`pipelines.py`代码中完善

示例代码如下：

```python
import json
from pymongo import MongoClient


class ItcastFilePipeline(object):
    def open_spider(self, spider):  # 在爬虫开启的时候仅执行一次
        if spider.name == 'itcast':
            self.f = open('json.txt', 'a', encoding='utf-8')
    
    def close_spider(self, spider):  # 在爬虫关闭的时候仅执行一次
        if spider.name == 'itcast':
            self.f.close()
    
    def process_item(self, item, spider):
        if spider.name == 'itcast':
            self.f.write(json.dumps(dict(item), ensure_ascii=False, indent=2) + ',\n')
        # 不return的情况下，另一个权重较低的pipeline将不会获得item
        return item


class ItcastMongoPipeline(object):
    def open_spider(self, spider):  # 在爬虫开启的时候仅执行一次
        if spider.name == 'itcast':
            # 也可以使用isinstanc函数来区分爬虫类:
            con = MongoClient(host='127.0.0.1', port=27017)  # 实例化mongoclient
            self.collection = con.itcast.teachers  # 创建数据库名为itcast,集合名为teachers的集合操作对象
    
    def process_item(self, item, spider):
        if spider.name == 'itcast':
            self.collection.insert(item)
            # 此时item对象必须是一个字典,再插入
            # 如果此时item是BaseItem则需要先转换为字典：dict(BaseItem)
        # 不return的情况下，另一个权重较低的pipeline将不会获得item
        return item
复制错误复制成功...
```

## [四、开启管道](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/13?id=四、开启管道)

在settings.py中设置开启管道

```python
......
ITEM_PIPELINES = {
    'myspider.pipelines.ItcastFilePipeline': 400, # 400表示权重
    'myspider.pipelines.ItcastMongoPipeline': 500, # 权重值越小，越优先执行！
}
......复制错误复制成功...
```

**思考：在设置中能够开启多个管道，为什么需要开启多个？**

1. 不同管道的数据，可以通过爬取蜘蛛名称属性来处理不同的虫子的数据
2. 的管道能够对一个或多个不同的虫子进行不同的数据处理程序的操作，例如一个进行数据清洗，一个进行数据的保存
3. 同一个管道类也可以处理不同虫子的数据，通过爬虫名属性来处理不同的虫子的数据

## [五、管道使用注意点](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/13?id=五、pipeline使用注意点)

1. 使用之前需要在`settings.py`中开启
2. 多个在管道项目中的位置可以近自定义，距离引擎的远值，越近数据越先经过：**权重项目中值优先执行**
3. 有多个管道的时候，什么`process_item`方法应该`return item`，否则之后一个管道取到的数据为无值
4. pipeline中`process_item`的方法有，否则item没有必须接收和处理办法
5. `process_item`方法接受item和spider，其中spider表示当前传递item过来的spider
6. `open_spider(spider)`:能够在爬虫开启的时候执行一次
7. `close_spider(spider)`:能够在爬虫关闭的时候执行一次
8. 两个常用的连接数据库和数据库的方法，在爬虫开启和数据库的连接方式，在爬虫的爬行时连接和建立这个连接和数据库的连接



# [去重](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/14?id=去重)

## [一、目的](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/14?id=一、目的)

在实际进行爬取某个网站的时候，可能由于某些原因导致虫子以外的其他原因结束等，当开发人员修复之后，需要在爬取之前的基础上爬取已经爬取的 URL 或者过滤掉数据，这就是去重

1. 可以判断URL是否爬取过
2. 可以判断数据是否存储过

## [二、具体操作过程](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/14?id=二、具体操作过程)

爬取北京新发蔬菜基地网站上的蔬菜水果地价，网址： http: [//www.fadi.com.cn/marketanalysis/0/list/1.shtml](http://www.xinfadi.com.cn/marketanalysis/0/list/1.shtml)

具体的代码请参考：[https://gitee.com/dong4716138/Python19/tree/master/035-Scrapy%E6%A1%86%E6%9E%B6/07-%E7%AE%A1%E9%81](https://gitee.com/dong4716138/Python19/tree/master/035-Scrapy框架/07-管道)



# [暂停、恢复开始](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/15?id=暂停、恢复爬取)

## [一、目的](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/15?id=一、目的)

情况下，爬取大的站点，我们之后希望能暂停爬取，比如再恢复运行

于是就取了爬取和恢复的暂停

## [二、参考资料](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/15?id=二、参考资料)

关于 Scrapy 的暂停但很容易恢复，官方文档中是有说明的，不是详细的，地址如下：

中文版：https://www.osgeo.cn/scrapy/topics/jobs.html#

中文版：https://docs.scrapy.org/en/latest/topics/jobs.html

## [三、暂停爬取的方式](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/15?id=三、暂停爬取的方式)

想要实现暂停，Scrapy 的不需要，只需要在运行时自动运行即可

支持暂停爬取的命令如下：

```
scrapy crawl 爬虫名 -s JOBDIR=缓存scrapy信息的路径复制错误复制成功...
```

例如：

```
scrapy crawl mySpider -s JOBDIR=crawls/myspider-1复制错误复制成功...
```

## [四、怎样暂停爬虫](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/15?id=四、怎样暂停爬虫)

只需要在爬虫的过程中，在终端里`ctrl+c`点击，就可以让爬虫暂停

### [切记：只需要1次`ctrl+c`，不能2次](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/15?id=切记：只需要1次ctrlc，不能2次)

## [五、恢复采摘的方式](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/15?id=五、恢复爬取的方式)

与暂停爬取功能类，恢复爬取时，同样运行相同的命令

```
scrapy crawl 怕重名 -s JOBDIR=缓存scrapy信息的路径复制错误复制成功...
```

例如：

```
scrapy crawl mySpider -s JOBDIR=crawls/myspider-1复制错误复制成功...
```

## [六、注意](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/15?id=六、注意)

1. 如果在Spy项目里面有很多个爬虫（就是在爬虫文件夹下有很多其他的爬虫类），那么在指定`JOBDIR`时，就隔壁，不能用一个路径，比如myspder1爬虫`-s JOBDIR=crawls/myspider-1`，第2个爬虫myspder2用`-s JOBDIR=crawls/myspider-2`
2. 想要实现暂停功能一定是1次`ctrl+c`而不是2次



# [dont_filter 与 start_requests 方法](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/16?id=dont_filter与start_requests方法)

## [一、dont_filter](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/16?id=一、dont_filter)

当在使用scrapy生成一个新的请求请求对象时，有时需要指定过滤，有时需要我们指定不过滤

那什么是过滤呢？

如果在使用 Scrapy 爬取某个网站的过程中，生成了 2 次相同的第 1 个 URL，此时 Scrapy 处理次的时候肯定是发送请求的，但是是第 2 次收到相同的 URL 请求的请求，是否该发送请求呢？

来让我们看看`scrapy.Reqeust`默认的情况

![image-20201203205752737](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201203205752737.png)

通过上图能够，发现我们原来重新函数中生成了所有的请求请求，在初始化请求中的请求都被设置了“过滤”，即如果如果这个 URL 再收到相同的不再发送

大白话：以后你生成新的URL如果参数不管多少次生成的话，就会生成Scrapy帮你抄录的话，如果在创建请求对象的时候，需要命名指定`dont_filter=True`

## [二、start_requests](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/16?id=二、start_requests)

`start_requests`方法类`scrapy.Spider`中的方法，这个方法虽然之前我们从没有讲过讲过，但现在有必要

Scrapy的学习虫项目，我想现在大家不会了，操作流程是：

1. 创建一个项目( `scrapy startproject mySpder`)
2. 进入项目文件夹( `cd mySpider`)
3. 大家爬虫( `scrapy genspider my_spider xxx.com`)
4. 然后修改自定义的爬虫类中的`start_urls`列表中的点击网址
5. 写`parse`等功能
6. 写`process_item`等管道职能
7. 写下件中间等

上面的步骤中`start_urls`是一个列表，它包含的是URL字符串，而Scrapy引擎传递的是Request对象，那这个`start_urls`是怎样被处理的呢？

语句Scrapy中是否有判断方法列表：当前爬虫类是否有判断方法`start_requests`，如果没有，提取爬虫`start_urls`的URL，然后创建请求对象。`start_reqeusts`写出的方法，只要保证该方法的返回值可以自动学习

说了这么多，到现在为止我们没有像什么`start_requests`方法一样，Scrapy正常运行吗？

来看看原因：

场景1：如果`start_urls`则中的url是需要登录后才能访问的url，需要使用start_request并在其中手动添加地址上cookie

所以：默认情况下`start_urls`中的URL在生成请求对象时，都是设置为不过滤，即`dont_filter=True`如果想使用暂停、爬取功能的话，就需要通过这种方法了

场景 3：如果在`start_urls`中的 URL 需要使用`POST`提交的话，则需要在`start_requests`方法中



# [scrapy_redis实现增量爬虫](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/17?id=scrapy_redis实现增量爬虫)

## [一、引进](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/17?id=一、引入)

在前面我们学习可以在运行爬取项目的时候，使用`scrpay crawl 爬虫名 -s JOBDIR=xxx`来实现暂停、恢复提取（其实就是在爬升的时候，再次的时候开始继续上爬），这种虽然能够实现爬升爬取，无法从`JOBDIR`指定的路径但是我们现在的情况是我们现在去取的

为了搞清楚这些到底是什么，如下图

![image-20201206191935426](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201206191935426.png)

我们给scrapyredis模块，继续研究上面的文件意味着添加到底什么含义

## [二、安装](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/17?id=二、安装)

```
pip install scrapy-redis  -i https://pypi.tuna.tsinghua.edu.cn/simple复制错误复制成功...
```

## [三、配置](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/17?id=三、配置)

想要让scrapy实现增量爬取（即暂停、配置），就需要在scrapy项目中的`settings.py`文件中进行

具体如下：

```python
""" scrapy-redis配置 """
# 调度器类
SCHEDULER = "scrapy_redis.scheduler.Scheduler"
# 指纹去重类
DUPEFILTER_CLASS = "scrapy_redis.dupefilter.RFPDupeFilter"
# 是否在关闭时候保留原来的调度器和去重记录，True=保留，False=清空
SCHEDULER_PERSIST = True
# Redis服务器地址
REDIS_URL = "redis://127.0.0.1:6379/1"  # Redis默认有16库，/1的意思是使用序号为2的库，默认是0号库（这个可以任意）复制错误复制成功...
```

将上述配置添加到`settings.py`的空白处，效果：

![image-20201206192424033](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201206192424033.png)

除了4行之外，没有其他配置的地方。

## [四、运行&看效果](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/17?id=四、运行amp看效果)

### [1. 运行](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/17?id=_1-运行)

在终端中运行爬虫命令

```
scrapy crawl 爬虫名复制错误复制成功...
```

### [2.看效果](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/17?id=_2-看效果)

[下豆图看的效果是爬取瓣电影top250的爬虫执行的效果，地址： https](https://gitee.com/dong4716138/Python19/tree/master/036-Scrapy-Redis/03-scrapy-redis暂停、恢复爬取（debugURL中的pagenumber问题）/douban) ://gitee.com/dong4716138/Python19/tree/master/036-Scrapy-Redis/03-scrapy-redis% [E6%9A%82%E5%81%9C%E3%80%81%E6%81%A2%E5%A4%8D%E7%88%AC%E5%8F%96%EF%BC%88debugURL%E4% B8%AD%E7%9A%84页码%E9%97%AE%E9%A2%98%EF%BC%89/豆瓣](https://gitee.com/dong4716138/Python19/tree/master/036-Scrapy-Redis/03-scrapy-redis暂停、恢复爬取（debugURL中的pagenumber问题）/douban)

在爬取的过程中，点击一次`ctrl+c`，打开爬虫暂停爬取，Redis客户端，此时会看到在Redis数据库中的1号库中，2个key

第1个为：`top250:dupfilter`，界面如下：

![image-20201206192946719](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201206192946719.png)

这个打标的编号是在这个打标点`ctrl+c`之前进行的如果再有同样的请求那么就不会在取

第2个为：`top250:requests`，界面如下：

![image-20201206193003672](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201206193003672.png)

这个关键的中在刚刚点击`ctrl+c`之前，还没有得来及爬取的请求，从上图的第一个我们能够`https://movie.douban.com/top250?start=50&filter=`显示的信息，这个URL要求来得及爬取

### [3. 恢复提取](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/17?id=_3-恢复爬取)

在终端中，继续`scrapy crawl 爬虫名`看到会在运行上运行基础上继续爬取

## [五、总结](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/17?id=五、总结)

- scrapy可以通过插件`scrapy_redis`来将爬取过程中的信息存储到Redis中的实现能力
- 通过Redis的图形化更好地看到这样的“最终实现”的结果、可以完成的过程



# [scrapy_redis 卡车蠕虫](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/18?id=scrapy_redis实现分布式爬虫)

在前面的scrapy能够使用我们已经使用爬虫爬取网站的数据进行比较，如果网站的数据比较好，我们就需要使用桌面边框来提供的获取数据

## [一、scrapy-redis是什么](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/18?id=一、scrapy-redis是什么)

我们已经能够学习到Spy了，它是它通用的虫虫代码，能写出一个简单的之前的时间就可以开始爬虫了

Scrapy-redis 是 spy 的一个组件，它使用了 Redis 数据库，以便更方便地让 Scrapy-redis 为电话目的取用

Scrapy要开始改进的启动模式可以同时查看一个相似的客户端程序。

## [二、是什么](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/18?id=二、分布式是什么)

简单的说，不同的不同就是的服务器（服务器，ip）共同完成一个任务，并且数据出乱子

比说：公司到年底要了这一年公司所有的收入与业绩统计公司业绩的情况，所以请一个人来做，此时（因为只有1个人做事）。有9位来做此事，每个人都有10人，此时成为多个人，因为每个人都是的个体，所以这个任务由我们共同负责一个负责人。

看看，这10名工作人员在统计数据之前，他们会先做什么呢？

。。。想象看，给你1个。。。

他们约定好，或者谁分配好，先把谁的统计结果好，这样把最后的统计结果就是总结果了

所以说：系统中的一个很重要的事情就是，任务的分配与结果的收集

## [三、scrapy_redis的作用](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/18?id=三、scrapy_redis的作用)

scrapy_redis在scrapy_redis的基础上实现了更多、更强大的功能，具体在py照片上：

请求实现请求和请求的集合来实现：

- 断点续写

  通俗的说法：本次爬取的数据，下载再运行时不会爬取，只有在爬取之前没有爬过的数据

- 快速快速抓取

  通俗的说法：多台电脑（也可以在一台电脑上运行多个程序来模拟）可以一起提取数据，而且不会有冲突

## [四、scrapy_redis的工作流程](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/18?id=四、scrapy_redis的工作流程)

### [1.回顾scrapy的流程](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/18?id=_1-回顾scrapy的流程)

![img](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/1.3.3.scrapy%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%A8%8B.png)

也可以用下面的图标来理解（图表示是同一个英文字母，两种不同的方式）

![图像](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/62d1dc3038e8b596d6df6f8e8a28258a.jpg)

#### [思考：](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/18?id=思考：)

> 如果要实现一个高性能，即多台服务器同时，需要怎么做呢？

### [2. scrap_redis 电阻的核心](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/18?id=_2-scrapy_redis实现分布式的核心)

![图像](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/0a94645a8f10707fe80610b5ebeb945e.jpg)

#### [说明](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/18?id=说明)

本来只有1个scrapy的时候，所有对象的请求，都可以直接存放到内存中，此时请求完成本台电脑上的功能，但是电脑上的scrapy是不能获取它一个计算机中的内存数据的，所以用了 Redis 的数据库，将直接存储到内存中的数据（像请求请求等）又换了 Redis 中（因为 Redis 效率非常高，它而不是用 MySQL、MongoDB 数据库），因为 Redis是支持网络访问的，所以在本电脑上的Redis中存储的数据，就可以让其他电脑上的scrapy去使用，哪个请求对象已经处理过，哪个没有并处理过，一目了然。

请结合本说明与上图多理解会有种醍醐灌顶的感觉，你会茅顿开的。

### [3. scrapy_redis的流程](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/18?id=_3-scrapy_redis的流程)

1. 在scrapydis中，所有的待抓取_request对象和request去指纹都存在使用的redis中的重
2. 所有服务器中的scrapy进程同一个redis中的请求对象的资源
3. 所有的请求对象存入redis前，政府通过该redis中的请求指纹集合进行判断，之前是否已经存入过
4. 在默认情况下所有的数据会保存在redis中

具体流程如下：

![img](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/7.4.2.scrapy_redis%E7%9A%84%E6%B5%81%E7%A8%8B.png)

## [五、scrapy-redis 案例](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/18?id=五、scrapy-redis分布式案例)

有四台电脑：Windows 10、Mac OS X、Ubuntu 16.04、CentOS 7.2，任何一台电脑都可以作为 Master 端或 Slaver 端，例如：

- `Master端`（服务器）：Windows 10，使用一个核心Redis数据库，不负责，只负责**指纹识别重取，请求的分配数据的存储**
- `Slaver端`（爬虫程序）：使用Mac OS X 、Ubuntu 16.04、CentOS 7.2，负责执行爬虫程序，运行过程中提交新的执行端给Master

![这里写图片描述](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/70.png)

1. 首先Slaver端从Master端拿任务（Request、url）进行数据抓取，Slaver抓取数据的同时，产生新的任务请求便提交给Master处理；
2. Master只有一个Redis数据库，负责将未加入的Request去重和任务分配，将处理后的Request待处理进程，并存储爬取的数据。

scrapy-redis默认使用的这种策略，我们实现起来很简单，因为任务调度等工作scrapy-redis都帮我们做好了，我们只要继承RedisSpider、指定redis_key就行了。

是：scrapy-redis调度的任务是请求对象，里面的信息量大（包括改进的url，还有回调函数、headers等信息），可能导致的结果就是会降低爬虫速度，而且会占用Redis大量的存储空间，所以如果要保证效率，那么就需要一定的硬件水平。

## [小结](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/18?id=小结)

Scarpy_redis的轮胎工作原理

- 在scrapydis中，所有的待抓取_公有的对象和去重的指纹都用的redis中
- 所有的服务器公用同一个中的请求对象的时间
- 所有的请求对象存入重新分配，政府通过请求对象的指纹前进行判断，在此之前是否已经存入过



# [scrapy_redis靴虫案例](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/19?id=scrapy_redis分布式爬虫案例)

## [一、说明](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/19?id=一、说明)

豆电影225，我们已经对它展示过什么经典案例0，大家都想顶一下，给大家是优秀的优秀级虫，再次使用这个

## [二、架构](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/19?id=二、架构)

![image-20201206203140387](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201206203140387.png)

## [三、Redis配置](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/19?id=三、redis配置)

在这种情况下，Redis 服务值运行本地电脑访问，即 Redis 运行在哪台电脑上就默认只允许这台电脑上的软件连接试用它

我们用电脑来自动取用，就需要用Redis进行操作，因此需要对Redis进行

配置参考地址：https://www.cnblogs.com/masonblog/p/12726914.html

注意

1. Mac配置文件的路径是：`/usr/local/etc/redis.conf`

2. 配置完成后需要重新启动Redis服务器，并指定最新的这个Redis配置文件，如果配置文件是`/usr/local/etc/redis.conf`，那么重新运行Redis的是`redis-server /usr/local/etc/redis.conf`

3. 如果不配置Redis远程访问，那么在运行运行虫命令的时候`scrapy crawl 爬虫名`，会看到爬虫停止了，提示爬图如下：

   

4. 别忘了修改爬虫的配置文件`settings.py`，将Redis服务器地址改为你运行Redis服务器的ip

## [四、效果](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/19?id=四、效果)

1. 在节点1、2开启爬虫（此时爬虫没有开始，而是在等待Redis中`top250:start_urls http://xxxxx`）

   

2. 在redis客户端中输入推送指令，参考格式：（一定要选择爬虫`settings.py`文件中配置的数据库，然后在输入推送命令）

   ```shell
   $redis > select 2
   $redis > lpush top250:start_urls https://movie.douban.com/top250?start=0&filter=复制错误复制成功...
   ```

   

3. 爬虫开始了

   

4. Redis中此时爬取过程的数据，比如指纹等

   

5. 验证结果

   1. Ubuntu18.04节点，爬取的CSV文件里面有75条信息，如下图：

      

   2. MacOS节点，爬取的CSV文件里面有175条信息，如下图：

      

   3. 75+175=250条信息，是完全正确的

## [五、总结](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/19?id=五、总结)

- scrapy的功能让我们用它的redis，而现在的功能让pyre的功能已经深入挖掘了_redis的功能



# [scrapy_re中dis挖掘案例-从Redis提取m数据](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/20?id=scrapy_redis分布式案例-从redis中提取item数据)

## [一、架构](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/20?id=一、架构)

![image-20201206215852207](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201206215852207.png)

## [二、解决的问题](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/20?id=二、解决的问题)

上一节课到使用scrapy_redis可以运行多个线程跟踪网站一起讲的问题（即在各个线程中提取的数据），编组，在各个线程中都分别进行存储数据，即在蠕虫节点1中爬取到数据后在管道进程_item函数中将进行存储，而蠕虫节点2中执行相同的操作，在爬到最后的结果是：所有的爬取到数据都分布在爬虫节点服务器上，没有多数据虫的集成

所以为了解决这个问题，scrpay_redis 为我们提供了一个可能特殊的管道，可以直接将存储的数据保存到 Redis 中

保存到 Redis 怎么改做，scrapy_redis 到是没有提供的，现在我们要根据开发者自己的实际需求进行开发，比如在虫结构中添加一个设备单独负责从 Redis 中提取数据，然后存储，这样的问题就在爬取到多个节点

## [三、代码参考](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/20?id=三、代码参考)

1. 对于base64与图片之间的转换，可以参考：[https ://blog.csdn.net/qq_34449006/article/details/84312550](https://blog.csdn.net/qq_34449006/article/details/84312550)
2. 本案例Top25爬取代码请参考git仓库代码，gitee仓库地址：[https://gitee.com/dong4716138/Python19/tree/master/036-Scrapy-Redis/06-%E7%AE%A1%E9%81 %93%E5%AD%98%E5%82%A8%E4%BF%A1%E6%81%AF%E5%88%B0Redis/豆瓣](https://gitee.com/dong4716138/Python19/tree/master/036-Scrapy-Redis/06-管道存储信息到Redis/douban)
3. 从Redis提取数据相关代码请参考git仓库，gitee仓库地址：[https://gitee.com/dong4716138/Python19/tree/master/036-Scrapy-Redis/07-%E4%BB%8ERedis%E4%B8 %AD%E6%8F%90%E5%8F%96item%E6%95%B0%E6%8D%AE%E5%B9%B6%E5%AD%98%E5%82%A8](https://gitee.com/dong4716138/Python19/tree/master/036-Scrapy-Redis/07-从Redis中提取item数据并存储)



# [Scrapy项目部署-scrapyd](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=scrapy项目部署-scrapyd)

## [一、说明](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=一、说明)

Scarpy是一个爬虫框架，而scrapyd相当于一个组件，能够将爬虫项目进行远程部署，安排使用等

## [二、服务端（即运行爬虫的电脑）](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=二、服务端（即运行爬虫的电脑）)

### [1.安装scrapyd](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=_1-安装scrapyd)

安装命令如下

```
pip install scrapyd  -i https://pypi.tuna.tsinghua.edu.cn/simple复制错误复制成功...
```

## [2. 运行](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=_2-运行)

在终端中输入

```
scrpayd复制错误复制成功...
```

运行效果如下：

![图像-20201207201710027](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207201710027.png)

### [3.修改配置，方便远程访问](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=_3-修改配置，以便远程访问)

使用`ctrl+c`停止上一步运行的`scrapyd`

在运行`scrapyd`命令的路径下，要新建文件`scrpayd.conf`文件

![image-20201207202133958](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207202133958.png)

输入内容：

```python
[scrapyd]
# 网页和Json服务监听的IP地址，默认为127.0.0.1（只有改成0.0.0.0 才能在别的电脑上能够访问scrapyd运行之后的服务器）
bind_address = 0.0.0.0
# 监听的端口，默认为6800
http_port   = 6800
# 是否打开debug模式，默认为off
debug = off
复制错误复制成功...
```

效果如下：

![图像-20201207202201245](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207202201245.png)

### [4.运行看效果](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=_4-运行看效果)

在刚刚新建的`scrpayd.conf`文件所在的路径下通过终端运行`scrapyd`，命令如下

```python
scrapyd复制错误复制成功...
```

![image-20201207202438924](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207202438924.png)

然后在打开电脑上，打开浏览器输入，运行`scrapyd`命令的电脑的ip、端口，下图

![图像-20201207202604080](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207202604080.png)

## [代码上传端（即本地编写的三爬虫的电脑）](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=三、代码上传端（即本地编写scrapy爬虫代码的电脑）)

### [1. 安装scrapyd-client](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=_1-安装scrapyd-client)

安装命令如下：

```
pip install scrapyd-client  -i https://pypi.tuna.tsinghua.edu.cn/simple复制错误复制成功...
```

### [2.配置Scrapy项目](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=_2-配置scrapy项目)

#### [2.1 配置如下](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=_21-配置如下)

![image-20201207202947527](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207202947527.png)

注意：

- 如果运行scrapy的节点只有1个，那么上面只需要留1个部署配置即可，如果有多个就可以配置多个部署

#### [2.2 检查配置是否正常](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=_22-检查配置是否ok)

在scrapy项目路径中，运行如下命令，可以检查scrapy配置是否正确

```
scrapyd-deploy -l复制错误复制成功...
```

注意：

- 注意是小写的L,不是数字1

如果看到如下效果，表示scrapy项目配置ok

![图像-20201207203301782](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207203301782.png)

### [3. 发布scrapy项目到scrapyd所在的服务器（此时爬虫未运行）](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=_3-发布scrapy项目到scrapyd所在的服务器（此时爬虫未运行）)

#### [3.1 命令格式](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=_31-命令格式)

```
scrapyd-deploy <target> -p <project> --version <version>复制错误复制成功...
```

- 目标：就是前面的配置文件中部署后面的目标名字，例如`ubuntu-1`
- 项目：可以随意定义，跟爬虫的工程名字一样，一般建议和爬虫项目名称相同
- 版本：自定义版本，默认不写为目标号，一般不写

#### [3.2 发布爬虫到服务器](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=_32-发布爬虫到服务器)

```
scrapyd-deploy ubuntu-1 -p douban复制错误复制成功...
```

注意

- 爬虫目录下不要发布可以放掉的py文件，放其他的py文件会导致失败，但是当爬虫发布成功后，会在当前目录生成一个setup.py文件，删除。

效果如下：

![图像-20201207203637010](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207203637010.png)

发布成功之后，会在运行scrapyd的服务器上看到，如下效果：

![image-20201207203859617](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207203859617.png) ![image-20201207204044924](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207204044924.png)

## [四、运行爬虫](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=四、运行爬虫)

### [1. 运行命令哪找？](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=_1-运行命令哪找？)

scrapyd 已经提供了如何开始运行爬虫，如下图所示

![image-20201207204134941](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207204134941.png)

### [2.发送运行爬虫命令](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=_2-发送运行爬虫命令)

比如上面的命令复制，然后在终端中适当的修改，就可以开启爬虫，

```
curl http://10.211.55.5:6800/schedule.json -d project=douban -d spider=top250复制错误复制成功...
```

效果如下：

![image-20201207204600948](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207204600948.png)

注意：

- 使用相同的方式可以将scrapy项目发布到Ubuntu-2（即另外一个爬虫节点上）在此不演示情况了，大家根据实际情况处理

### [3.通过浏览器看现象](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=_3-通过浏览器看现象)

![image-20201207204827693](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207204827693.png)

从上图可以看到，目前top250这个虫子已经开始爬取了

### [4. 验证是否开始爬取](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=_4-验证是否开始爬取)

#### [4.1 看scrapyd端](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=_41-看scrapyd端)

![image-20201207204959617](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207204959617.png)

#### [4.2 看Redis，这里用的是7号库](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=_42-看redis，此时用的是7号库)

![图像-20201207205023671](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207205023671.png)

## [五、停止爬虫](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=五、停止爬虫)

命令如下：

```
curl http://ip:6800/cancel.json -d project=项目名 -d job=任务的id值复制错误复制成功...
```

![图像-20201207205327024](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207205327024.png)

例如：

```
curl http://10.211.55.5:6800/cancel.json -d project=douban -d job=121cc034388a11ebb1a7001c42d0a249复制错误复制成功...
```

![image-20201207205429940](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207205429940.png)

现象：

![image-20201207205552263](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207205552263.png)

## [六、注意](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/21?id=六、注意)

1. 如果scrapy项目代码，修改了，只需要重新发布到scrapyd具备的服务器能力
2. 如果scrapy项目暂停了，可以再次通过`curl`的发送命令让其“断点续写”



# [Scrapy项目部署-图形化操作ScrapydWeb](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/22?id=scrapy项目部署-图形化操作scrapydweb)

## [一、介绍](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/22?id=一、介绍)

### [1、scrapy是什么？](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/22?id=_1、scrapy是什么？)

一个爬虫框架，你可以创建一个爬虫项目

### [2、scrapyd是什么？](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/22?id=_2、scrapyd是什么？)

差不多是一个组件，能够将零碎的项目进行远程部署，调度使用等

### [3、scrapydweb是什么？](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/22?id=_3、scrapydweb是什么？)

是一个基于scrapyd的可视化组件，集成提供更多的可视化功能和更优美的界面

注意：

- scrapydweb 的时候，所以采用flask框架的同学是可以适合定制的
- 官方文档：https://github.com/my8100/files/blob/master/scrapydweb/README_CN.md

## [二、安装ScrapydWeb](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/22?id=二、安装scrapydweb)

在运行scrapyd的服务器上，安装scrapydweb，命令如下：

```
pip install scrapydweb  -i https://pypi.tuna.tsinghua.edu.cn/simple复制错误复制成功...
```

效果如下：

![图像-20201207210300967](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207210300967.png)

## [三、运行](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/22?id=三、运行)

### [1.运行命令](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/22?id=_1-运行命令)

注意：一定是要保证scrapyd运行成功，并且不退出的情况下运行如下命令，可以在另外一个新终端中运行

```
scrapydweb复制错误复制成功...
```

第一次运行，不会成功，但会创建一个文件，效果如下：

![图像-20201207210502992](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207210502992.png) ![图像-20201207210519270](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207210519270.png)

第二次运行，会成功如下：

![image-20201207210611351](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207210611351.png)

### [2. 浏览器访问图形化管理页面](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/22?id=_2-浏览器访问图形化管理页面)

提示如上图所示，注意ip改为当前爬取节点的ip

![image-20201207210728316](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207210728316.png)

## [四、基本使用](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/22?id=四、基本使用)

### [1.发布scrapy项目](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/22?id=_1-发布scrapy项目)

![image-20201207213415788](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207213415788.png) ![image-20201207213505624](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207213505624.png) ![image-20201207213630536](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207213630536.png) ![image-20201207213650370](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207213650370.png)

### [2. 运行爬虫](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/22?id=_2-运行爬虫)

![image-20201207213814923](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207213814923.png) ![image-20201207213848772](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207213848772.png)

运行成功之后，现象变成几张图片所示

![图像-20201207213929063](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207213929063.png) ![图像-20201207214021483](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207214021483.png) ![图像-20201207214416106](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207214416106.png) ![image-20201207214139557](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207214139557.png)

红字号已经收到了（至有dis，库里看到你是否已经在scrapy项目中已经看到了8个数据）

![图像-20201207214215277](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207214215277.png)

### [3.停止爬虫](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/22?id=_3-停止爬虫)

![image-20201207214328581](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207214328581.png)

### [4.断点续写](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/22?id=_4-断点续爬)

这个爬虫没有爬取可以结束，只是被暂停了，通过下面的按钮开启爬取

![image-20201207214544177](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207214544177.png)

## [五、开启用户认证](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/22?id=五、开启用户认证)

### [1.配置](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/22?id=_1-配置)

找到运行`scrapydweb`命令时的文件`scrapydweb_setting_v10.py`，修改如下：

![image-20201207215204658](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207215204658.png)

### [2.运行看效果](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/index.html#/22?id=_2-运行看效果)

![图像-20201207214905672](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207214905672.png)



# Scrapy项目部署-图形化操作Gerapy

## 一、说明

Gerapy是一款用于管理人员开发的操作虫），是部署项目的实时化可视化，把项目的重新部署到一个项目中，便于控制软件运行控制（控制运行、管理、管理、管理、管理）。 。

gerapy和scrapyd的关系就是，我们可以通过gerapy中配置scrapyd后，不使用命令，直接通过图形化界面开启爬虫。

## 二、安装

### 1. 命令

```
pip install gerapy  -i https://pypi.tuna.tsinghua.edu.cn/simple复制错误复制成功...
```

### 2. 测试

安装成功之后，可以在终端输入gerapy命令进行测试：

![图像-20201207221320039](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/ukloh.png-1)

## 三、使用

### 1.创建一个gerapy工作目录

命令如下：

```
gerapy init复制错误复制成功...
```

效果：

![image-20201207221616954](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207221616954.png)

会生成文件夹，如下

![图像-20201207221710168](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207221710168.png)

### 2. 创建sqlite数据库，部署scrapy项目版本等

![image-20201207221838890](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207221838890.png)

创建成功之后，用tree命令，查看当前的文件列表

![图像-20201207222002824](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207222002824.png)

### 3. 创建用户名密码

执行以下命令可以创建新的用户名、密码

```
gerapy createsuperuser复制错误复制成功...
```

效果如下：

![图像-20201207222630615](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207222630615.png)

### 4. 启动服务

命令如下：

```
gerapy runserver复制错误复制成功...
```

效果如下：

![图像-20201207222054921](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207222054921.png)

用浏览器访问上面的地址，效果

![图像-20201207222714723](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207222714723.png)

用户签名创建用户名密码，点击登录后，效果如下：

![图像-20201207222754023](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207222754023.png)

## 三、创建主机

![图像-20201207222905313](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207222905313.png) ![image-20201207222953635](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207222953635.png) ![图像-20201207223020986](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207223020986.png)

## 四、运行已存在的项目

![image-20201207223144471](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207223144471.png)

![图像-20201207223159116](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207223159116.png) ![image-20201207223241611](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207223241611.png)

## 五、停止

![image-20201207223357208](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207223357208.png) ![image-20201207223447076](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207223447076.png)

## 六、多个部署（多个节点部署）

### 1.新建项目

![图像-20201207224020187](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207224020187.png) ![image-20201207224122371](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207224122371.png) ![image-20201207224144824](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207224144824.png)

### 2. 部署

#### 2.1 打包打包

![图像-20201207224206745](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207224206745.png) ![图像-20201207224256131](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207224256131.png)

![image-20201207224457957](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207224457957.png)

#### 2.2 部署部署

注意：为了演示部署豆瓣成功，远程登录scrapyd运行的服务器，然后停止项目了这个命令，然后再删除了`scrapyd.conf`除掉的文件，最后重新运行`scrapyd`

![image-20201207224554954](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207224554954.png) ![image-20201207224606490](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207224606490.png) ![图像-20201207224729896](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207224729896.png)

此时点击“主机管理”，分别点击调度

![image-20201207225338469](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207225338469.png)

都只有1个豆瓣的项目了

![图像-20201207225409020](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207225409020.png)

#### 2.3 点击运行之后，开启爬取

![image-20201207225636441](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207225636441.png)

## 七、定时爬取等

![图像-20201207230015665](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207230015665.png) ![图像-20201207230128451](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207230128451.png) ![图像-20201207230213071](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207230213071.png)

![image-20201207230313755](https://doc.itprojects.cn/0001.zhishi/python.0018.scrapy/assets/image-20201207230313755.png)
