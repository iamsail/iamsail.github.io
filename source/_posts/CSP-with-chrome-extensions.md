---
title: 开发chrome插件遇到的CSP问题
date: 2019-07-28 12:01:45
categories: chrome-extensions
---

###  ** Preface **

最近开发chrome插件遇到了一个问题。

![1.png](/img/chrome-extensions/CSP-with-chrome-extensions/1.png)

我是使用react进行开发的,build过后,点击插件图标,显示了一个白色的方框,如上图所示。
最初毫无下手的头绪,直到后来发现,插件卡片处,出现了一个错误按钮,才发现有给出错误信息。
![2.png](/img/chrome-extensions/CSP-with-chrome-extensions/2.png)

```
# 错误信息
Refused to execute inline script because it violates the following 
Content Security Policy directive: "script-src 'self' https://apis.google.com". 
Either the 'unsafe-inline' keyword, a hash ('sha256-5As4+3YpY62+l38PsxCEkjB1R4YtyktBtRScTJ3fyLU='), 
or a nonce ('nonce-...') is required to enable inline execution.
```
***********************

###  ** 解决方案 **
```
{
  "name": "Hello Extensions",
  "description" : "Base Level Extension",
  "version": "1.0",
  "manifest_version": 2,
  "browser_action": {
    "default_popup": "index.html",
    "default_icon": {
      "19": "./hello_extensions.png",
      "38": "./hello_extensions.png"
  },
    "default_title": "帅"
  },
  "icons": {
    "16": "./hello_extensions.png",
    "48": "./hello_extensions.png",
    "128": "./hello_extensions.png"
},
  "permissions": [
    "alarms", "tabs", "notifications", "activeTab"
  ],
  "background": {
    "persistent": false,
    "scripts": [
      "background.js"
    ]
  },
  "commands": {
    "_execute_browser_action": {
      "suggested_key": {
          "windows": "Ctrl+Shift+Y",
          "mac": "Command+Shift+L",
          "chromeos": "Ctrl+Shift+U",
          "linux": "Ctrl+Shift+J"
      },
      "description": "Opens index.html"
    }
  },
  "content_security_policy":"script-src 'self' https://apis.google.com; object-src 'self'"
}
```

根据错误信息,我对`content_security_policy`增加了hash值(hash值来自错误信息)

```
{
  "name": "Hello Extensions",
  "description" : "Base Level Extension",
  "version": "1.0",
  "manifest_version": 2,
  "browser_action": {
    "default_popup": "index.html",
    "default_icon": {
      "19": "./hello_extensions.png",
      "38": "./hello_extensions.png"
  },
    "default_title": "帅"
  },
  "icons": {
    "16": "./hello_extensions.png",
    "48": "./hello_extensions.png",
    "128": "./hello_extensions.png"
},
  "permissions": [
    "alarms", "tabs", "notifications", "activeTab"
  ],
  "background": {
    "persistent": false,
    "scripts": [
      "background.js"
    ]
  },
  "commands": {
    "_execute_browser_action": {
      "suggested_key": {
          "windows": "Ctrl+Shift+Y",
          "mac": "Command+Shift+L",
          "chromeos": "Ctrl+Shift+U",
          "linux": "Ctrl+Shift+J"
      },
      "description": "Opens index.html"
    }
  },
  "content_security_policy":"script-src 'self' 'sha256-5As4+3YpY62+l38PsxCEkjB1R4YtyktBtRScTJ3fyLU=' https://apis.google.com; object-src 'self'"
}
```
重新build即可,如下图

![3.png](/img/chrome-extensions/CSP-with-chrome-extensions/2.png)

**************************
###  ** CSP **
CSP 定义 Content-Security-Policy HTTP 标头，其允许您创建信任的内容的来源白名单，并指示浏览器仅执行或渲染来自这些来源的资源，而不要盲目地信任服务器提供的所有内容。即使攻击者能够发现可从中注入脚本的漏洞，由于此脚本也不符合此白名单，因此，也不会执行该脚本。

假如我们信任 apis.google.com 传输有效代码，并且我们信任我们自己也能做到，因此，我们可以定义一个政策，该政策仅允许执行来自以下两个来源之一的脚本：
```
Content-Security-Policy: script-src 'self' https://apis.google.com
```

###  ** 语法 **
```
One or more sources can be allowed for the script-src policy:
Content-Security-Policy: script-src <source>;
Content-Security-Policy: script-src <source> <source>;
```
** 介绍常用的source取值 **

| source取值 | 含义 | 
| :--- | :----: | 
|`'self'`| 指从中提供受保护文档的来源，包括相同的URL方案和端口号。 您必须包含单引号。 某些浏览器专门从源指令中排除blob和文件系统。 需要允许这些内容类型的站点可以使用Data属性指定它们。|
| `'none'` | 指空集; 也就是说，没有URL匹配。 单引号是必需的。|
| `'<hash-algorithm>-<base64-value>'`| 脚本或样式的sha256，sha384或sha512哈希。 此源的使用包括由短划线分隔的两个部分：用于创建散列的加密算法和脚本或样式的base64编码散列。 生成哈希时，不要包含`<script>`或`<style>`标记，并注意大小写和空格很重要，包括前导或尾随空格。 有关示例，请参阅不安全的内联脚本。 在CSP 2.0中，这仅适用于内联脚本。 对于外部脚本，CSP 3.0允许使用script-src。 |
|`'unsafe-inline'` | 允许使用内联资源，例如内联`<script>`元素，javascript：URL，内联事件处理程序和内联`<style>`元素。 您必须包含单引号。|
|`'unsafe-eval'`| 允许使用`eval（）`和类似方法从字符串创建代码。 您必须包含单引号。 |
*********************
CSP还有一些其他常用的资源指令

| 资源指令 | 含义 | 
| :--- | :----: | 
|`base-uri` | 用于限制可在页面的 `<base>` 元素中显示的网址 | 
|`child-src` | 用于列出适用于工作线程和嵌入的帧内容的网址。例如：child-src https://youtube.com 将启用来自 YouTube（而非其他来源）的嵌入视频。 使用此指令替代已弃用的 frame-src 指令。 | 
|`connect-src` | 用于限制可（通过 XHR、WebSockets 和 EventSource）连接的来源。 | 
|`font-src` | 用于指定可提供网页字体的来源。Google 的网页字体可通过 font-src https://themes.googleusercontent.com 启用。 | 
|`object-src` | 可对 Flash 和其他插件进行控制。 | 
|`style-src`| script-src 版的样式表 | 
|`img-src` | 用于定义可从中加载图像的来源 | 

**************************

###  ** 参考链接 **

- [CSP: script-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/script-src)
- [内容安全政策](https://developers.google.com/web/fundamentals/security/csp/?hl=zh-cn)
- [An Introduction to Content Security Policy](https://www.html5rocks.com/en/tutorials/security/content-security-policy)
- [Content Security Policy Level 3](https://w3c.github.io/webappsec-csp/)