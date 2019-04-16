---
title: JavaScript中分号引起的bug
date: 2019-04-14 09:08:30
categories: Javascript
---
### ** Prafece **

前阵子写代码遇到一个诡异的错误,排查了很久才定位到是分号的问题,本文做下记录

*****************

```javascript
// 可以正常工作
  showProjectTaskModal(projectTaskData) {
    this.setState({
      projectTaskData: projectTaskData
    })

  
    if (this.ifShowZhanKai()) {
      this.showZhanKai()
    }
  }

   // 可以正常工作
  showProjectTaskModal(projectTaskData) {
    this.setState({
      projectTaskData: projectTaskData
    });

  
    (this.ifShowZhanKai()) ?
      this.showZhanKai() :
      null
    
  }


  // 不可以正常工作
  showProjectTaskModal(projectTaskData) {
    this.setState({
      projectTaskData: projectTaskData
    })

  
    (this.ifShowZhanKai()) ?
      this.showZhanKai() :
      null
    
  }
```
上面的`showProjectTaskModal`函数,前两个可以正常工作,第三个却会抛错。问题在于`this.setState`后面有没有根分号。


**<span class="under0"> 至于说 “很难总结什么时候加不加”，其实真的很简单。真正会导致上下行解析出问题的 token 有 5 个：括号，方括号，正则开头的斜杠，加号，减号。我还从没见过实际代码中用正则、加号、减号作为行首的情况，所以总结下来就是一句话：一行开头是括号或者方括号的时候加上分号就可以了，其他时候全部不需要。——尤雨溪</span>**


*****************
### ** 参考链接 **
[JavaScript 语句后应该加分号么？ - 知乎](https://www.zhihu.com/question/20298345)