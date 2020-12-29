---
layout:     post
title:      "区分是否是第一次进入该页面"
subtitle:   "Distinguish whether it is the first time to enter the page"
date:       2020-12-29 17:41:00
author:     "wsz"
header-style: "text"
tags:
    - JavaScript
    - Works
---
# 遇到的问题
做vue项目的时候需要将一个数据详情展示，该页面复用在三个功能上：新增一条数据，选中编辑一条数据，选中复制一条数据（可更改其中数据）
当编辑时，上面有几个输入框需要锁定不能编辑，当复制时，所有输入框可编辑，有两条数据是包含关系，先要查出第一个数据，才能查询其中包 
含的第二条数据，所以需要做成如果第一条数据清空，第二条数据也要相应清空。其中有一些老数据没有第一条数据，所以查询回来以后因为之前 
的逻辑，这里第二条数据就没展示了。
# 需要实现的效果
第一次进入可编辑页面，需要展示的是后端返回的数据，没有第一条数据也可以展示第二条数据，但你编辑第一条数据时，需要清空第二条数据
# 实现思路
vue开发是数据驱动，所有的逻辑都应该依靠数据，那么我们需要写一个第二条数据的清空逻辑，当页面第一次渲染出来时，不进入这个清空逻辑, 
但当修改第一条时，进入清空逻辑清空第二条，我们先给一个标识数据`isinit = true`，vue渲染的时候这个`isinit`的值为`true`，此时不触发清空 
当执行第一条数据改变时，触发函数，将`isinit`改为`false`，这时候进入清空逻辑，清空第二条数据
```javascript
data(){
    return{
        isinit:true
    }
}
methods:{
    inputFirstChange(){
        this.isinit = false
    }
    clearSecondInput(secondValue){
        secondValue = []
    }
}
```
