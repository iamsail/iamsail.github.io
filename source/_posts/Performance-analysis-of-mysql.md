---
title: MySQL性能分析
date: 2018-5-06 08:20:45
categories: 数据库
tags: [MySQL]
---

### ** Preface **

本文是对MySQL中性能分析的`EXPLAIN`和`PROFILE`的介绍

********************************

### ** EXPLAIN **


EXPLAIN语句提供了有关SELECT语句的执行计划的信息。完整的EXPLAIN用法见[官方文档](https://dev.mysql.com/doc/refman/5.5/en/explain-output.html)

EXPLAIN返回SELECT语句中使用的每个表的一行信息。 它按照MySQL在处理语句时读取它们的顺序列出输出中的表。 MySQL使用嵌套循环连接方法解析所有连接。 这意味着MySQL从第一个表中读取一行，然后在第二个表，第三个表等中找到匹配的行。 处理完所有表后，MySQL将通过表列表输出所选列和回溯，直到找到有更多匹配行的表。 下一行从该表中读取，并且该过程继续下一个表.

```
mysql> explain select * from help_category;
+----+-------------+---------------+------------+------+---------------+------+---------+------+------+----------+-------+
| id | select_type | table         | partitions | type | possible_keys | key  | key_len | ref  | rows | filtered | Extra |
+----+-------------+---------------+------------+------+---------------+------+---------+------+------+----------+-------+
|  1 | SIMPLE      | help_category | NULL       | ALL  | NULL          | NULL | NULL    | NULL |   40 |   100.00 | NULL  |
+----+-------------+---------------+------------+------+---------------+------+---------+------+------+----------+-------+
1 row in set, 1 warning (0.00 sec)

<=====>

mysql> explain select * from help_category\G;
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: help_category
   partitions: NULL
         type: ALL
possible_keys: NULL
          key: NULL
      key_len: NULL
          ref: NULL
         rows: 40
     filtered: 100.00
        Extra: NULL
1 row in set, 1 warning (0.00 sec)
```

|列|北京|
|:----:|:----:|
|id|查询标识符|
|select_type|查询类型|
|table|显示这一行的数据是关于哪张表|
|partitions|使用的哪个分区|
|type|[the join type](https://dev.mysql.com/doc/refman/5.5/en/explain-output.html#explain-join-types),描述这些表是如何连接的|
|possible_keys|可能用到的索引|
|key|实际用到的索引|
|key_len|实际用到的索引的长度|
|ref|引用索引对应的表中哪些行|
|rows|该查询遍历了多少行数据|
|filtered|通过过滤条件之后对比总数的百分比|
|Extra|额外信息|

#### ** select_type **
|查询类型值|解释|
|:----:|:----:|
|SIMPLE|简单select(不使用union或子查询)|
|PRIMARY|最外面的select|
|UNION|union中的第二个或后面的select|
|DEPENDENT UNION|union union中的第二个或后面的select语句,取决于外面的查询|
|UNION RESULT|result union的结果|
|SUBQUERY|子查询中的第一个select|
|DEPENDENT SUBQUERY|subquery 子查询中的第一个select,取决于外面的查询|
|UNCACHEABLE SUBQUERY|不可缓存的子查询,必须重新评估外部查询的每一行|
|UNCACHEABLE UNION|union中的第二个或后面的select,且属于UNCACHEABLE SUBQUERY|

#### ** type **
从最好到最差的连接类型:

`system > const > eq_ref > ref > fulltext > ref_or_null > index_merge > unique_subquery > index_subquery > range > index > ALL`

ALL代表扫描了全表才确定结果。一般来说,得保证查询至少达到range级别,最好能达到ref。可以通过加索引等方法来优化。

************************
### ** PROFILE **

当我们要对某一条sql的性能进行分析时,可以使用PROFILE来分析SQL语句的执行过程。

这个我用得还不多,推荐阅读[MySQL使用profile分析SQL语句执行过程](http://www.ywnds.com/?p=8677)

************************
### ** 参考 **

[EXPLAIN Output Format](https://dev.mysql.com/doc/refman/5.5/en/explain-output.html)
[MySQL索引原理及慢查询优化](https://tech.meituan.com/mysql-index.html)
[Mysql处理海量数据时的一些优化查询速度方法](http://www.imooc.com/article/1204)
[【mysql的设计与优化专题(6)】mysql索引攻略](http://www.cnblogs.com/nixi8/p/4574709.html)
[mysql 执行计划explain详解](https://blog.csdn.net/u012410733/article/details/66472157)
[MySQL使用profile分析SQL语句执行过程](http://www.ywnds.com/?p=8677)
