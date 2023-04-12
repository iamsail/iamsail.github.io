---
title: Vue中平级组件通信
date: 2017-06-17 16:02:01
categories: Vue
---

### ** 总述 **

Vue中如何实现非父子关系的两个组件进行通信,在不太复杂的场景下,可以通过** 使用一个空的Vue实例作为中央事件总线 **

```
var bus = new Vue()

// 触发组件 A 中的事件
bus.$emit('id-selected', 1)

// 在组件 B 创建的钩子中监听事件
bus.$on('id-selected', function (id) {
  // ...
})

```
*********************
### ** 组件、总线代码 **

<span class="under0"> ** ./src/App.vue **</span>

```
<template>
  <div id="app">
    <firstChild></firstChild>
    <secondChild></secondChild>
  </div>
</template>

<script>
  import firstChild from './components/firstChild';
  import secondChild from './components/secondChild';
  export default {
    name: 'app',
    components:{
      firstChild,
      secondChild
    }
  }
</script>

<style lang="stylus" scoped>

</style>

```

<span class="under0">** ./src/assets/eventBus.js **</span>

```
import Vue from 'Vue'

export default new Vue;

```

<span class="under0">** ./src/components/firstChild.vue **</span>

```
<template>
    <div id="firstChild">
        <h2>firstChild组件</h2>
        <button @click="sendMsg">
            向组件传值
        </button>
    </div>
</template>

<script>
    import bus from '../assets/eventBus';
    export default{
        methods:{
            sendMsg:function(){
                bus.$emit("userDefinedEvent","this message is from firstChild");
            }
        }
    }
</script>

<style lang="stylus" scoped>

</style>


```

<span class="under0">** ./src/components/secondChild.vue **</span>

```
<template>
    <div id="secondChild">
        <h2>secondChild组件</h2>
        <p>从firstChild接收的字符串参数:{{msg}}</p>
    </div>
</template>

<script>
    import bus from '../assets/eventBus';
    export default{
       data(){
           return {
               msg: "默认值"
           }
       },
        mounted(){
            var self = this;
            bus.$on("userDefinedEvent",function(msg){
                self.msg = msg;
            });
        }
    }
</script>

<style lang="stylus" scoped>

</style>



```

******************

### ** 参考 **

- [Vue2.0组件之间通信](http://www.jianshu.com/p/d946bd7c26f4)

