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

