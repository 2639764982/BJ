---
title: python自动化简介
date: 2022-04-05 21:26:50
categories:
 - python自动化
tags:
 - python自动化
 - selenium
 - api自动化
 - 自动化测试框架
---

<h2>
    原理与安装
</h2>

<h4>一、Selenium</h4

<h5>原理</h5>

<p>Selenium 是一套 Web网站 的程序自动化操作 解决方案。通过它，我们可以写出自动化程序，像人一样在浏览器里操作web界面。 比如点击界面按钮，在文本框中输入文字 等操作。而且还能从web界面获取信息。 比如获取 火车、汽车票务信息，招聘网站职位信息，财经网站股票价格信息 等等，然后用程序进行分析处理。Selenium 的自动化原理是这样的</p>

![](https://cdn2.byhy.net/imgs/api/tut_20200504110845_36.png)

<p>从上图可以看出：

我们写的自动化程序 需要使用 **客户端库**。

我们程序的自动化请求都是通过这个库里面的编程接口发送给浏览器。

比如，我们要模拟用户点击界面按钮， 自动化程序里面就应该 调用客户端库相应的函数， 就会发送 **点击元素** 的请求给 下方的 **浏览器驱动**。 然后，浏览器驱动再转发这个请求给浏览器。

这个自动化程序发送给浏览器驱动的请求 是HTTP请求。

客户端库从哪里来的？ 是Selenium组织提供的。

Selenium组织提供了多种 编程语言的Selenium客户端库， 包括 java，python，js， ruby等，方便不同编程语言的开发者使用。

我们只需要安装好客户端库，调用这些库，就可以发出自动化请求给浏览器咯。



**浏览器驱动** 也是一个独立的程序，是由浏览器厂商提供的， 不同的浏览器需要不同的浏览器驱动。 比如 Chrome浏览器和 火狐浏览器有 各自不同的驱动程序。

浏览器驱动接收到我们的自动化程序发送的界面操作请求后，会转发请求给浏览器， 让浏览器去执行对应的自动化操作。



浏览器执行完操作后，会将自动化的**结果**返回给浏览器驱动， 浏览器驱动再通过HTTP响应的消息返回给我们的自动化程序的客户端库。

自动化程序的客户端库 接收到响应后，将结果转化为 `数据对象` 返回给 我们的代码。

我们的程序就可以知道这次自动化操作的结果如何了。</p>

<p>我们再总结一下，selenium 自动化流程如下：

1. 自动化程序调用Selenium 客户端库函数（比如点击按钮元素）

2. 客户端库会发送Selenium 命令 给浏览器的驱动程序

3. 浏览器驱动程序接收到命令后 ,驱动浏览器去执行命令

4. 浏览器执行命令

5. 浏览器驱动程序获取命令执行的结果，返回给我们自动化程序

6. 自动化程序对返回结果进行处理</p>

   

<h4>安装</h4>

<p>Selenium环境的安装主要就是安装两样东西： `客户端库` 和 `浏览器 驱动` 。</p>

<h5>安装客户端库</h5>

<p>不同的编程语言选择不同的Selenium客户端库。

对应我们Python语言来说，Selenium客户端库的安装非常简单，用 pip 命令即可。

打开 命令行程序，运行如下命令</p>

```
pip install selenium
```

<p>
   如果安装不了，可能是网络问题，可以指定使用国内的豆瓣源 
</p>

```
pip install selenium -i https://pypi.douban.com/simple/
```



<h4>
    安装浏览器和驱动
</h4>

<p>
    浏览器驱动 是和 浏览器对应的。 不同的浏览器 需要选择不同的浏览器驱动。目前主流的浏览器中，谷歌 Chrome 浏览器对 Selenium自动化的支持更加成熟一些。推荐大家使用 Chrome浏览器 。</p>


[点击下载谷歌浏览器]( https://www.google.cn/chrome/)

<p>
    确保Chrome浏览器安装好以后，请大家打开下面的连接，访问Chrome 浏览器的驱动下载页面
</p>
[谷歌浏览器驱动下载地址](https://chromedriver.storage.googleapis.com/index.html)

<p>
    注意浏览器驱动 必须要和浏览器版本匹配，下图红圈里面的版本号 就是和浏览器版本号对应的
</p>

![](https://cdn2.byhy.net/imgs/api/tut_20201125093152_29.png)

<p>
    比如：当前Chrome浏览器版本是98, 通常就需要下载98开头的目录里面的驱动程序 。

注意：驱动和浏览器的版本号越接近越好，但是略有差别，比如98和97 ，通常也没有什么问题。


打开目录，里面有3个zip包，分别对应Linux、Mac、Windows平台。

如果我们是Windows平台的电脑，就下载 chromedriver_win32.zip

这是个zip包，下载下来之后，解压里面的程序文件 chromedriver.exe 到某个目录下面，注意这个目录的路径最好是没有中文名和空格的。

比如，解压到 d:\tools 目录下面。

也就是保证我们的Chrome浏览器驱动路径为 d:\tools\chromedriver.exe
</p>

如果你选择微软 Edge浏览器，[点击这里下载驱动](https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/)

基于selenium的web自动化环境搭建就是这些，比较简单。



<h4>简单示例</h4>

下面的代码, 可以自动化的 打开Chrome浏览器，并且自动化打开百度网站，可以大家可以运行一下看看。

```
from selenium import webdriver
from selenium.webdriver.chrome.service import Service

# 创建 WebDriver 对象，指明使用chrome浏览器驱动
wd = webdriver.Chrome(service=Service(r'd:\tools\chromedriver.exe'))

# 调用WebDriver 对象的get方法 可以让浏览器打开指定网址
wd.get('https://www.baidu.com')
```

其中，下面这行代码，就会运行浏览器驱动，并且运行Chrome浏览器

```
wd = webdriver.Chrome(r'd:\tools\chromedriver.exe')
```

注意，等号右边 返回的是 WebDriver 类型的对象，我们可以通过这个对象来操控浏览器，比如 打开网址、选择界面元素等。

<br>

而下面这行代码，就是使用 WebDriver 的 get 方法 打开网址 百度

```
wd.get('https://www.baidu.com')
```

执行上面这行代码时，自动化程序就发起了 打开百度网址的 `请求消息` ，通过浏览器驱动， 给 Chrome浏览器。

Chome浏览器接收到该请求后，就会打开百度网址，通过浏览器驱动， 告诉自动化程序 打开成功。



<h4>省略浏览器驱动路径</h4>

前面，我们的代码创建 WebDriver对象时，需要指定浏览器驱动路径，比如

```
from selenium.webdriver.chrome.service import Service
wd = webdriver.Chrome(service=Service(r'd:\tools\chromedriver.exe'))
```

这样写有几个问题：

一是，比较麻烦， 每次写自动化代码都 要指定路径。

二是，如果你的代码给别人运行，他的电脑上存放浏览器驱动的路径不一定和你一样（比如他的电脑是苹果Mac电脑），得改脚本。

有什么好办法呢？

我们可以把浏览器驱动 `所在目录` 加入环境变量 `Path` ， 写代码时，就可以无需指定浏览器驱动路径了，像下面这样

```
wd = webdriver.Chrome()
```

因为，Selenium会自动在环境变量 Path 指定的那些目录里查找名为chromedriver.exe 的文件。

一定要注意的是， 加入环境变量 Path 的，

不是浏览器驱动全路径，比如 `d:\tools\chromedriver.exe`

而是 浏览器驱动所在目录，比如 `d:\tools`



而且设置完环境变量后，别忘了重启IDE（比如 PyCharm） 新的环境变量才会生效。



那么，selenium又是如何 自动化地 在网页上 点击、输入、获取信息，将在接下来的章节要学习。



<h4>
    常见问题
</h4>

<h4>
    关闭 chromedriver 日志
</h4>

缺省情况下 chromedriver被启动后，会在屏幕上输出不少日志信息，如下

```
DevTools listening on ws://127.0.0.1:19727/devtools/browser/c19306ca-e512-4f5f-b9c7-f13aec506ab7
[21564:14044:0228/160456.334:ERROR:device_event_log_impl.cc(211)] [16:04:56.333] Bluetooth: bluetooth_adapter_winrt.cc:1072 Getting Default Adapter failed.
```

可以这样关闭

```
from selenium import webdriver

# 加上参数，禁止 chromedriver 日志写屏
options = webdriver.ChromeOptions()
options.add_experimental_option(
    'excludeSwitches', ['enable-logging'])

wd = webdriver.Chrome(options=options  # 这里指定 options 参数
)
```

<h4>
    浏览器首页显示防病毒重置设置
</h4>

有的朋友的电脑上Selenium自动化时，浏览器开始显示如下

![](https://cdn2.byhy.net/imgs/api/tut_20220226101749_73.png)

可以这样解决：

- 命令行输入 `regedit` ，运行注册表编辑器
- 在左边的目录树找到 `HKEY_CURRENT_USER\Software\Google\Chrome`
- 删除其下的 `TriggeredReset` 子项
- 关闭 注册表编辑器



<h2>
    选择元素的基本方法
</h2>



