---
title: 深入编码
date: 2021-2-15 10:58:45
categories: 代码人生
tags: [字符编码]
---

### Preface 

今天在微信看到这样一串代码

<span class="_img4">
![1.jpeg](/img/代码人生/encode-and-decode/1.jpeg)
</span>

```
\u53eb\u4f60\u7ffb\u8bd1\u4f60\u5c31\u7ffb\u8bd\uff0c\u4f60\u662f\u4e0d\u662f\u50bb\uff1f
```

```
\u6211\u662f\u4f60\u7238\u7238
```

这里涉及到了编码的知识，我初看之下，也不能确定是什么编码。经过一番搜索，整理出了本文。

**************

### 编码 

汉字转`Unicode`方法

```javascript
function toUnicodeFun(data){
  if(data == '' || typeof data == 'undefined') return '请输入汉字';
   var str =''; 
   for(var i=0;i<data.length;i++){
      str+="\\u"+data.charCodeAt(i).toString(16);
   }
   return str;
}

var resultUnicode = toUnicodeFun('中国'); // \u4e2d\u56fd
```


`Unicode`转化为汉字

```javascript
function toChineseWords(data){
    if(data == '' || typeof data == 'undefined') return '请输入十六进制unicode';
    data = data.split("\\u");
    var str ='';
    for(var i=0;i<data.length;i++){
        str+=String.fromCharCode(parseInt(data[i],16).toString(10));
    }
    return str;
}
var resultChineseWords = toChineseWords("\u4e2d\u56fd"); 
console.log(resultChineseWords);//中国
```

```javascript
var GB2312UnicodeConverter={
    ToUnicode:function(str){
       return escape(str).toLocaleLowerCase().replace(/%u/gi,'\\u');
    },
    ToGB2312:function(str){
       return unescape(str.replace(/\\u/gi,'%u'));
    }
};
var result = GB2312UnicodeConverter.ToUnicode('中国'); //\u4e2d\u56fd
var result2 = GB2312UnicodeConverter.ToUnicode(result); //%5cu4e2d%5cu56fd
```


汉字转`Unicode`码
```javascript
function toUnicode(s){ 
    return s.replace(/([\u4E00-\u9FA5]|[\uFE30-\uFFA0])/g,function(newStr){
        return "\\u" + newStr.charCodeAt(0).toString(16); 
    }); 
}
```


**************

### ** 参考链接 **

- [JS基础篇--JS之汉字与Unicode码的相互转化](https://segmentfault.com/a/1190000012030831)
- [JS Unicode编码和解码（6种方法）](http://c.biancheng.net/view/5602.html)
- [ifreesite](https://www.ifreesite.com/unicode/)
- [字符编码笔记：ASCII，Unicode 和 UTF-8](http://www.ruanyifeng.com/blog/2007/10/ascii_unicode_and_utf-8.html)
- [Unicode 和 UTF-8 有什么区别？](https://www.zhihu.com/question/23374078    )