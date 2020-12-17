---
layout:     post
title:      "BetterSCroll使用遇到的问题"
subtitle:   "BetterSCroll"
date:       2020-12-17 18:59:00
author:     "wsz"
header-style: "text"
tags:
    - BetterScroll
---
# 问题
BetterScroll用起来更加顺滑，相比传统的在css中写`overflow：scroll`，BetterScroll只需要定义一些参数就能使用<br>
这次的使用场景是h5实现下拉刷新和上拉到底加载更多的效果，首先我是用`calc`将父容器高度计算出来，再给父容器定css中定一个`overflow：scroll`<br>
上述效果成功实现，但在使用bs的时候出现了问题，我在mounted中写上了初始化bs的代码，但刷新之后效果并没有出来，问题出在创建bs对象的时间上<br>
# 解决思路
1.先F12查看父容器和子元素的高度，父容器的高度大于或者等于子元素的话没有刷新效果<br>
2.父容器高度小于子元素高度，检查是否选中了父元素DOM，父元素DOM是否已经是一个BS对象了，可以打印出来看<br>
3.这里就是我使用遇到的问题了，我用Vue写的，子元素还没渲染出来，也就是说在初始化BS的时候子元素还没完全渲染出来，高度为0，父元素大于子元素
# 解决办法
找到问题后就简单了，`$nexttick()`，当父元素渲染完成以后，触发`$nexttick()`刷新初始化BS对象，这时候的bs对象中的子元素就是渲染完成后的子元素了
# 知识点
Vue中的`$nextTick`涉及到Vue中DOM的异步更新<br>
1.在Vue生命周期的`created()`钩子函数进行的DOM操作一定要放在`Vue.nextTick()`的回调函数中<br>
2.在数据变化后要执行的某个操作，而这个操作需要使用随数据改变而改变的DOM结构的时候，这个操作都应该放进Vue.nextTick()的回调函数中。
