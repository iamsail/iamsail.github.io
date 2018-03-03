---
title: MySQL字符编码相关设置
date: 2018-3-03 8:39:45
categories: 数据库
tags: [MySQL, SQL,  字符编码]
---

### **  Preface **

最近开发的时候,因为数据库相关字段编码设置的问题,出现了bug。本文是对MySQL字符编码相关设置的记录。

本文较多参考了鸟哥的[ 深入Mysql字符集设置 ](http://www.laruence.com/2008/01/05/12.html)一文,更多参考链接均在文末。

****************
### ** 基本概念 **

• ** 字符(Character) **是指人类语言中最小的表义符号。例如’A'、’B'等；

• 给定一系列字符，对每个字符赋予一个数值，用数值来代表对应的字符，这一数值就是** 字符的编码(Encoding) **。例如，我们给字符’A'赋予数值0，给字符’B'赋予数值1，则0就是字符’A'的编码；

• 给定一系列字符并赋予对应的编码后，所有这些字符和编码对组成的集合就是** 字符集(Character Set) **。例如，给定字符列表为{‘A’,'B’}时，{‘A’=>0, ‘B’=>1}就是一个字符集；

• ** 字符序(Collation) **是指在同一字符集内字符之间的比较规则；

• 确定字符序后，才能在一个字符集上定义什么是等价的字符，以及字符之间的大小关系；

• ** 每个字符序唯一对应一种字符集，但一个字符集可以对应多种字符序，其中有一个是默认字符序(Default Collation)；**

• MySQL中的字符序名称遵从命名惯例：以字符序对应的字符集名称开头；以_ci(表示大小写不敏感)、_cs(表示大小写敏感)或_bin(表示按编码值比较)结尾。例如：在字符序“utf8_general_ci”下，字符“a”和“A”是等价的；

*****************

### ** 查看编码 **

#### ** 查看数据库编码 **

```sql
> show variables like '%char%'; | show variables like 'character%';

+--------------------------+------------------------------------------------------------+
| Variable_name            | Value                                                      |
+--------------------------+------------------------------------------------------------+
| character_set_client     | gbk                                                        |
| character_set_connection | gbk                                                        |
| character_set_database   | utf8mb4                                                    |
| character_set_filesystem | binary                                                     |
| character_set_results    | gbk                                                        |
| character_set_server     | latin1                                                     |
| character_set_system     | utf8                                                       |
| character_sets_dir       | D:\tools\wamp\wamp64\bin\mysql\mysql5.7.19\share\charsets\ |
+--------------------------+------------------------------------------------------------+
```

#### ** 系统变量介绍 **

```
character_set_client        客户端来源数据使用的字符集
character_set_connection    连接层字符集(从客户端接收到数据，然后传输的字符集)
character_set_database      当前选中数据库的默认字符集
character_set_filesystem    把os上文件名转化成此字符集，即把 character_set_client转换character_set_filesystem， 默认binary是不做任何转换的
character_set_results       查询结果字符集
character_set_server        默认的内部操作字符集
character_set_system        系统元数据(字段名等)字符集
character_sets_dir          该目录保存配置文件，使MySQL可以使用不同的字符集。
```

#### ** MySQL中的字符集转换过程 **

A. MySQL Server收到请求时将请求数据从`character_set_client`转换为`character_set_connection`；

B. 进行内部操作前将请求数据从`character_set_connection`转换为内部操作字符集，其确定方法如下：

• 使用每个数据字段的`CHARACTER SET`设定值；

• 若上述值不存在，则使用对应数据表的`DEFAULT CHARACTER SET`设定值(MySQL扩展，非SQL标准)；

• 若上述值不存在，则使用对应数据库的`DEFAULT CHARACTER SET`设定值；

• 若上述值不存在，则使用`character_set_server`设定值。

C. 将操作结果从内部操作字符集转换为`character_set_results`。

![MySQL中的字符集转换过程](/img/database/the-setting-of-Character-encoding-format-about-mysql/1.jpg)

#### ** 查看所有数据库的编码 **
```sql
> SELECT SCHEMA_NAME 'database', default_character_set_name 'charset', DEFAULT_COLLATION_NAME 'collation' FROM information_schema.SCHEMATA;
```
#### ** 查看单个数据库的编码 **

```sql
> USE my_database;
> show variables like "character_set_database";
```

#### ** 查看表编码 **
```sql
show create table <表名>;
```

#### ** 查看数据表中字符集设置  **

```sql
> show full columns from <表名>;

+----------------+------------------+--------------------+------+-----+---------+----------------+---------------------------------+---------+
| Field          | Type             | Collation          | Null | Key | Default | Extra          | Privileges                      | Comment |
+----------------+------------------+--------------------+------+-----+---------+----------------+---------------------------------+---------+
| id             | int(10) unsigned | NULL               | NO   | PRI | NULL    | auto_increment | select,insert,update,references |         |
| name           | varchar(191)     | utf8mb4_unicode_ci | NO   |     | NULL    |                | select,insert,update,references |         |
| email          | varchar(191)     | utf8mb4_unicode_ci | NO   | UNI | NULL    |                | select,insert,update,references |         |
| password       | varchar(191)     | utf8mb4_unicode_ci | NO   |     | NULL    |                | select,insert,update,references |         |
| remember_token | varchar(100)     | utf8mb4_unicode_ci | YES  |     | NULL    |                | select,insert,update,references |         |
| created_at     | timestamp        | NULL               | YES  |     | NULL    |                | select,insert,update,references |         |
| updated_at     | timestamp        | NULL               | YES  |     | NULL    |                | select,insert,update,references |         |
+----------------+------------------+--------------------+------+-----+---------+----------------+---------------------------------+---------+
```

<span class="under0">**这里要特别说明**</span>,网上的很多文章都是将 `show full columns from <表名>` 这个命令写为查看字段的编码。这个确切的说来是错误的。

<span class="under0">**从上面的查询结果可以看到实际查询出来的是Collation(字符序),而不是字段的编码,但是我们可以通过Collation(字符序)的前缀得知字段的编码。**</span>

在stackoverflow上找到这样一段命令

#### ** 查询当前数据库所有表的所有字段的字符编码 **

```sql
SELECT TABLE_SCHEMA,
       TABLE_NAME,
       CCSA.CHARACTER_SET_NAME AS DEFAULT_CHAR_SET,
       COLUMN_NAME,
       COLUMN_TYPE,
       C.CHARACTER_SET_NAME
  FROM information_schema.TABLES AS T
  JOIN information_schema.COLUMNS AS C USING (TABLE_SCHEMA, TABLE_NAME)
  JOIN information_schema.COLLATION_CHARACTER_SET_APPLICABILITY AS CCSA
       ON (T.TABLE_COLLATION = CCSA.COLLATION_NAME)
 WHERE TABLE_SCHEMA=SCHEMA()
   AND C.DATA_TYPE IN ('enum', 'varchar', 'char', 'text', 'mediumtext', 'longtext')
 ORDER BY TABLE_SCHEMA,
          TABLE_NAME,
          COLUMN_NAME
;
```
这里推荐阅读[MySQL中CREATE DATABASE和CREATE SCHEMA区别](http://blog.useasp.net/archive/2013/05/21/The-difference-between-create-database-and-create-schema-in-mysql.aspx)


#### ** 查询所有表的信息 **

```sql
> SHOW TABLE STATUS
```

#### ** 查询单张数据表的信息 **

```sql
> SHOW TABLE STATUS where name like 'table_123'; |
> SHOW TABLE STATUS where name = 'table_name';
```

*************
### ** 修改编码 **

#### ** 修改数据库编码格式 **

```sql
alter table <表名> character set utf8;
```

#### ** 修改一张表的所有字段的编码格式 **
```sql
alter table `tablename` convert to character set utf8;  
```

#### ** 修改数据表编码格式 **

```sql
alter table <表名> character set utf8;
```

#### ** 修改字段编码格式 **

```sql
alter table <表名> change <字段名> <字段名> <类型> character set utf8;
```

注意字段名要输入两次

*************

### ** 存emoji表情 **

mysql的`utf8`编码的一个字符最多3个字节，但是一个emoji表情为4个字节，所以utf8不支持存储emoji表情。但是`utf8`的超集`utf8mb4`一个字符最多能有4字节，所以能支持emoji表情的存储。

****************

### ** 参考 **

[整理 ： 查看和修改 mysql库、表、字段编码](http://blog.csdn.net/springsunss/article/details/70337915)
[深入Mysql字符集设置](http://www.laruence.com/2008/01/05/12.html)
[mysql字符集小结](http://blog.csdn.net/wyzxg/article/details/8779682)
[How do I see what character set a MySQL database / table / column is?](https://stackoverflow.com/questions/1049728/how-do-i-see-what-character-set-a-mysql-database-table-column-is)
[数据库 schema含义](http://blog.csdn.net/netcome/article/details/2048296)
[MySQL中CREATE DATABASE和CREATE SCHEMA区别](http://blog.useasp.net/archive/2013/05/21/The-difference-between-create-database-and-create-schema-in-mysql.aspx)
[mysql修改数据库表和表中的字段的编码格式的修改](http://blog.csdn.net/luo4105/article/details/50804148)
[浅谈MySQL中utf8和utf8mb4的区别](http://blog.xieyc.com/utf8-and-utf8mb4/)
****************
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>