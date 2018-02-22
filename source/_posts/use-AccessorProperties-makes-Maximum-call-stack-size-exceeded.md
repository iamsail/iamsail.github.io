---
title: 使用访问器属性导致堆栈溢出
date: 2017-03-14 10:48:27
categories: Javascript
---

最近宅在图书馆老老实实刷红宝书。

撸访问器属性的时候,自己修改了部分代码,导致堆栈溢出。** 昨夜夜观天象,明白一二。**

以红宝书上的代码进行讲解
- 因为我是在node环境下跑的代码,所以alert的语句都改用了console.log

```
         var book = {
                _year: 2004,
                edition: 1
            };

        Object.defineProperty(book, "year",{
                get: function(){
                    return this.year;
                },
                set: function(newValue){

                    if(newValue > 2004){
                        this._year = newValue;
                        this.edition += newValue - 2004;
                    }
                }
            });

        book.year = 2005;
        console.log(book.edition);  //2
```
这段代码也就是书上的示例代码，是能够正常执行的,最后输出的结果是2

************************

然而我写代码的时候并不太规矩，常常改来改去的。现在把示例代码略作改动。
```
    var book = {
            _year: 2004,
            edition: 1
        };
```
修改为
```
    var book = {
            year: 2004,
            edition: 1
        };
```
且
```
    console.log(book.edition);
```
修改为
```
    console.log(book.year);
```
现在代码变为
```
        var book = {
            year: 2004,
            edition: 1
        };

        Object.defineProperty(book, "year",{
            get: function(){
                return this.year;
            },
            set: function(newValue){

                if(newValue > 2004){
                    this._year = newValue;
                    this.edition += newValue - 2004;
                }
            }
        });

        book.year = 2005;
        console.log(book.year);
```
******************************
跑一下
```
![stack-size-exceeded.png](/img/JavaScript/stack-size-exceeded.png)
```
图示的错误就是说** 堆栈溢出了 **。
纳闷...

******************************

解释:
- ** 在ECMAScript中有两种属性:数据属性和访问器属性 **

数据属性有4个描述其行为的特性,分别是
- ** Configurable **[表示是否能通过delete删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性。默认值为true]
- ** Enumerable **[表示能否用for-in循环返回。默认值为true]
- ** Writable **[表示能否修改属性的值。默认值为true]
- ** Value **(包含这个属性的数据值) [包含这个属性的数据值。读取属性值的时候从这个位置读，写入属性值的时候更新到这个位置，默认值为undefined。]

这个大家都是比较熟悉的。

而访问器属性不包含数据值,它们包含一对儿getter和setter函数(这两个函数不是必须的)
访问器属性的4个特性如下:

- ** Configurable **[表示是否能通过delete删除属性从而重新定义属性，能否修改属性的特性，能否把属性修改为访问器属性。默认值为true]
- ** Enumerable **[表示能否用for-in循环返回。默认值为true]
- ** Get **[在读取属性时调用的函数。默认值为Undefined]
- ** Set **[在写入属性时调用的函数。默认值为Undefined]

特别需要注意的是,** 访问器属性不能直接定义,必须使用Object.defineProperty()来定义。**

有了这些知识，再来分析下上面那段代码.
```
    var book = {
        year: 2004,
        edition: 1
    };
```
此处的year,是一个数据属性,并被赋值为2014。
```
    Object.defineProperty(book, "year",{
        get: function(){
            return this.year;
        },
        set: function(newValue){

            if(newValue > 2004){
                this._year = newValue;
                this.edition += newValue - 2004;
            }
        }
    });
```
在这儿我们又通过<code>Object.defineProperty()</code>定义了一个访问器属性,且同样命名为year。

** 此时之前定义的数据属性year已经over了，被新定义的访问器属性year覆盖掉了。**
```
    book.year = 2005;
    console.log(book.year);
```
** 最后两行代码分别触发了setter和getter函数。**

<code>book.year = 2005;</code>

写入属性,触发了setter。[第一段代码，也就是书上的示范代码，也是通过这一语句触发setter函数,修改了edition的值]

而导致堆栈溢出的就是下面这一句

<code>console.log(book.year);</code>

** 这一句的工作是读取访问器属性year,从而触发了getter函数。而getter函数的语句是<code>return this.year;</code>
这个语句又是读取访问器属性year,再次触发了getter函数。递归无限循环下去,所以堆栈溢出。**

****************************************

其实仔细些看图片中报错的信息,是可以看出多次调用了Object.get[as year]导致堆栈溢出了。

** 有时bug解决起来费时,是因为对某些基础的地方还没掌握牢固。**

** 又或许是许久不曾看过星空了... **

**************

<div width="100%" align="center"><div name="dashmain" id="dash-main-id-87905c" class="dash-main-2 87905c-3"></div></div>
<script type="text/javascript" charset="utf-8" src="http://www.dashangcloud.com/static/ds.js"></script>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>