---
layout:     post
title:      "vue的动态参数的使用"
subtitle:   "vue动态参数验证时遇到的一些坑"
date:       2020-11-01 19:36:00
author:     "wsz"
header-style: text
tags:
    - vue
---
<center>vue动态参数使用的时候的一个小问题</center><br>
看到vue动态参数的时候，想起要验证一下，就试着搞了一下用a标签试了一下，具体问题如下<br>
```javascript
//JavaScript
let app = new Vue({
        el:"#app",
        data:{
            url:"http://www.baidu.com",
            aName:"href"
        },
    })
```

```html
//html
<div id="app">
    <a v-bind:[aName]=url>baidu</a>
</div>
```

最后的效果如下面所示
<div id="app">
    <a>baidu</a>
</div>
点击之后并没有跳转页面，因为vue中的动态参数会自动全部变成小写，这样vue实例中找不到一个aName，因为被改成了aname<hr>
当vue实例中的参数改成全小写之后
```javascript
//JavaScript
let app = new Vue({
        el:"#app",
        data:{
            url:"http://www.baidu.com",
            aname:"href"//这里的aname变成了全小写
        },
    })
```
```html
//html
<div id="app">
    <a v-bind:[aName]=url>baidu</a>
</div>
```
效果如下
<div id="app">
    <a href="http://www.baidu.com">baidu</a>
</div>
现在a标签有了href属性，并给a标签的href属性赋值data中的值，现在能够点击并跳转了。开始我以为是我使用的方法问题，查阅了开发者文档才发现是需要全部小写。
