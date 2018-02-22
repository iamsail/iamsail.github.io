---
title: is Palindrome
date: 2017-04-11 17:35:02
categories: [水题]
---
** 判断字符串是否回文 **
```
    #include <stdio.h>
    int main(int argc, char *argv[])
    {
    	char a[101],s[101];
    	int i,len,mid,next,top;

    			gets(a);  //读入一行字符串
    			len = strlen(a);  // 求字符串的长度
    		 	mid = len/2 - 1; // 求中点
    			top = 0;    //栈初始化
    			// mid 之前的字符依次入栈

    			for(i = 0; i <= mid; i++){
    				s[++top] = a[i];
    			}
    			if(len % 2 == 0){
    				next = mid + 1;

    			}else{
    				next = mid + 2;
    			}

    			// 开始匹配

    			for(i = next;i <= len - 1; i++){
    				if(a[i] != s[top])
    					break;
    				top--;
    			}

    			if(top == 0){
    				printf("YES");
    			}else{
    				printf("NO");
    			}
    	return 0;
    }
```
************************************

** 参考 **

- 《啊哈！算法》

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<script type="text/javascript" charset="utf-8" src="http://www.dashangcloud.com/static/ds.js"></script>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>