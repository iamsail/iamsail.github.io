---
title: JS中的数字类型
date: 2020-01-22 11:06:01
categories: Javascript
---
### ** Preface **
在JavaScript中，一个数字过大，会导致数字不准确。比如在浏览器中输入下图中的数字，输出的却是另外一个数字。
![1.png](/img/JavaScript/number-type-in-javascript/1.png)

这是因为超出了JS中的数字的最大类型。不在双精度浮点数的取值范围内。 超出这个范围，JavaScript 中的数字不再安全了。
本文会对JS中的数字类型做些记录。
**********************

### ** IEEE 754 **

IEEE二进制浮点数算术标准（IEEE 754）是20世纪80年代以来最广泛使用的浮点数运算标准，为许多CPU与浮点运算器所采用。IEEE 754规定了四种表示浮点数值的方式：单精确度（32位）、双精确度（64位）、延伸单精确度（43比特以上，很少使用）与延伸双精确度（79比特以上，通常以80位实现）。

![2.png](/img/JavaScript/number-type-in-javascript/2.png)

#### ** 浮点数剖析 **
一个浮点数 (Value) 的表示其实可以这样表示：

$value = sign \times exponent \times fraction$

也就是浮点数的实际值，等于符号位`（sign bit）`乘以指数偏移值`(exponent bias)`再乘以分数值`(fraction)`。

以下内文是`IEEE 754`对浮点数格式的描述。

#### ** 32位单精度 **

单精度二进制小数，使用32个比特存储

| S | Exp | Fraction|
| ----- | ----- | ----- |
| 1 | 8 |	23位长 |
| 31 |	30至23 偏正值（实际的指数大小+127） |  22至0位编号（从右边开始为0） |

S为符号位，Exp为指数字，Fraction为有效数字。 指数部分即使用所谓的偏正值形式表示，偏正值为实际的指数大小与一个固定值（32位的情况是127）的和。采用这种方式表示的目的是简化比较。因为，指数的值可能为正也可能为负，如果采用补码表示的话，全体符号位S和Exp自身的符号位将导致不能简单的进行大小比较。正因为如此，指数部分通常采用一个无符号的正数值存储。单精度的指数部分是−126～+127加上偏移值127，指数值的大小从1～254（0和255是特殊值）。浮点小数计算时，指数值减去偏正值将是实际的指数大小。

#### ** 64位双精度 **

双精度二进制小数，使用64个比特存储。


| S | Exp | Fraction|
| ----- | ----- | ----- |
|1 | 11 | 52位长 | 
| 63 | 62至52 偏正值（实际的指数大小+1023）| 51至0位编号（从右边开始为0）|

S为符号位，Exp为指数字，Fraction为有效数字。指数部分即使用所谓的偏正值形式表示，偏正值为实际的指数大小与一个固定值（64位的情况是1023）的和。采用这种方式表示的目的是简化比较。因为，指数的值可能为正也可能为负，如果采用补码表示的话，全体符号位S和Exp自身的符号位将导致不能简单的进行大小比较。正因为如此，指数部分通常采用一个无符号的正数值存储。双精度的指数部分是−1022～+1023加上1023，指数值的大小从1～2046（0（2进位全为0）和2047（2进位全为1）是特殊值）。浮点小数计算时，指数值减去偏正值将是实际的指数大小。


**********************

### ** 数字类型 **
根据 `ECMAScript` 标准，`JavaScript` 中只有一种数字类型：基于 `IEEE 754` 标准的双精度 64 位二进制格式的值（$-2^{53} - 1$   到 $2^{53} - 1$）。它并没有为整数给出一种特定的类型。除了能够表示浮点数外，还有一些带符号的值：`+Infinity`，`-Infinity` 和 NaN (非数值，Not-a-Number)。

要检查值是否大于或小于 `+/-Infinity`，你可以使用常量 `Number.MAX_VALUE` 和 `Number.MIN_VALUE`。另外在 `ECMAScript 6` 中，你也可以通过 `Number.isSafeInteger()` 方法还有 `Number.MAX_SAFE_INTEGER` 和 `Number.MIN_SAFE_INTEGER` 来检查值是否在双精度浮点数的取值范围内。 超出这个范围，`JavaScript` 中的数字不再安全了，也就是只有 `second mathematical interger` 可以在 `JavaScript` 数字类型中正确表现。

数字类型中只有一个整数有两种表示方法： 0 可表示为 -0 和 +0（"0" 是 +0 的简写）。 在实践中，这也几乎没有影响。 例如 +0 === -0 为真。 但是，你可能要注意除以0的时候：
```
42 / +0; // Infinity
42 / -0; // -Infinity
```
尽管一个数字常常仅代表它本身的值，但JavaScript提供了一些位运算符。 这些位运算符和一个单一数字通过位操作可以用来表现一些布尔值。然而自从 `JavaScript` 提供其他的方式来表示一组布尔值（如一个布尔值数组或一个布尔值分配给命名属性的对象）后，这种方式通常被认为是不好的。位操作也容易使代码难以阅读，理解和维护， 在一些非常受限的情况下，可能需要用到这些技术，比如试图应付本地存储的存储限制。 位操作只应该是用来优化尺寸的最后选择。

#### ** Number.MAX_SAFE_INTEGER  **

`MAX_SAFE_INTEGER` 是一个值为 `9007199254740991的常量`。因为`Javascript`的数字存储使用了`IEEE 754`中规定的双精度浮点数数据类型，而这一数据类型能够安全存储 $-2^{53} - 1$  到 $2^{53} - 1$ 之间的数值（包含边界值）。

这里安全存储的意思是指能够准确区分两个不相同的值，例如 `Number.MAX_SAFE_INTEGER + 1 === Number.MAX_SAFE_INTEGER + 2` 将得到 true的结果，而这在数学上是错误的，参考`Number.isSafeInteger()`获取更多信息.

由于 `MAX_SAFE_INTEGER` 是`Number`的一个静态属性，所以你不用自己动手为Number对象创建`Number.MAX_SAFE_INTEGER`这一属性，就可以直接使用它。

**********************

### ** BigInt 类型 **
`BigInt`类型是 `JavaScript` 中的一个基础的数值类型，可以用任意精度表示整数。使用 BigInt，您可以安全地存储和操作大整数，甚至可以超过数字的安全整数限制。BigInt是通过在整数末尾附加 n 或调用构造函数来创建的。

通过使用常量`Number.MAX_SAFE_INTEGER`，您可以获得可以用数字递增的最安全的值。通过引入 BigInt，您可以操作超过Number.MAX_SAFE_INTEGER的数字。您可以在下面的示例中观察到这一点，其中递增`Number.MAX_SAFE_INTEGER`会返回预期的结果:

```
const x = 2n ** 53n;
9007199254740992n
const y = x + 1n; 
9007199254740993n
```
可以对BigInt使用运算符+、*、-、**和%，就像对数字一样。BigInt 严格来说并不等于一个数字，但它是松散的。

在将BigInt转换为Boolean时，它的行为类似于一个数字：if、||、&&、Boolean 和!。

BigInt不能与数字互换操作。否则，将抛出TypeError。

**********************

### ** 参考链接 **

[IEEE 754](https://zh.wikipedia.org/wiki/IEEE_754)
[JavaScript 数据类型和数据结构](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures)
[Number.MAX_SAFE_INTEGER](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER)
[JavaScript 关于 IEEE 754 双精度浮点数的实现](https://blog.windstone.cc/front-end/js/data-structure/number/js-number-implementation.html#javascript-%E5%85%B3%E4%BA%8E-ieee-754-%E5%8F%8C%E7%B2%BE%E5%BA%A6%E6%B5%AE%E7%82%B9%E6%95%B0%E7%9A%84%E5%AE%9E%E7%8E%B0)
[number-precision](https://github.com/nefe/number-precision)
[前端应该知道的JavaScript浮点数和大数的原理](https://zhuanlan.zhihu.com/p/66949640)
[JavaScript 浮点数陷阱及解法 #9](https://github.com/camsong/blog/issues/9)

