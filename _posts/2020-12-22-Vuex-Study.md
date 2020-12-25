---
layout:     post
title:      "Vuex学习总结"
subtitle:   "Learning summary for Vuex"
date:       2020-12-22 09:31:00
author:     "wsz"
header-style: "text"
tags:
    - vue
    - Vuex
---
# 什么是Vuex
Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。
<br>
<br>

# 使用场景
如果不打算开发大型单页应用，就最好不用vuex，一个简单的Store模式就足够了，但是如果构建中大型的单页应用，就要考虑更好的在组件外部管理状态VUex是不错的选择
# 组成
- <strong>State</strong>
- <strong>Getter</strong>
- <strong>Mutation</strong>
- <strong>Action</strong>
- <strong>module</strong>
### State
vueX使用state来存储应用中需要共享的状态，也就是驱动应用的数据源，我把它理解成vue中公共的data，能够被所有的组件使用。
### Getter
类似于Vue中的计算属性，也可以理解为store的计算属性，getter的返回值会根据他的依赖被缓存起来，只有当依赖值发生改变才会被重新计算<br>
- <strong>通过属性访问</strong>
```javascript
//Getterh会暴露为store.getter对象，可以以属性的形式访问
store.getters.xxx
//Getter方法也接受state和其他getters作为前两个参数
getters:{
    doneTodosCount：(state,getters) =>{
        return getters.doneTodos.length
    }
}
```
- <strong>通过方法访问</strong>
```javascript
//通过让getter返回一个函数，来实现给getter传参，在对store里的数据进行查询时非常有用
getters:{
    getTodoById:(state) => (id) => {
        return state.todos.find(todo => todo.id === id)
    }
//注意：getter在通过方法访问时，每次都会调用方法，而不是缓存结果
}
```
### Mutation
更改Vuex的store中的state的唯一办法就是提交Mutation，前面的State，getter都只是状态本身，Mutation才是状态改变的执行<br>
Vuex中的mutation类似于事件，每个mutation都有一个字符串的事件类型（type）和一个回调函数（handler）这个回调函数就是改变状态的地方
```javascript
this.$store.commit("MutationName",state)
```
### Action
异步修改状态，就需要Action
