---
title: Vue中父子组件通信
date: 2017-06-14 15:05:30
categories: Vue
---
### ** 添加stylus-loader **

```
npm install stylus-loader css-loader style-loader --save-dev
```
******************

### ** 父子组件代码 **

<span class="under0">** ./src/App.vue **<span/>

```
<template>
  <div id="app">
    <child v-bind:message="parentMsg" v-on:listenToChildEvent="showMsgFromChild"></child>
  </div>
</template>

<script>
  import child from './components/Child'
  export default {
    name: 'app',
    data(){
      return{
        parentMsg:"hello,child"
      }
    },
    methods:{
      showMsgFromChild:function(data){
        console.log(data);
      }
    },
    components:{
      child
    }
  }
</script>

<style lang="stylus" scoped>
div
  font-size 500px
  color green
</style>


```

<span class="under0">** ./src/components/Child.vue **</span>

```
<template>
    <div id="app">
        <h2>child子组件部分</h2>
        <p>{{message}}</p>
        <button v-on:click="sendMsgToParent">向父组件传值</button>
    </div>
</template>

<script>
    export default {
        props:["message"],
        methods:{
            sendMsgToParent: function () {
                this.$emit("listenToChildEvent","this message is from child");
            }
        }
    }
</script>

<style>

</style>

```
******************

### ** 参考 **

- [Vue2.0子父组件通信](http://www.jianshu.com/p/2670ca096cf8)

