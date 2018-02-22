---
title: 括号匹配
date: 2017-04-14 00:03:38
categories: 水题
---
** 对括号匹配有着特别的感情。在一年多前,初学C++时，就遇见过此题。**

** 思想: 左括号进栈,右括号出栈。**

************

代码中用到了C++,STL中的stack。当然也可以自己封装。

简要介绍下stack中的各个方法

<code>s.push(x)</code>

** 无返回值，将元素x压栈 **

<code>s.pop()</code>

** 退栈，无返回值 **

<code>s.top()</code>

** 取栈顶元素，返回栈顶元素 **

<code>s.empty()</code>

** 判断栈是否为空，如果是空，返回1，否则返回0 **

<code>s.size()</code>

** 返回栈中元素的个数 **

***************************

** 实现代码 **

```
        #include <iostream>
        #include <stack>
        using namespace std;

        int main(int argc, char *argv[])
        {
        	stack<char> s;
        	char a[101];
        	gets(a);
        	int flag=0,i,len =strlen(a); // 若flag为1，则不匹配
        	for(i=0;i < len; i++){

        		switch(a[i]){
        			case '(':
        			case '[':
        			case '{': s.push(a[i]); break;
        			case ')':{
        						if(s.top() != '('){
        								flag = 1;

        						} else{
        							s.pop();
        						}
        					}
        					break;
        			case ']':{
        						if(s.top() != '['){
        								flag = 1;

        						} else{
        								s.pop();
        						}
        					}
        					break;
        			case '}':{
        						if(s.top() != '{'){
        								flag = 1;

        						} else{
        								s.pop();
        						}
        					}
        					break;
        			default:break;
        		}
        		if(flag)
        			break;
        	}

        	if(!flag && s.empty()){
        		cout<<"括号匹配成功"<<endl;
        	}else{
        		cout<<"括号匹配失败"<<endl;
        	}
        	return 0;
        }
```

************************************

** 参考 **

- [ c++ STL中栈stack的用法](http://blog.csdn.net/sunquana/article/details/13095075)

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<script type="text/javascript" charset="utf-8" src="http://www.dashangcloud.com/static/ds.js"></script>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>