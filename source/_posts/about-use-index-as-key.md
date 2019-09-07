---
title: 关于使用index作为key的问题
date: 2019-08-10 12:01:45
categories: react
---

### ** Preface **

这两天和朋友小小的讨论了下关于index作为key的问题,虽然知道不建议使用index作为key，应该使用id。之前还没有仔细了解过,本文做些记录。

***********************

### ** 使用index作为key引起的性能问题 **

在使用vue或者react开发一些前端应用的时候,在一些列表或者table场景下,有的时候会使用index来作为key

```javascript
    array.forEach(item, index => {
        key: index
    })
```

这种使用index作为key的方式其实是存在一些问题的,比如一个列表中的数据最初是[1, 2, 3, 4]

#### ** 使用index作为key **

| 数据 | key | index |
| ------ | ------ | ------ |
| 1 | 0 | 0 |
| 2 | 1 | 1 |
| 3 | 2 | 2 |
| 4 | 3 | 3 |

数据打乱过后,比如[4, 3, 2, 1] 

| 数据 | key | index |
| ------ | ------ | ------ |
| 4 | 3 | 3 |
| 3 | 2 | 2 |
| 2 | 1 | 1 |
| 1 | 0 | 0 |

这样元素和key的对应关系变了,就会导致重新渲染,对性能会造成一定的影响。

#### ** 使用id作为key **

| 数据 | key | id |
| ------ | ------ | ------ |
| 1 | x01 | x01 |
| 2 | x99 | x99 |
| 3 | 66x | 66x |
| 4 | s768 | s768 |

数据顺序打乱过后 

| 数据 | key | id |
| ------ | ------ | ------ |
| 4 | s768 | s768 |
| 3 | 66x | 66x |
| 2 | x99 | x99 |
| 1 | x01 | x01 |

元素和key的对应关系是没有发生变化的, 不会重新渲染。

上面提到的还算是比较好的情况,只是影响性能上的问题。

************************

### ** 使用index作为key引起的bug **

倘若进行一些删除或者增加操作时,甚至会导致bug。
比如以下的场景,这里我提供了codepen链接,可以体验下[使用index作为key引起的bug](https://codepen.io/iamsail/pen/wVYgQr)

```javascript
class HelloWorld extends React.Component {
  constructor() {
    super();
     this.state = {
       date: [1,2,4,5],
       xxx: [{
         id: 98,
         name: 'apple'
       }, {
         id: 1997,
         name: 'box'
       }, {
         id: 'fff',
         name: 'card'
       }, {
         id: 4,
         name: 'dog'
       }]
     };
  }
  
  handleClick = () => {
    this.setState({
      xxx: this.state.xxx.filter((val, index) => {
        // 需要return
        return val.name !== 'box'
      })
    })
  }
  
  render () {
    return (
      <div>
        <select>
          {this.state.xxx.map((item, index) => {
             return <option value ={item.name} key={index}>{item.name}</option>
          })}
        </select>
        <button  onClick={this.handleClick}>
          点我
        </button>
      </div>
    )
  }
}

class App extends React.Component {
  render () {
    return (
      <div>
        <HelloWorld />
      </div>
    )
  }
}

ReactDOM.render(
  <App />,
  document.getElementById('app')
)
```
渲染出来如下图
![1.jpeg](/img/react/about-use-index-as-key/1.jpeg)

首先选中第三项, 也就是选中`card`项, 接下来点击按钮会删除第二项,也就是`box`, 这个时候就变成最初的第四项`dog`被选中了。
通过表格来阐述下:

** 删除之前 **

| key | id | index | name |
| ------ | ------ | ------ |
| 0 | 98 | 0 | apple |
| 1 | 1997 | 1 | box |
| 2 | fff | 2 | card |
| 3 | 4 | 3 | dog |

** 删除之后 **

| key | id | index | name |
| ------ | ------ | ------ |
| 0 | 98 | 0 | apple |
| 1 | fff | 1 | card |
| 2 | 4 | 2 | dog |

使用的index作为key,因为最初选择的是`card`,key是2,删除过后,key为2的元素是`dog`。

**********************
### ** 解决方案 **

在前面我举了两个例子来说明index作为key存在的一些问题。所以我们应该避免使用index作为key。

1.倘若后端有返回id,可以使用id做为key
2.通过一个全局变量比如 
```javascript
let counter = 0;
++counter;
```
将自增后的`counter`

3.使用`shortid`,这个npm库,会通过算法生成id
```
const shortid = require('shortid');
console.log(shortid.generate());
// PPBqWA9
```
**********************

### ** 参考链接 **

- [React之key详解](https://www.cnblogs.com/wonyun/p/6743988.html)
- [vue中使用v-for时为什么不能用index作为key？](https://segmentfault.com/a/1190000019961419)
- [shortid](https://www.npmjs.com/package/shortid)
- [在React中index作为key是反模式的](https://juejin.im/post/5aed94cbf265da0b934831d6)
- [React列表增删时使用index当作key引发的问题及原因](http://carolunar.com/2018/08/05/why-should-not-we-use-indexes-for-keys-in-react-list/)
- [Controlled and uncontrolled form inputs in React don't have to be complicated](https://goshakkk.name/controlled-vs-uncontrolled-inputs-react/)
- [非受控组件](https://zh-hans.reactjs.org/docs/uncontrolled-components.html)
