---
title: JSON必知必会
date: 2016-12-18 19:23:45
categories: JSON
---

最近看了《JSON必知必会》，做些记录。其实主要是想讲讲**语法验证和一致性验证**。

**文末亦有书籍的相关信息(书名，作者，ISBN)。**

## 基础知识

**老司机可以跳过这段**


什么是JSON。JSON是一种**数据交换格式**。数据交换格式是一种在不同平台间传递数据的文本格式。除JSON外，你也可能听说过XML这种数据交换格式。像XML和JSON这样的数据交换格式非常重要，我们需要它们来实现不同系统间的数据交换。


JSON是一种被许多系统用于交换数据格式的数据交换格式，但**不是所有的系统都支持使用JSON来交换数据。**


JSON的全称是Javascript Object Notation(Javascript对象表示法)。JSON基于Javascript对象字面量。JSON独立于编程语言（你不必先学习JS）。

当然如果你会JS，那就再好不过了。


#### 什么是表示法

一个用于表示诸如数字或单词等数据的字符系统


#### 什么是字面量

所谓字面量，是对数据值的具体表示。**它的字面意思与其想要表达的意思完全一致。**	
		
		a=5
		a=a+5


a的值是10，是一个变量。这里，5就是5，是字面量


JSON的表示形式是名称-值对。也叫键-值对，属性-值对，或者字段-值对。
JSON中使用冒号（：）来分隔名称和值。名称始终在左侧，值始终在右侧。


**比如，使用JSON来描述我的内裤**

		{
			"brand":"CK",
			"Color":"black",
			"size":23
		}




JSON中的名称-值对列表被花括号包裹

**名称必须被双引号包裹，而值并不是总是需要被双引号包裹。**

当值是字符串时，必须使用双引号。而在json中，还有数字、布尔值、数组、对象、null等其他数据类型，而这些都不应该被双引号包裹。


双引号中的名称可以是任何有效的字符串，例如

		"My animal":"cat"
		"Sail's animal":"dog"



在JSON中是完全合法的。但是最好不要这样做。

因为，JSON中的名称-值对是一种对许多系统都十分友好的数据结构，**而使用空格和特殊字符（字母和数字以外）忽略了可移植性（以一种双方系统都兼容的方式在平台间传递信息）。如果我们这样做的话，会降低JSON数据的可移植性**


*****

### JSON文件

JSON这种数据交换格式是可以作为独立的文件存在于文件系统中的。它的文件扩展名非常好记.json。



### JSON的媒体类型


媒体类型也叫作，互联网媒体类型，内容类型，MIME类型
它使用“类型/子类型”这种格式来表示，比如text/html
JSON的MIME类型是application/json



### JSON中的布尔类型

**只能使用小写 true或false，其他的TRUE/FALSE都是错误的**


**JSON中的null类型，也必须使用小写**

*******

## 语法验证

语法验证关注的是JSON的格式，检测我们的JSON语法是否正确（是否被被花括号包括，名称-值对是否以逗号分隔）。

JSON语法验证工具

- [JSON Formatter & Validator](https://jsonformatter.curiousconcept.com/)

这是一个带有配置选项、能够高亮错误且UI很棒的格式化工具。经过处理的JSON会显示在两个窗口，一个用于展示JSON的树/节点结构，类似于可视化工具，另一个用于复制/粘贴格式化后的代码
	

- [JSON Editor Online](http://www.jsoneditoronline.org/)

这是一个集验证、格式化和可视化工具于一身的JSON工具。错误提示会显示在出错的那一行。除了验证以外，还会显示解析错误的详情，右边的可视化工具使用树/节点的形式来展示JSON。
	

- [JSONLint](http://jsonlint.com/)

这是一个毫不花哨的JSON验证工具。简单的复制、粘贴、验证即可。也可以友好地格式化你的JSON。


以上都是语法验证工具。


**一致性验证关注的是其独特的数据结构，**会检测我们的数据是否包含name，breed和age等信息。它还会检测
age的值是不是数字，name的值是不是字符串，等等......

******

## 一致性验证

JSON验证器负责验证语法错误，**JSON Schema负责提供一致性验证。**

JSON Schema(Schema意为模式)，数据交换中的一种虚拟“合同”。
JSON Schema是数据接收方的第一道防线，也是数据发送方节约时间、保证数据正确的好工具。

JSON Schema可以解决以下有关一致性验证的问题

- **值的数据类型是否正确？**
  可以具体规定一个值是数字、字符串类型

- **是否包含数据所需要的数据？**
  可以具体规定哪些数据是需要的，哪些是不需要的

- **值的形式是不是我需要的？**
  可以指定范围、最小值和最大值


尽管JSON已经相当成熟，但JSON Schema仍在开发当中。截至2015年4月，JSON Schema最新版是草拟版本4。当然这并不意味着你现在不可以使用它，这仅仅说明了它仍旧在成长当中，且将来会做得更好。


JSON Schema使用JSON来书写，所以几步就能掌握它。
首先，需要在JSON第一个名称-值对中，声明一个schema文件。


		{
			"$schema": "http://json-schema.org/draft-04/schema#"
		}


第二个名称-值对，应该是JSON Schema文件的标题


		{
			"$schema": "http://json-schema.org/draft-04/schema#",
			"title":"cat"
		}


第三个名称-值对，要**定义需要在JSON中包含的属性。**"properties"的值实质上是我们想要的JSON的名称-值对的骨架。

		{
			"$schema": "http://json-schema.org/draft-04/schema#",
			"title":"cat",
			"properties":{
			"name":{
				"type":"string"
			   },
			"age":{
				"type":"number",
				"description":"your cat's age in years."
			   },
			"declawed":{
				"type":"boolean"
			  },
			"description":{
			            "type":"string"
			 }
			}
		}


如果想实现某些字段不能漏填，需要加上在"$schema"，"title"，"properties"后面加上第四个名称-值对，**它的名称是
"required",值为一个数组，数组中包含必填字段。**

假设"name","age","declawed"是必填字段，所以把它们加入数组。"description"不是必填字段，就不应加入数组
		
		{
			"$schema": "http://json-schema.org/draft-04/schema#",
			"title":"cat",
			"properties":{
			"name":{
				"type":"string"
			   },
			"age":{
				"type":"number",
				"description":"your cat's age in years."
			   },
			"declawed":{
				"type":"boolean"
			  },
			"description":{
			            "type":"string"
			 }
			}，
			"required":[
				"name",
				"age",
				"declawed"
			]
		}


例如

		{
			"name":"Fluffy",
			"age":2,
			"declawed":"false",
			"description":"hello world."
		}

		{
			"name":"Fluffy",
			"age":2,
			"declawed":"false"
		}

以上两个都是合法的JSON。

需要提一下的是，如果你JSON Schema中不包含"required"名称-值对，那么将不会有必填项。**一个没有任何名称-值对的空JSON对象也被认为是合法的。**例如

		{}

也是合法的JSON。

现在还有一个问题，值的形式是不是我们所需要的？比如用户名不能超过30个字符，年龄不为负数等。
	
	{
		"$schema": "http://json-schema.org/draft-04/schema#",
		"title":"cat",
		"properties":{
		"name":{
			"type":"string",
			"minLength":3,
			"maxLength":20
		   },
		"age":{
			"type":"number",
			"description":"your cat's age in years.",
			"minmum":0
		   },
		"declawed":{
			"type":"boolean"
		  },
		"description":{
		            "type":"string"
		 }
		}，
		"required":[
			"name",
			"age",
			"declawed"
		]
	}


以上只是JSON Schema的冰山一角，JSON Schema还支持正则表达式等。
如果你希望深入了解掌握JSON Schema，可以访问以下链接

- [JSON Schema主页](http://json-schema.org/)


JSON Schema在线检测工具

- [JSON Schema Lint](http://jsonschemalint.com/#/version/draft-05/markup/json)
- [JSON Schema Validator](http://www.jsonschemavalidator.net/)


《JSON必知必会》一书还讲到了一些安全方面的问题，跨站请求伪造，注入攻击等。

有兴趣的话可以买来看看。

<i>Introduction to Javascript Object Notation<i/> by Lindsay Bassett(O'Reilly).
Copyright 2015 Lindsay Bassett,978-1-491-92948-3.

![《JSON必知必会》](/img/read/JSONbzbh.png)


<hr />
    <p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
    </p>