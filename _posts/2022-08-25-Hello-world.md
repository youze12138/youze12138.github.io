---
title: Hello World
date: 2022-08-25 10:34:00 +0800
categories: [Java]
tags: [后端]
pin: true
author: BruceZhou

toc: true
comments: true
typora-root-url: ../../youze12138.github.io
math: false
mermaid: true
---

# 属于你的第一个Java程序

### 操作步骤

①右击电脑桌面创建一个的文本文件

②把文件的名字修改为"Test.java"

③用记事本打开这个文件,在文件中书写下面的代码.

~~~java
public class Test{

    public static void main(String[] args){
        System.out.println("Hello World");
    }
}
~~~

#### 解释

~~~
public: 
用来限制"类名"和"文件名"必须保持一致.

class Test: 
表示定义一个类,类名叫"Test".

public static void main(String[] args): 
这叫main方法,也叫主方法，是java程序的入口.程序就是从这开始运行的.

System.out.println("Hello World");
输出语句,将(" ")里面的内容Hello World在控制台（DOS窗口）打印出来.
~~~

### 运行该程序

④在Dos窗口中找到该文件（不会用DOS命令的话返回首页找DOS博文）

⑤编译并运行

~~~
打开DOS黑窗口输入：
cd Desktop
再输入：
javac Test.java
又输入：
java Test
~~~

#### 解释

~~~
cd Desktop这句代码表示:
我们告诉电脑：“兄弟，把路径给我转到桌面上，我待会要操作桌面上的文件。”
javac Test.java这句代码表示:
我们告诉电脑：“兄弟，你帮我把Test.java这个文件编译一下，我一会要运行它。” 然后电脑就会把Test.java这个文件编译一下，编译成功后会在桌面生成一个Test.class文件。
java Test:
我们告诉电脑：“好兄弟，你现在再帮我运行一下Test文件，把内容给我放出来看看。”
~~~

### 常见问题

~~~java
1).XXX不存在/找不到符号: 英文单词写错了(大小写字母也算)
2).已到达文件结尾: {}没有成对出现. 要么多了,要么少了
3).需要")": ()没有成对出现. 要么多了,要么少了		
4).非法字符XXX: 标点符号写成中文的标点符号了.
5).类XXX是公共的,应在名为XXX的文件中声明:	类名和文件名不一样
6).找不到文件XXX: cmd运行的路径错误/文件名写错了
7).XXX不是内部或外部命令: 环境变量配置的有问题/因为操作系统的问题导致环境变量失效了
8).编码XXX不可映射的字符: 编码设置错误(NotePad++没有配置)
9).需要class,interface或enum: 多个一个大括号}
~~~
