---
title: MySQL缓存处理
date: 2018-5-03 21:51:45
categories: 数据库
tags: [MySQL]
---

### ** Preface **

缓存可以加快我们的查询速度,但是在做性能优化的时候,通常需要关闭缓存,避免缓存给性能优化带来的影响。本文做些记录。

************************
#### ** 基础 **

`sql_cache`，将查询结果放入查询缓存中。
`sql_no_cache`，查询的时候不缓存查询结果。
`sql_buffer_result`，在查询语句中，将查询结果缓存到临时表中。


`FLUSH QUERY CACHE`，可以整理查询缓存，以更好的利用它的内存。这个命令不会从缓存中移除任何查询。
`FLUSH TABLES`， 会转储清除查询缓存。
`RESET QUERY CACHE`， 使命从查询缓存中移除所有的查询结果,重置查询缓存。


#### ** show variables like '%query_cache%'; **

```
> show variables like '%query_cache%';


+------------------------------+----------+
| Variable_name                | Value    |
+------------------------------+----------+
| have_query_cache             | YES      |
| query_cache_limit            | 1048576  |
| query_cache_min_res_unit     | 4096     |
| query_cache_size             | 16777216 |
| query_cache_type             | OFF      |
| query_cache_wlock_invalidate | OFF      |
+------------------------------+----------+
```

|系统变量|解释|
|:---:|:----:|
|`have_query_cache`|表示当前版本的MYSQL是否支持Query Cache.|
|`query_cache_limit`|表示单个结果集所被允许缓存的最大值.默认是 1MB，超过此参数设置的 Query 结果集将不会被 Cache|
|`query_cache_min_res_unit`|每个被缓存的结果集要占用的最小内存.|
|`query_cache_type`|mysql就是根据这个变量的值来决定到底要不要把查询结果放到查询缓存中. 有三个取值：0,1,2，分别代表了off、on、demand。|
|`query_cache_size`|使用的内存大小，默认值为 16M，大小必须是 1024 的整数倍，如果不是整数倍，MySQL 会自动调整降低最小量以达到 1024 的倍数|
|`query_cache_wlock_invalidate`|控制当有写锁加在表上的时候，是否先让该表相关的 Query Cache 失效|

##### ** query_cache_type **
|值|解释|
|:---:|:----:|
|0(OFF)|关闭 Query Cache 功能，任何情况下都不会使用 Query Cache|	
|1(ON)|开启 Query Cache 功能，但是当 SELECT 语句中使用的 SQL_NO_CACHE 提示后，将不使用 Query Cache|	
|2(DEMAND)|开启 Query Cache 功能，但是只有当 SELECT 语句中使用了 SQL_CACHE 提示后，才使用 Query Cache|	


##### ** query_cache_wlock_invalidate 值选项 **
|值|解释|
|:---:|:----:|
|1(TRUE)|在写锁定的同时将使该表相关的所有 Query Cache 失效|	
|0(FALSE)|在锁定时刻仍然允许读取该表相关的 Query Cache|	



#### ** SQL_NO_CACHE **

select 语句中使用 `SQL_NO_CACHE` 的意义为 这次查询的结果不会被缓存，如果这条语句的结果之前已经被缓存过，那么还有可能将会之前的缓存结果返回。即使`query_cache_type` 为 ON 或 1 。

如果要重新测试，就在查询前先执行一下`FLUSH QUERY CACHE` or `RESET QUERY CACHE`。然后再带上SQL_NO_CACHE选项.

当然将`query_cache_size`设置为0,也是可以使查询结果不被缓存的。如果需要禁止缓存最好将`query_cache_type`与`query_cache_size`调整为0.参考这篇文章[MySQL为什么要关闭Query Cache？](http://www.ywnds.com/?p=7386)

************************
#### ** show status like '%Qcache%'; **

```
mysql> show status like '%Qcache%';
+-------------------------+----------+
| Variable_name           | Value    |
+-------------------------+----------+
| Qcache_free_blocks      | 1        |
| Qcache_free_memory      | 16760152 |
| Qcache_hits             | 0        |
| Qcache_inserts          | 0        |
| Qcache_lowmem_prunes    | 0        |
| Qcache_not_cached       | 1        |
| Qcache_queries_in_cache | 0        |
| Qcache_total_blocks     | 1        |
+-------------------------+----------+
```

|系统变量|解释|
|:---:|:----:|
|Qcache_free_blocks|表示查询缓存中目前还有多少剩余的blocks，如果该值显示较大，则说明查询缓存中的内存碎片过多了，可能在一定的时间进行整理。|
|Qcache_free_memory|查询缓存的内存大小，通过这个参数可以很清晰的知道当前系统的查询内存是否够用，是多了，还是不够用，DBA可以根据实际情况做出调整。|
|Qcache_hits|表示有多少次命中缓存。我们主要可以通过该值来验证我们的查询缓存的效果。数字越大，缓存效果越理想。|
|Qcache_inserts|表示多少次未命中然后插入，意思是新来的SQL请求在缓存中未找到，不得不执行查询处理，执行查询处理后把结果insert到查询缓存中。这样的情况的次数，次数越多，表示查询缓存应用到的比较少，效果也就不理想。当然系统刚启动后，查询缓存是空的，这很正常。|
|Qcache_lowmem_prunes|该参数记录有多少条查询因为内存不足而被移除出查询缓存。通过这个值，用户可以适当的调整缓存大小。|
|Qcache_not_cached|表示因为query_cache_type的设置而没有被缓存的查询数量|
|Qcache_queries_in_cache|当前缓存中缓存的查询数量|
|Qcache_total_blocks|当前缓存的block数量|
************************
### ** 是否需要缓存 **

##### ** 在实际生产中,是否需要开启QC,是根据业务决定的,不过很多场景下都是不需要开启的。**

Query Cache有如下规则，如果数据表被更改，那么和这个数据表相关的全部Cache全部都会无效，并删除之。这里“数据表更改”包括: INSERT, UPDATE, DELETE, TRUNCATE, ALTER TABLE, DROP TABLE, or DROP DATABASE等。举个例子，如果数据表posts访问频繁，那么意味着它的很多数据会被QC缓存起来，但是每一次posts数据表的更新，无论更新是不是影响到了cache的数据，都会将全部和posts表相关的cache清除。如果你的数据表更新频繁的话，那么Query Cache将会成为系统的负担。有实验表明，糟糕时，QC会降低系统13%的处理能力。

如果你的应用对数据库的更新很少，那么QC将会作用显著。比较典型的如博客系统，一般博客更新相对较慢，数据表相对稳定不变，这时候QC的作用会比较明显。如果数据库一共往QC中写入了约800W次缓存，但是实际命中的只有约500W次。也就是说，每一个缓存的使用率约为0.66次。很难说，该缓存的作用是否大于QC系统所带来的开销。但是有一点是很肯定的，QC缓存的作用是很微小的，如果应用层能够实现缓存，将可以忽略QC的效果。


************************
### ** 参考 **

[MySQL高速缓存启动方法及参数详解(query_cache_size)](https://blog.csdn.net/jshuanghua/article/details/53858490)
[Mysql SQL_NO_CACHE不生效的问题](http://www.dewen.net.cn/q/5149/Mysql)
[你真的会用mysql 的SQL_NO_CACHE吗？](http://www.liaodiantec.com/a/news/9665)
[MySQL-强制不使用缓存来测试查询速度？](https://cloud.tencent.com/developer/ask/43726)
[MySQL query_cache_type 详解](https://www.cnblogs.com/JiangLe/p/5337383.html)
[mysql 查询缓存 query_cache_type](https://blog.csdn.net/wmsjlihuan/article/details/16337685)
[MySql | 查询缓存笔记](https://segmentfault.com/a/1190000003039232)
[MySQL为什么要关闭Query Cache？](http://www.ywnds.com/?p=7386)

