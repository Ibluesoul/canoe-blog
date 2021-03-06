---
title: pygobject-tutorial-1
date: '2016-11-09T00:55:47+08:00'
tags:
  - python
  - gtk
categories:
  - Python
---
# 基础
这章将会介绍GTK+比较重要的几个方面
## 主循环和信号
就像大部分GUI库一样，GTK+使用了一种事件驱动的编程模型。当用户什么都没做，GTK+让主循环处于就绪状态并等待用户的输入。如果用户做了一些动作，比如鼠标事件，主循环就会被唤醒，然后将这个事件传递给GTK+程序。
<!--more-->
当部件收到一个事件，它们将会频繁的发出一个或者更多的信号，这些信号将会调用与之相绑定的函数。这样的函数通常被称作回调函数。当回调函数被调用时，你就可以进行一些操作了。比如说，你可能要弹出一个文件选择对话框当一个“打开”按钮被点击的之后。当回调函数执行完毕之后，GTK+将会返回到主循环然后等待用户再一次输入。

一个典型的例子：
```python
handler_id = widget.connect('event',callback,data)
```
首先，`widget`是一个之前以及创建好的widget实例。接着，我们来看看事件，每个部件都有它自己的事件。举个例子，如果你有一个按钮，那么你往往希望绑定它的点击事件。这样只要按钮被点击，你就能收到它所触发的信号。然后，参数`callback`代表者需要调用的回调函数的名字，它包含者将要运行的代码，当特定的信号产生之后。最后，`data`参数包含着任意你想要传递的数据，这个参数是一个可选参数，如果不需要可以省略。
该方法返回一个数值，标志着这个signal-callback对。当这个函数再也不会
