---
title: 初学ESLint
date: 2017-08-01 15:56:00
categories: Javascript
tags: ESLint
---

### ** 前面 **

<span class="under0"> ** 为了能够写出更优雅的代码,更好的拥抱社区,开始在实际项目中使用ESLint。** </span>

本文是初学的记录,仅作参考。

***********

### ** ESLint **

#### ** 介绍 **

ESLint最初是由Nicholas C. Zakas ( JavaScript 红宝书 作者)于2013年6月创建的开源项目。它的目标是提供一个插件化的javascript代码检测工具。

ESLint 的初衷是为了让程序员可以创建自己的检测规则。ESLint 的所有规则都被设计成可插入的。ESLint 的默认规则与其他的插件并没有什么区别，规则本身和测试可以依赖于同样的模式。为了便于人们使用，ESLint 内置了一些规则，当然，你可以在使用过程中自定义规则。

每条规则

- 各自独立
- 可以开启或关闭（没有什么可以被认为“太重要所以不能关闭”）
- 可以将结果设置成警告或者错误

另外

- ESLint 并不推荐任何编码风格，规则是自由的
- 所有内置规则都是泛化的

#### ** 安装 **

```javascript
### yarn 全局
yarn add -g eslint
```
#### ** 初始化(配置文件)**

```javascript
eslint --init

## 生成 .eslintrc 文件
```

#### ** 使用 **
```javascript
eslint yourfile.js
```

以上是使用的yarn安装,这里我介绍下npm的全局安装和局部安装姿势

#### ** npm **
```javascript
## 局部

npm install eslint --save-dev

./node_modules/.bin/eslint --init

./node_modules/.bin/eslint yourfile.js

## 全局

npm install -g eslint

eslint --init

eslint yourfile.js

```
**********
### ** 配置 **

可以通过以下三种方式配置 ESLint:

- 使用 `.eslintrc` 文件（支持 JSON 和 YAML 两种语法）；
- 在 `package.json` 中添加 `eslintConfig` 配置块；
- 直接在代码文件中定义。

#### ** `.eslintrc` 文件示例 **

```javascript
{
  "env": {
    "browser": true,
    "commonjs": true,
    "es6": true
    
  },
  "globals": {
    "document": true,
    "navigator": true,
    "window": true,
    "angular":true //添加项目所需没有申明的全局变量
  },
  "rules": {
    "camelcase": 2,
    "curly": 2,
    "brace-style": [2, "1tbs"],
    "quotes": [2, "single"],
    "semi": [2, "always"],
    "space-in-brackets": [2, "never"],
    "space-infix-ops": 2,
  }
}
```

`env:`你的脚本将要运行在什么环境中
`globals:`额外的全局变量

`rules:`开启规则和发生错误时报告的等级

规则的错误等级有三种：
0或'off'：关闭规则。
1或'warn'：打开规则，并且作为一个警告（并不会导致检查不通过）。
2或'error'：打开规则，并且作为一个错误 (退出码为1，检查不通过)。

参数说明：
参数1 ： 错误等级 
参数2 ： 处理方式

更多[Rules](http://eslint.cn/docs/rules/)


#### ** `package.json `示例 **
```javascript
{
  "name": "mypackage",
  "version": "0.0.1",
  "eslintConfig": {
    "env": {
      "browser": true,
      "node": true
    }
  }
}
```

#### ** 文件内配置 **

代码文件内配置的规则会覆盖配置文件里的规则。

禁用 ESLint：
```javascript
/* eslint-disable */
var obj = { key: 'value', }; // I don't care about IE8  
/* eslint-enable */
```

禁用一条规则：
```javascript
/*eslint-disable no-alert */
alert('doing awful things');  
/* eslint-enable no-alert */
```

调整规则：

```javascript
/* eslint no-comma-dangle:1 */
// Make this just a warning, not an error
var obj = { key: 'value', }  
```
### ** 其它 **

检查且修复

```javascript
eslint xxx.js --fix
```
***********

### ** 尾声 **
 
本文只是对ESLint的粗浅介绍,或许在使用一段时间后,会对本文做修改、补充,有或者另写一篇博文介绍心得。

***********

### ** 参考 **
[eslint](https://github.com/eslint/eslint)
[eslint-cn](http://eslint.cn/)
[利用ESLint检查代码质量](https://cnodejs.org/topic/57c68052b4a3bca66bbddbdd)
[ESLint_docs](https://github.com/Jocs/ESLint_docs)
[ESLint 使用入门](https://csspod.com/getting-started-with-eslint/)
[ESLint深入使用](http://blog.csdn.net/xueboren001/article/details/53389221)
[Eslint 从入门到放弃](http://blog.csdn.net/walid1992/article/details/54633760)


