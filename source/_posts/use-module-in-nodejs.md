---
title: node(v8.5.0+)使用module
date: 2017-10-22 20:06:00
categories: Javascript
tags: node
---

## ** preface ** 

在 ES6 之前，社区制定了一些模块加载方案，最主要的有 `CommonJS` 和 `AMD` 两种。前者用于服务器，后者用于浏览器。ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，完全可以取代 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案。

ES6 模块的设计思想，是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。`CommonJS` 和 `AMD` 模块，都只能在运行时确定这些东西。比如，`CommonJS` 模块就是对象，输入时必须查找对象属性

node采用的模块方案是`CommonJS`。

module正是ES6引入的模块方案。node对ES6支持一直不错,不过并没有支持module,因为和node自身使用的`CommonJS`有所冲突,没拿出比较合适的解决方案。

直到最近的`v8.5.0`才开始支持module,到本文写作时,最新的版本是`v8.7.0`

***********

## ** 使用 **

`module`
Add support for ESM. This is currently behind the `--experimental-modules` flag and requires the .mjs extension. `node --experimental-modules index.mjs`

***********

目前使用这个功能,还需要将你的js文件后缀从`js`改为`mjs`

以下是示范

** one.mjs **

```javascript
let firstName = 'Michael';
let lastName = 'Jackson';
let year = 1958;

export {firstName, lastName, year};
```

*****************

** tow.mjs **

```javascript
import {firstName, lastName, year} from './one';


console.log(firstName);
console.log(lastName);
console.log(year);
```

`node --experimental-modules tow.mjs`

***********

** main.mjs **

```javascript
let tokenizer = (input)  =>{
    let current = 0;
    let tokens = [];
    console.log("666   " + input);
    console.log("1 " + input);
    console.log("2 " + input.length);
    while(current < input.length){
        let char = input[current];
        if(char === '{'){
            tokens.push({
                type: 'paren',
                value: '{',
            });
            current++;
            continue;
        }
        if(char === '}'){
            tokens.push({
                type: 'paren',
                value: '}',
            });
            current++;
            continue;
        }
        current++;
    }
};

export {tokenizer};

```

***********

** app.mjs **

```javascript
import {tokenizer}  from './main'

let input = "aaa";
tokenizer(input);
```
`node --experimental-modules app.mjs`


*********** 

## ** 参考 **

[Module 的语法](http://es6.ruanyifeng.com/#docs/module)
[CHANGELOG_V8.md](https://github.com/nodejs/node/blob/master/doc/changelogs/CHANGELOG_V8.md#8.7.0)
