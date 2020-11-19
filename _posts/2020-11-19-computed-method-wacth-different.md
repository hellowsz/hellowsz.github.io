---
layout:     post
title:      "computed，method和watch"
subtitle:   "computed，method和watch的区别"
date:       2020-11-19 13:08:00
author:     "wsz"
header-style: "text"
tags:
    - vue
---
# computed
`computed`属性特点：<br>
1.`computed`带有缓存功能;对于任何复杂逻辑，你都应当使用`计算属性`<br>
2.`computed`定义的方法我们是以属性访问的形式去调用的，就像调用`data`中的数据一样<br>
3.`computed`是依赖于`data`中的数据，当你申明了以后，他们之间建立依赖，`data`中的数据变化使`computed`中返回值变化<br>
4.尽量用`computed`来监视数据的变化<br>
5.数据量大，需要缓存的时候用`computed`<br>
# methods
`methods`属性的特点<br>
1.`methods`不带缓存功能，每次都要重新加载<br>
2.使用的时候不能像`data`那样使用，需要`{{ functionName() }}`加上()<br>
3.`methods`是函数调用
# watch
`wacth`属性的特点：<br>
1.一种更通的观察和响应`Vue` 实例上的数据变动的方式；<br>
2.用`watch`没有`computed`“自动”，手动设置会使代码变复杂；<br>
3.更好的办法是使用`computed`属性，而不是命令是的watch回调。<br>

