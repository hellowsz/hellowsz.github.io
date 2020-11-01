---
layout:     post
title:      "浏览器的运行原理"
subtitle:   "Operating Principle Of Web Browser"
date:       2020-10-31 20:05:30
author:     "wsz"
header-style: text
tags:
    - 浏览器
---

浏览器的运行原理

# 浏览器三个结构
- 用户界面：我们浏览网页呈现出来的界面
- 浏览器引擎：里面有数据持久层，比如cookie，用于在用户界面和渲染引擎之间传递数据
- 渲染引擎(浏览器内核)：里面有请求网络的程序，js解析器，用于渲染用户请求的页面内容
# 浏览器进程
- 浏览器进程：控制除了标签页外的用户界面，比如前进后退按钮等。
- 网络进程：网络进程负责发起和接受网络请求。
- GPU进程：负责整个浏览器的界面渲染
- 插件进程：控制网站所使用的所有插件
- 渲染器进程：用于控制显示tab标签内的所有内容。
# 浏览器的工作流程：
- 当请求完毕，并收到响应且安全校验通过时，网络线程就通知UI线程
- UI线程收到通知后，创建一个渲染器进程(renderer thread)
- 浏览器进程通过IPC管道将数据传递给渲染器进程，正式进入渲染流程，渲染器的核心任务就是把html，css，js，image渲染成用户的交互页面
- 渲染器进程的主线程将html解析，构造DOM数据结构，html—>tokeniser->tree construction->DOM,如果在构造树的过程中遇到'<script>'标签，就会转而执行js
解析完成后，得到一个DOM tree，这时候只知道标签有哪些，但不知道他们具体长什么样子
- 主线程开始解析css，确定每个DOM节点的样式
- 知道标签内容，知道样式，但不知道具体在哪个位置，确定位置就是主线程开始遍历DOM tree和计算好的样式style tree来生成render tree，上面的每一个节点都记录了
DOM tree上的标签相对应的坐标和尺寸，但不是一一对应的，设置了display：none属性的标签不会出现在render tree上。在before伪类上游content的内容会在
render tree 上，不会在DOM tree上。
- 现在还需要知道以什么样的顺序绘制(paint),主线程遍历上一步得到的layout tree，创建绘制记录表(paint record)
- 现在所有的都确定了，轮到展示了，这种行为称为栅格化(rastering),新的方案叫做合成(compositing),主线程将之前的全部传给合成器线程，合成器线程按规则
分图层，传给把图层分为图块传给栅格线程，再传给合成器进程产生合成器帧，GPU渲染以后展示在页面上。