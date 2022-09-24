---
title: MySQL 索引创建、删除和查看
tags: 
    - MySQL
categories: 
    - 数据库
    - MySQL
abbrlink: 32289
date: 2017-02-09 18:29:50
---

#### **1. 索引的作用**

   在索引列上，数据库利用各种各样的快速定位技术，能够大大的提高查询效率，特别是当数据量非常大和查询设计到多个表时，索引的利用能够将效率提高成千上万倍，当然要合理的利用索引。

#### **2. 创建索引**

​	在执行CREATE TABLE时可以创建索引，也可以在之后单独使用CREATE INDEX或ALTER TABLE来为表增加索引。

###### 2.1 ALTER TABLE

​	ALTER TABLE用来创建普通索引、UNIQUE索引或PRIMARY KEY索引。

```
ALTER TABLE tb_name ADD INDEX index_Name (column_list);
ALTER TABLE tb_name ADD UNIQUE (column_list);
ALTER TABLE tb_name ADD PRIMARY KEY (column_list);
```

​	tb_name 是要增加索引的表名，column_list 是要增加索引的列，多列用逗号隔开，index_Name 是可选，缺省为第一个索引列赋名称，ALTER TABLE允许在单个语句中更改多个表，因此可以也可以同时创建多个索引。

###### 2.2 CREATE INDEX

​	CREATE INDEX 可对表增加普通索引或者UNIQUE索引。

```
CREATE INDEX index_Name ON tb_name(column_list);
CREATE UNIQUE INDEX index_Name ON tb_name(column_list);
```

​	tb_name、index_Name和column_list具有ALTER TABLE语句中相同的含义，索引名称不可自定义，也不能创建PRIMARY KEY。

#### **3. 索引类型**

​	在创建索引时，可以规定索引能否包含重复的值，如果不包含，则索引应该为PRIMARY KEY或UNIQUE索引，对于单列唯一索引，这能保证单列不包含重复的值，对于多列唯一索引，保证多值的组合不重复。

​	PRIMAY KEY索引与UNIQUE索引非常类似，实际上PRIMAY KEY索引仅是一个具有名称PRIMAY的UNIQUE索引，这表示一个表只能包含一个PRIMAY KEY索引，因为一个表中不可能具有两个同名的索引。



#### **4. 删除索引**

​	可以使用ALTER TABLE或DROP INDEX语句来删除索引：

```
DROP INDEX index_Name On tb_name;
ALTER TABLE tb_Name DROP TABLE index_Name;
ALTER TABLE tb_Name DROP PRIMAY KEY;
```

​	第一条和第二条作用是一样的，删除tb_Name中index_Name索引；第三条仅适用于删除PRIMAY KEY时，因为一个只可能有一个PRIMAY KEY索引。

​	另外，如果在表中删除了某列，则索引会受到影响，对于多列组合的索引，如果删除其中某列，则该列也会在索引中删除，如果删除所有列，则该索引也会被删除。



#### **5. 查看索引**

```
mysql> show index from tb_name;
mysql> show keys from tb_name;
```

* Table : 表名
* Non_unique： 如果索引不能包含重复值为0，如果可以为1
* Key_name： 索引的名称
* Seq_in_index：索引中列的序号，从1开始
* Column_name： 列的名称
* Collation：列以什么方式存储在索引中，在MySQL中有值‘A’(升序)和NULL(无分类)
* Cardinality： 索引中唯一值的数量估计值，通过运行ANALYZE TABLE或者 myisamchk -a 可以更新，基数根据被存储的整数的统计数据来计数，所以，即使对于小型表，该值也没有必要是精确的，基数越大，当进行联合时，MySQL使用该索引的机会就越大。
* Sub_part： 如果列只是被部分编入，则为编入索引的字符数目，如果整列被编入索引，则为NULL
* Packed：关键字如何被压缩，没有压缩为NULL
* Null： 如果列含有NULL为YES，如果没有则为NO
* Index_type： 用过的索引方法，BTREE，FULLTEXT，HASH，RTREE
* Comment： 备注
