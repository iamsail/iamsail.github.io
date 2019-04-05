---
title: MIME 类型
date: 2019-04-05 10:32:00
categories: HTML&&CSS
---

`<input>` type 类型为 file 的 input 元素使得用户可以选择一个或多个元素以提交表单的方式上传到服务器上，或者通过 Javascript 的 File API 对文件进行操作 .

如果你不希望用户上传任何类型的文件, 你可以使用` input `的` accept `属性.accept 属性接受一个逗号分隔的` MIME `类型字符串, 如:

```
accept="image/png" or accept=".png" — 只接受 png 图片.
accept="image/png, image/jpeg" or accept=".png, .jpg, .jpeg" — PNG/JPEG 文件.
accept="image/*" — 接受任何图片文件类型
accept=".doc,.docx,.xml,application/msword,application/vnd.openxmlformats-officedocument.wordprocessingml.document" — 接受任何 MS Doc 文件类型.
```

** accept 属性并不会验证选中文件的类型. 他只是为开发这提供了一种引导用户做出期望行为的方式而已, 用户还是有办法绕过浏览器的限制.<span class="under0">因此, 在服务器端进行文件类型验证是必不可少的.</span> **

******************

### ** MIME 类型 **

多用途Internet邮件扩展（MIME）类型 是一种标准化的方式来表示文档的性质和格式。 浏览器通常使用MIME类型（而不是文件扩展名）来确定如何处理文档；因此服务器设置正确以将正确的MIME类型附加到响应对象的头部是非常重要的。

#### ** 语法 **

`type/subtype`

MIME的组成结构非常简单；由类型与子类型两个字符串中间用'/'分隔而组成。不允许空格存在。type 表示可以被分多个子类的独立类别。subtype 表示细分后的每个类型。** MIME类型对大小写不敏感，但是传统写法都是小写。**

以下是一些常用的MIME类型和后缀的对应，完整的请戳[Media Types](https://www.iana.org/assignments/media-types/media-types.xhtml)

```
后缀名       MIME名称

*.3gpp    audio/3gpp, video/3gpp
*.ac3     audio/ac3
*.asf     allpication/vnd.ms-asf
*.au      audio/basic
*.css     text/css
*.csv     text/csv
*.doc     application/msword    
*.docx    application/vnd.openxmlformats-officedocument.wordprocessingml.document
*.dot     application/msword    
*.dtd     application/xml-dtd    
*.dwg     image/vnd.dwg    
*.dxf     image/vnd.dxf
*.gif     image/gif    
*.htm     text/html    
*.html    text/html    
*.jp2     image/jp2    
*.jpe     image/jpeg
*.jpeg    image/jpeg
*.jpg     image/jpeg    
*.js      text/javascript, application/javascript    
*.json    application/json    
*.mp2     audio/mpeg, video/mpeg    
*.mp3     audio/mpeg    
*.mp4     audio/mp4, video/mp4    
*.mpeg    video/mpeg    
*.mpg     video/mpeg    
*.mpp     application/vnd.ms-project    
*.ogg     application/ogg, audio/ogg    
*.pdf     application/pdf    
*.png     image/png    
*.pot     application/vnd.ms-powerpoint    
*.pps     application/vnd.ms-powerpoint    
*.ppt     application/vnd.ms-powerpoint    
*.pptx    application/vnd.openxmlformats-officedocument.presentationml.presentation
*.rtf     application/rtf, text/rtf    
*.svf     image/vnd.svf    
*.tif     image/tiff    
*.tiff    image/tiff    
*.txt     text/plain    
*.wdb     application/vnd.ms-works    
*.wps     application/vnd.ms-works    
*.xhtml   application/xhtml+xml    
*.xlc     application/vnd.ms-excel    
*.xlm     application/vnd.ms-excel    
*.xlt     application/vnd.ms-excel    
*.xlw     application/vnd.ms-excel    
*.xml     text/xml, application/xml    
*.zip     aplication/zip    
*.xls     application/vnd.ms-excel    
*.xlsx    application/vnd.openxmlformats-officedocument.spreadsheetml.sheet

```

*******************
### ** 参考链接 **

[MIME 类型 - HTTP | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics_of_HTTP/MIME_types)
[HTML5的 input:file上传类型控制](https://www.haorooms.com/post/input_file_leixing)
[常用文件的mime和mimetype的对应关系 - 阳水平的博客 - CSDN博客](https://blog.csdn.net/zhezhebie/article/details/80513499)
[`<input type="file">` - HTML（超文本标记语言） | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/file)
[Media Types](https://www.iana.org/assignments/media-types/media-types.xhtml)