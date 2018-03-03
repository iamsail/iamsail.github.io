---
title: hexo站内搜索
date: 2017-08-16 22:09:17
categories: 代码人生
tags: hexo&&博客记录
---

### ** 前言 **

今天花了些时间为博客增加了站内搜索功能,并且对主题进行了较大幅度的修改。

![1.png](/img/codelife/hexo-site-search/1.png)

大致看上去就是这样的,当然,因为是截图,看不到动画效果。

本文做些记录。

**********

### ** 搜索 **

之前[肖高阳](https://blog.xgy666.cn/)为我推荐了[hexo-generator-search](https://github.com/PaicHyperionDev/hexo-generator-search).
他的hexo所用的主题是Next,该主题是自带了这个插件的,只需要改下配置文件即可。

也就是说倘若你的主题没有集成该插件,需要自己安装配置。

#### ** Install **

```
### npm
npm install hexo-generator-search --save

### yarn
yarn add hexo-generator-search  --dev
```
#### ** Options **

修改根目录下的_config.yml

```
search:
  path: search.xml
  field: post
  
###
path - 指定生成的索引数据的文件名。默认为 search.xml 。
field - 指定索引数据的生成范围。可选值包括：
    post - 只生成博客文章（post）的索引（默认）；
    page - 只生成其他页面（page）的索引；
    all - 生成所有文章和页面的索引。  
```
如果以上步骤都正确的话,会生成一个`search.xml`文件。
通过你的预览地址/search.xml即可以预览

#### ** 搜索框 **

```
<div id="site_search">
  <input type="text" id="local-search-input" name="q" results="0"
   placeholder="search my blog..." class="form-control"/>
  <div id="local-search-result"></div>
</div>
```
将搜索框放置在你需要插入的地方

#### ** 搜索函数 **

```javascript
var searchFunc = function(path, search_id, content_id) {
    'use strict';
    $.ajax({
        url: path,
        dataType: "xml",
        success: function( xmlResponse ) {
            // get the contents from search data
            var datas = $( "entry", xmlResponse ).map(function() {
                return {
                    title: $( "title", this ).text(),
                    content: $("content",this).text(),
                    url: $( "url" , this).text()
                };
            }).get();
            var $input = document.getElementById(search_id);
            var $resultContent = document.getElementById(content_id);
            $input.addEventListener('input', function(){
                var str='<ul class=\"search-result-list\">';
                var keywords = this.value.trim().toLowerCase().split(/[\s\-]+/);
                $resultContent.innerHTML = "";
                if (this.value.trim().length <= 0) {
                    return;
                }
                // perform local searching
                datas.forEach(function(data) {
                    var isMatch = true;
                    var content_index = [];
                    var data_title = data.title.trim().toLowerCase();
                    var data_content = data.content.trim().replace(/<[^>]+>/g,"").toLowerCase();
                    var data_url = data.url;
                    var index_title = -1;
                    var index_content = -1;
                    var first_occur = -1;
                    // only match artiles with not empty titles and contents
                    if(data_title != '' && data_content != '') {
                        keywords.forEach(function(keyword, i) {
                            index_title = data_title.indexOf(keyword);
                            index_content = data_content.indexOf(keyword);
                            if( index_title < 0 && index_content < 0 ){
                                isMatch = false;
                            } else {
                                if (index_content < 0) {
                                    index_content = 0;
                                }
                                if (i == 0) {
                                    first_occur = index_content;
                                }
                            }
                        });
                    }
                    // show search results
                    if (isMatch) {
                        str += "<li><a href='"+ data_url +"' class='search-result-title'>"+ data_title +"</a>";
                        var content = data.content.trim().replace(/<[^>]+>/g,"");
                        if (first_occur >= 0) {
                            // cut out 100 characters
                            var start = first_occur - 20;
                            var end = first_occur + 80;
                            if(start < 0){
                                start = 0;
                            }
                            if(start == 0){
                                end = 100;
                            }
                            if(end > content.length){
                                end = content.length;
                            }
                            var match_content = content.substr(start, end);
                            // highlight all keywords
                            keywords.forEach(function(keyword){
                                var regS = new RegExp(keyword, "gi");
                                match_content = match_content.replace(regS, "<em class=\"search-keyword\">"+keyword+"</em>");
                            });

                            str += "<p class=\"search-result\">" + match_content +"...</p>"
                        }
                        str += "</li>";
                    }
                });
                str += "</ul>";
                $resultContent.innerHTML = str;
            });
        }
    });
};

var path = "<%= config.root %>" + "search.xml";
searchFunc(path, 'local-search-input', 'local-search-result');

```
**********************

以下是于18年3月3日对搜索函数的更新。今天发现了博客的搜索结果点击还是停留在当前页面,发现上面搜索函数中的

```javascript
url: $( "url" , this).text()
```
没有获取到搜索结果的url,结果为空。我看了插件作者当初写的文章(本文末尾)的链接,确乎是上面的代码。不过已经不能工作了。

对这个搜索函数略做修改,又可以正常work了,贴下代码

```javascript
var searchFunc = function(path, search_id, content_id) {
    'use strict';
    $.ajax({
        url: path,
        dataType: "xml",
        success: function( xmlResponse ) {
            // get the contents from search data

            var datas = $( "entry", xmlResponse ).map(function() {
                return {
                    title: $( "title", this ).text(),
                    content: $("content",this).text(),
                    url: $( "link" , this).attr("href")
                };
            }).get();
            var $input = document.getElementById(search_id);
            var $resultContent = document.getElementById(content_id);
            $input.addEventListener('input', function(){
                var str='<ul class=\"search-result-list\">';
                var keywords = this.value.trim().toLowerCase().split(/[\s\-]+/);
                $resultContent.innerHTML = "";
                if (this.value.trim().length <= 0) {
                    return;
                }

                // perform local searching
                datas.forEach(function(data) {
                    var isMatch = true;
                    var content_index = [];
                    var data_title = data.title.trim().toLowerCase();
                    var data_content = data.content.trim().replace(/<[^>]+>/g,"").toLowerCase();
                    var data_url = data.url;
                    var index_title = -1;
                    var index_content = -1;
                    var first_occur = -1;
                    // only match artiles with not empty titles and contents
                    if(data_title != '' && data_content != '') {
                        keywords.forEach(function(keyword, i) {
                            index_title = data_title.indexOf(keyword);
                            index_content = data_content.indexOf(keyword);
                            if( index_title < 0 && index_content < 0 ){
                                isMatch = false;
                            } else {
                                if (index_content < 0) {
                                    index_content = 0;
                                }
                                if (i == 0) {
                                    first_occur = index_content;
                                }
                            }
                        });
                    }
                    // show search results
                    if (isMatch) {

                        str += "<li><a href='"+ data_url  +"' class='search-result-title'>"+ data_title +"</a>";
                       console.log(data_url);
                        console.log("=====命中=====", data);


                        var content = data.content.trim().replace(/<[^>]+>/g,"");
                        if (first_occur >= 0) {
                            // cut out 100 characters
                            var start = first_occur - 20;
                            var end = first_occur + 80;
                            if(start < 0){
                                start = 0;
                            }
                            if(start == 0){
                                end = 100;
                            }
                            if(end > content.length){
                                end = content.length;
                            }
                            var match_content = content.substr(start, end);
                            // highlight all keywords
                            keywords.forEach(function(keyword){
                                var regS = new RegExp(keyword, "gi");
                                match_content = match_content.replace(regS, "<em class=\"search-keyword\">"+keyword+"</em>");
                            });

                            str += "<p class=\"search-result\">" + match_content +"...</p>"
                        }
                        str += "</li>";
                    }
                });
                str += "</ul>";
                $resultContent.innerHTML = str;
            });
        }
    });
};

var path = "<%= config.root %>" + "search.xml";
searchFunc(path, 'local-search-input', 'local-search-result');
```

**********************

将以上的搜索框和搜索函数放在适当的地方即可,我是放在`layout.ejs`文件中的。

这样就完成了搜索框的核心部分了。这里我给出我定制过后的CSS

```CSS
/*============搜索栏样式封装=============*/
@media screen and (max-width: 1000px) {
  #site_search{
   display: none;
  }
}
@media screen and (min-width: 1000px){
  #site_search{
    position:fixed;
    z-index:4;
    white-space: normal;
    word-break: break-all;
  }
  #local-search-input{
    display: flex;
    justify-content: center;
    align-items: center;
    opacity: 0.5;
    width: 250px;
  }

  #local-search-input:focus{
    opacity: 0.8;
    width: 540px;
    animation: car .5s ease-in;
  }
  #local-search-result{
    background: white;
    color:black;
    opacity: .95;
    width: 570px;
    max-height: 600px;
    overflow: auto;
  }

  .search-result{
    max-height: 140px;
    overflow: hidden;
  }
}

@keyframes car {
  0%{
    width: 250px;
  }

  50%{
    width: 1000px;
  }

  100%{
    opacity: 0.8;
    width: 540px;
  }
}
/*============搜索栏样式封装=============*/
```

![2.png](/img/codelife/hexo-site-search/2.png)

*******************

### ** 主题改造 **

在我的第一篇博文[叶尖滴落的星球](http://www.sail.name/2016/12/01/first/)中,提到过本博客是使用的huno,它是为Hexo编写的一个响应式的主题，该主题基于Uno。

到此刻,已经大半年过去了,我也写下了接近90篇博文。中途也对huno主题进行了数次修改,以符合我的需求。

在修改的过程中,发现源码中的不少地方写得不够合理。现在我的博客和当初也已经相差挺大了。

<spna class="under0"> ** 或许今后再优化更多过后,我会开源一个Suno的主题 **</span>

现在博客PC端和移动端差距挺大的。



考虑到看我博客的大多数是程序员,来自PC的访问更多。
再加之手机相比PC硬件上差距还是很大,移动端,动画除了chrome都有些卡顿,于是就克制了一下,在移动端删除了首页动画...


*******************

### ** 参考 **

[jQuery-based Local Search Engine for Hexo](http://www.hahack.com/codes/local-search-engine-for-hexo/)

