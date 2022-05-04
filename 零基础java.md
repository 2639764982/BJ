---
title: 零基础java
date: 2022-04-25 15:26:50
tags:
- JAVA基础
categories:
- JAVA
---

# 变量与计算

## 读输入

```java
Scanner in = new Scanner(System.in);
System.out.println(in.nextLine());
```

## 字符串+

```java
System.out.println("Hello" + "world.");
Syetem.out.println("Hello" + 2);
System.out.println("Hello" + 2 + 3);
System.out.println(2+3 + "Hello");
```

## 变量

- 输入一个表示应该付多少元的数字，比如l2，它告诉你88，意思是如果你付100

```java
Scanner in = new Scanner(System.in);
int price = 0;
prince = in.nextInt();
int change = 100 - price;
System.out.println(change);
```

## 变量定义

- 变量定义一般形式就是：
  - <类型名称><变量名称>

- int price;
- int amount;
- int price,amount;

## 常量

- int change = 100 -price;
- 固定不变的数，是常量。
- 定义常量 final int AMOUNT =100;

- final是一个修饰符，加在int的前面，这个final的属性表示这个变量的值一旦初始化，就不能再修改了。

## 浮点数

### 计算身高程序

```java
Scanner in = new Scanner(System.in);
System.out.print("请分别输入身高的英尺和英寸，如输入\5 7\表示5英寸7英寸");
int foot = in.nextInt();
int inch = in.nextInt();
System.out.println("身高是：" + (foot + inch /12)* 0.3048) + "米");
```

## 强制类型转换

- 身高1.524米
- System.out.println("身高是："+（foot+inch/12）*0.3048 * 100）+”厘米“）;
- 身高是152.4厘米

- 如果想把一个浮点的小数部分去掉，变成整数

  ```java
  int i = 32/30;
  int i =(int)(32/3.0);判断
  ```

# 判断



