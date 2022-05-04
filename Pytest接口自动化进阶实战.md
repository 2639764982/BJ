---
title: Pytest接口自动化进阶实战
date: 2022-04-06 20:08:18
top_img: https://cms.liara.ir/wp-content/uploads/2020/07/pytest.jpg
tags:
- python自动化
- api自动化
categories:
- python自动化
cover: https://cms.liara.ir/wp-content/uploads/2020/07/pytest.jpg
---

<h1>
    一、为什么要用pytest来做自动化
</h1>

1.pytest是目前最主流的一个自动化测试框架

pytest的优点：

1.可以自动识别模块

文件名：格式为test_*.py或*_test.py文件

类：test开头

def xxxx():

​              pass

2.模块化的夹具fixture可用来管理各类测试资源

3.对unittest完全兼容

4.pytest是最能“装插”的开源测试框架

安装：pip install 插件名

5.pytest安装

```
pip install pytest
```

验证命令

```
pytest --version
```

<h1>
    二、接口测试简介
</h1>

接口组成元素

1.接口地址（url+端口+路径）

2.接口请求地址：post get delete put....

3.接口请求参数

4.响应数据



token用途简介

登陆系统 = 进医院

token = 绿码

拥有token才能访问系统内部的各个页面 = 拥有绿码才有进入医院的权限



<h1>
    三、用python代码实现接口测试
</h1>

相对于工具，python做接口自动化的优势

扩展性强

各种封装

可集成各种库跟工具

allure报告

jsonpath报文解析

jenkins持续集成



<h1>
    四、接口关键字封装
</h1>

jsonpath、get、post



<h1>
    五、用pytest框架编写接口自动化测试代码
</h1>

1.基本用例组织

从上往下，按照用例放置的顺序执行



2.接口关联

1）全局变量，类中或者文件中所有的测试函数方法都可以访问了

2）setup_class



<h1>
    六、Fixture+Conftest实现项目级token预置
</h1>


