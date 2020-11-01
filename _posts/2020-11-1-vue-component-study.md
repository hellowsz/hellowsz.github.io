---
layout:     post
title:      "vue父作用域传值到子组件"
subtitle:   "vue的父作用域和子组件的传值思考"
date:       2020-11-01 16:35:00
author:     "wsz"
header-style: "text"
tags:
    - vue
---

<center>vue从父作用域传值给子组件</center> <br>
从父作用域将数据传到子组件，修改一下组件的定义，使之能够接受一个prop<br>
javascript
```javascript
Vue.component('todo-item', {
  // 这个 prop 名为 todo。
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
//创建一个vue实例并挂载
let app = new Vue({
        el:"#app-7",
        data:{
            groceryList: [
                { id: 0, text: '蔬菜' },
                { id: 1, text: '奶酪' },
                { id: 2, text: '随便其它什么人吃的东西' }
            ]
        }
    })
```

html
```html
<div id="app-7">
        <p>{{message}}</p>
        <ol>
            <todo-item v-for="item in groceryList" v-bind:todo="item" v-bind:key="item.id">
            </todo-item>
        </ol>
</div>
```
这个组件中的props类似于自己给组件定义了一个attribute，这个attribute叫做todo，组件其实很类似于自定义标签，给标签一些属性,prop给了组件能够调用的值，你只需要写好怎么取，再绑定一些事件就可以了。
