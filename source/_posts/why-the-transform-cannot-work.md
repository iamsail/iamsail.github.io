---
title: transform失效了?
date: 2017-05-06 22:10:17
categories: HTML&&CSS
---

<style>

    .underline{
        border-bottom:2px ridge red;
    }

</style>

#### ** 问题背景: **

昨晚在某个群，看到一个问题:** 大概是CSS动画,color属性能够生效，transform属性却没能生效。 **

***************************************

作者写了个demo,重现了一下问题,** 更多请戳[demo](http://www.sail.name/CSS_Demo/why-the-transform-cannot-work-test.html) **

```
        .tow{
            width: 200px;
            height: 200px;
            border-radius: 50%;
            background-color: red;
            /*display: inline-block;*/
            animation: test 5s 1s infinite;
            text-align: center;
            line-height:200px;
        }

        @keyframes test {
            0%{
                transform: translateX(0px);
            }

            100%{
                background-color: darkturquoise;
                transform: translateX(500px);
            }
        }


        <span class="tow">tow</span>
```

上面这段代码只能看到背景颜色的转变,却看不到transform的变化

最后这位同学在样式中设置了<code>display:inline-block</code>就搞定了

**************************

当时我正在复习概率论。今天查阅了些资料,大致弄明白其中的道理。

[规范中有这样一段描述:](https://www.w3.org/TR/css-transforms-1/#transform-property)

** transformable element **
** A transformable element is an element in one of these categories: **
an element whose layout is governed by the CSS box model<span class="underline"> which is either a block-level or atomic inline-level element,</span>or whose display property computes to table-row, table-row-group, table-header-group, table-footer-group, table-cell, or table-caption [CSS21]
an element in the SVG namespace and not governed by the CSS box model which has the attributes transform, ‘patternTransform‘ or gradientTransform [SVG11].

注意到下划线部分:** which is either a block-level or atomic inline-level element **

transform适用的范围包括但不限于a block-level or atomic inline-level element

block-level本文并不讨论。这里我想谈谈Inline-level elements , inline boxes ,Inline-level boxes

** 依旧先看看规范 **

** Inline-level elements and inline boxes **

<span class="underline">Inline-level elements are those elements of the source document that do not form new blocks of content; </span>the content is distributed in lines (e.g., emphasized pieces of text within a paragraph, inline images, etc.). <span class="underline">The following values of the 'display' property make an element inline-level: 'inline', 'inline-table', and 'inline-block'. </span>Inline-level elements generate inline-level boxes, which are boxes that participate in an inline formatting context.

An inline box is one that is both inline-level and whose contents participate in its containing inline formatting context.<span class="underline"> A ** non-replaced ** element with a 'display' value of 'inline' generates an inline box. Inline-level boxes that are not inline boxes (such as replaced inline-level elements, inline-block elements, and inline-table elements) are called ** atomic inline-level boxes ** because they participate in their inline formatting context as a single opaque box.</span>

**************************

上面这两段我反复读了数十次,一直翻译不好。

最后在[MDN](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Visual_formatting_model)上看到一段翻译,如下

行内级元素生成行内级盒(inline-level boxes)，参与行内格式化上下文(inline formatting context)。同时参与生成行内格式化上下文的行内级盒称为行内盒(Inline boxes)。所有display:inline 的非替换元素生成的盒是行内盒。而不参与生成行内格式化上下文的行内级盒称为原子行内级盒(atomic inline-level boxes)。这些盒由可替换行内元素，或 display 值为 inline-block 或 inline-table 的元素生成，不能拆分成多个盒

** 或许你会有些疑惑,为什么和你的翻译不一样。文末会进行解答 **

看看下图加深理解

![inlines.png](/img/htmlcss/inlines.png)

当一个元素的display的值为inline,inline-table,inline-block时,这个元素是行内级元素/内联级元素(Inline-level elements)。这些行内级元素会生成一个行内级盒,即inline-level boxes。倘若这个盒子还同时参与生成行内格式化上下文(IFC),该行内级盒称为行内盒(Inline boxes)。而用inline-level boxes集合减去Inline boxes集合便是atomic inline-level boxes(原子行内级盒)。即是不参与生成行内格式化上下文的行内级盒。** 这些盒由可替换行内元素，或 display 值为 inline-block 或 inline-table 的元素生成，不能拆分成多个盒。**

至于什么是可替换元素,什么是不可替换元素,[戳这儿](https://www.w3.org/TR/CSS21/conform.html)
**************************

回到最初,这位同学之所以在样式中设置了<code>display:inline-block</code>就解决了问题。

** 是因为transform作用于transformable element(作者在这里译为可变元素), **有以下两种

1.an element whose layout is governed by the CSS box model<span class="underline"> which is either a block-level or atomic inline-level element, </span>or whose display property computes to table-row, table-row-group, table-header-group, table-footer-group, table-cell, or table-caption [CSS21]

2.an element in the SVG namespace and not governed by the CSS box model which has the attributes transform, ‘patternTransform‘ or gradientTransform [SVG11].

** span会形成inline boxes,而不会形成atomic inline-level boxes。span本身并不是可变元素,在设置<code>display:inline-block</code>就是atomic inline-level boxes。**

**************************

在查阅文档过程中遇到几个问题

1.规范在对atomic inline-level boxes出现了 a single opaque box。single比较好理解,单个的,不可拆分的。而opaque是不透明的意思,MDN上的翻译,直接忽略了这个词。规范中确乎有一处进行了描述,[戳这儿](https://www.w3.org/2009/07/B-and-B/border-image-shadow-combine.html)。这里作者的理解就是从字面意思理解,不透明的。如果你有更好的理解,可以告诉我。

2.第二个问题,是规范中有处错误,导致我的走了一些弯路。这里指出

<span class="underline">Inline-level boxes </span> that are not <span class="underline"> inline boxes </span>  (such as replaced inline-level elements, inline-block elements, and inline-table elements) are called atomic inline-level boxes because they participate in their inline formatting context as a single opaque box.

在上面这段中,有两处下滑线和一对括号。** 括号是应该紧放在需要进行形容,具体说明的词的后方。 **按照这段文字的表达,括号中的内容是对inline boxes进行说明的。而实际上括号中的内容是对inline-boxes的具体诠释。

作者便是在这儿疑惑不已,耽误了几个小时。** 最后在高中同桌答谋锐的帮助下理清了思路。 **

**************************

#### ** 写在最后 **

- ** 感谢小志的赞赏 **,虽然我只是提出了一个问题而已。

