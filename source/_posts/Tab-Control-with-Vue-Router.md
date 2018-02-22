---
title: vue-router实现选项卡
date: 2017-07-10 16:02:01
categories: Vue
---

本文是对通过 `Vue+vue-router` 实现的选项卡记录

该demo使用的是单文件组件实现。demo去掉了多余的部分,使代码尽可能简单。

***********************

### ** 项目结构 **

![Tab-Control-with-Vue-Route](/img/Vue/Tab-Control-with-Vue-Route.png)


***********************

### ** 源代码 **

<span class="under0">main.js</span>


```JavaScript

import Vue from 'vue'
import App from './App.vue'
import router from './router'

Vue.config.productionTip = false

new Vue({
  el: '#app',
  router,
  template: '<App/>',
  components: { App }
})

```


<span class="under0">./router/index.js</span>

```JavaScript
import Vue from 'vue'
import Router from 'vue-router'

import header from '@/components/header'
import footer from '@/components/footer'

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/header',
      name: 'header',
      component: header
    },
    {
        path: '/footer',
        name: 'footer',
        component: footer
    }
  ]
})

```


<span class="under0">App.vue</span>

```HTML
<template>
  <div id="app">
      <h1>{{msg}}</h1>
      <router-link to="/header">/header</router-link>
      <router-link to="/footer">/footer</router-link>
      <router-view></router-view>
  </div>
</template>

```
```JavaScript
<script>
    export default{
        name: app,
        data () {
            return{
                msg: "hello world"
            }
        }
    }
</script>
```


<span class="under0">./components/header.vue</span>

```HTML
<template>
  <ul id="header">
    <li>{{msg[0]}}</li>
    <li>{{msg[1]}}</li>
    <li>{{msg[2]}}</li>
    <li>{{msg[3]}}</li>
  </ul>
</template>
```
```JavaScript
<script>
  export default{
    data(){
      return{
        msg:["HTML","CSS","JS","VUE"]
      }
    },
  }
</script>
```


```stylus
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
  li
    float  left
    list-style none
    font-size 18px
    margin-left  8px
</style>

```


<span class="under0">./components/footer.vue</span>

```HTML
<template>
    <ul id="footer">
        <li>{{msg[0]}}</li>
        <li>{{msg[1]}}</li>
        <li>{{msg[2]}}</li>
        <li>{{msg[3]}}</li>
    </ul>
</template>
```
```JavaScript
<script>
    export default{
        data(){
            return{
                msg:["1","2","3","4"]
            }
        },
    }
</script>
```
```stylus
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
    li
        float  left
        list-style none
        font-size 18px
        margin-left  8px
</style>
```
******************
### ** 演示 **

![Tab-Control-with-Vue-Route](/img/Vue/Tab-Control-with-Vue-Route.gif)

******************
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>
