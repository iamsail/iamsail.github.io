---
title: JavaScript获取页面url参数
date: 2020-01-26 21:33:45
categories: Javascript
---

### ** Preface **

获取页面url的参数是一个很常见的需求，我也遇到过了很多次了。本文做下记录。
当然已经有了一个开源库做了相关的工作[query-string](https://github.com/sindresorhus/query-string)
*********************

### ** URLSearchParams **

`URL()` 构造函数返回一个新创建的 `URL` 对象，表示由一组参数定义的 `URL`。
如果给定的基本 URL 或生成的 URL 不是有效的 URL 链接，则会抛出一个类型为 SYNTAX_ERROR 的 DOMException。

在`stackoverflow`上看到了一个方法，利用[URL()](https://developer.mozilla.org/zh-CN/docs/Web/API/URL/URL)。
```
var url_string = "http://www.example.com/t.html?a=1&b=3&c=m2-m3-m4-m5"; //window.location.href
var url = new URL(url_string);
var c = url.searchParams.get("c");

# console.log(c);
"m2-m3-m4-m5"
```

如果是旧的浏览器不支持的话
```javascript
function parse_query_string(query) {
  var vars = query.split("&");
  var query_string = {};
  for (var i = 0; i < vars.length; i++) {
    var pair = vars[i].split("=");
    var key = decodeURIComponent(pair[0]);
    var value = decodeURIComponent(pair[1]);
    // If first entry with this name
    if (typeof query_string[key] === "undefined") {
      query_string[key] = decodeURIComponent(value);
      // If second entry with this name
    } else if (typeof query_string[key] === "string") {
      var arr = [query_string[key], decodeURIComponent(value)];
      query_string[key] = arr;
      // If third or later entry with this name
    } else {
      query_string[key].push(decodeURIComponent(value));
    }
  }
  return query_string;
}

var query_string = "a=1&b=3&c=m2-m3-m4-m5";
var parsed_qs = parse_query_string(query_string);
console.log(parsed_qs.c);

var query = window.location.search.substring(1);
var qs = parse_query_string(query);
```

*********************

### ** 正则法 **

```javascript
function GetQueryString(name)
{
     var reg = new RegExp("(^|&)"+ name +"=([^&]*)(&|$)");
     var r = window.location.search.substr(1).match(reg);
     if(r!=null)return  unescape(r[2]); return null;
}
 
// 调用方法
alert(GetQueryString("参数名1"));
alert(GetQueryString("参数名2"));

```

```javascript
function gup( name, url ) {
    if (!url) url = location.href;
    name = name.replace(/[\[]/,"\\\[").replace(/[\]]/,"\\\]");
    var regexS = "[\\?&]"+name+"=([^&#]*)";
    var regex = new RegExp( regexS );
    var results = regex.exec( url );
    return results == null ? null : results[1];
}
gup('q', 'hxxp://example.com/?q=abc')
```

*********************

### ** 参考链接 **

[How to get the value from the GET parameters?](https://stackoverflow.com/questions/979975/how-to-get-the-value-from-the-get-parameters)
[decodeURIComponent()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/decodeURIComponent)
[encodeURIComponent()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent)