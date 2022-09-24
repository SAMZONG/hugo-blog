# MySQL 开启慢日志优化


# 工欲善其事，必先利其器 -- mysql开启慢日志优化


### 慢查询日志
顾名思义就是记录查询比较慢得日志。


### 测试环境

* mysql-server 5.6
* CentOS 6.5
* VMware Fushion 8 pro


首先，第一部查看是否已经开启慢查询日志：

```
mysql> show variables like '%slow%';
+---------------------+---------------------------------+
| Variable_name       | Value                           |
+---------------------+---------------------------------+
| log_slow_queries    | OFF                             |
| slow_launch_time    | 2                               |
| slow_query_log      | OFF                             |
| slow_query_log_file | /var/run/mysqld/mysqld-slow.log |
+---------------------+---------------------------------+
4 rows in set (0.00 sec)

mysql>
```

打开慢查询日志。修改MySQL的配置文件my.cnf一般是在/etc目录下面，加上下面三行配置后重启MySQL。

```
slow_query_log = ON
slow_launch_time = 2
slow_query_log_file = /usr/local/mysql/data/slow_query.log

```
slow_launch_time只能精确到秒，如果需要更精确可以使用一些第三方的工具比如后面介绍的pt-query-digest

```
mysql> show variables like '%slow%';
+---------------------------+--------------------------------------+
| Variable_name             | Value                                |
+---------------------------+--------------------------------------+
| log_slow_admin_statements | OFF                                  |
| log_slow_slave_statements | OFF                                  |
| slow_launch_time          | 2                                    |
| slow_query_log            | ON                                   |
| slow_query_log_file       | /usr/local/mysql/data/slow_query.log |
+---------------------------+--------------------------------------+
5 rows in set (0.00 sec)

mysql>
```
> Tips: 我这里用的MySQL版本是5.6，不同版本的MySQL开启慢查询的配置是不同的，比如5.6之前的某些版本是long_query_time, long_query_time和log-slow-queries。可以先在终端执行show variables like '%slow%';查看下当前版本具体配置是什么。

也可以在终端中通过设置全局变量来打开慢查询日志：

```
set @@global.slow_query_log = ON;
```

### 保持慢查询日志到表中
MySQL支持将慢查询日志保存到mysql.slow_log这张表中。通过@@global.log_output可以设置默认为TABLE，FILE和TABLE只能同时使用一个。

```
mysql> select @@global.log_output;
+---------------------+
| @@global.log_output |
+---------------------+
| FILE                |
+---------------------+
1 row in set (0.00 sec)

mysql>
```

```
set @@global.log_output='TABLE';
```

```
mysql> show create table mysql.slow_log;
+----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
| Table    | Create Table                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
+----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
| slow_log | CREATE TABLE `slow_log` (
  `start_time` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  `user_host` mediumtext NOT NULL,
  `query_time` time NOT NULL,
  `lock_time` time NOT NULL,
  `rows_sent` int(11) NOT NULL,
  `rows_examined` int(11) NOT NULL,
  `db` varchar(512) NOT NULL,
  `last_insert_id` int(11) NOT NULL,
  `insert_id` int(11) NOT NULL,
  `server_id` int(10) unsigned NOT NULL,
  `sql_text` mediumtext NOT NULL,
  `thread_id` bigint(21) unsigned NOT NULL
) ENGINE=CSV DEFAULT CHARSET=utf8 COMMENT='Slow log' |
+----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
1 row in set (0.00 sec)

mysql>
```

我们可以用下列语句用来模仿慢查询；

```
select sleep(10);
```

```
mysql> select * from mysql.slow_Log
    -> ;
ERROR 1146 (42S02): Table 'mysql.slow_Log' doesn't exist
mysql> select *  from mysql.slow_log;
+---------------------+---------------------------+------------+-----------+-----------+---------------+----+----------------+-----------+-----------+------------------+-----------+
| start_time          | user_host                 | query_time | lock_time | rows_sent | rows_examined | db | last_insert_id | insert_id | server_id | sql_text         | thread_id |
+---------------------+---------------------------+------------+-----------+-----------+---------------+----+----------------+-----------+-----------+------------------+-----------+
| 2016-03-21 23:07:15 | root[root] @ localhost [] | 00:00:10   | 00:00:00  |         1 |             0 |    |              0 |         0 |         0 | select sleep(10) |         2 |
+---------------------+---------------------------+------------+-----------+-----------+---------------+----+----------------+-----------+-----------+------------------+-----------+
1 row in set (0.01 sec)

mysql>
```


### 慢查询日志分析
1. 可以使用MySQL自带的mysqldumpslow工具。使用很简单，可以跟-help来查看具体的用法。

```
# -s：排序方式。c , t , l , r 表示记录次数、时间、查询时间的多少、返回的记录数排序；
# ac , at , al , ar 表示相应的倒叙； # -t：返回前面多少条的数据；
# -g：包含什么，大小写不敏感的； mysqldumpslow -s r -t 10 /slowquery.log
#slow记录最多的10个语句 mysqldumpslow -s t -t 10 -g "left join" /slowquery.log
#按照时间排序前10中含有"left join"的
```

2. 可以导到mysql.slow_query表中，然后通过sql语句进行分析。
3. 使用第三方工具，下面会有介绍。


### pt-query-digest
pt-query-digest可以从普通MySQL日志，慢查询日志以及二进制日志中分析查询，甚至可以从SHOW PROCESSLIST和MySQL协议的tcpdump中进行分析，如果没有指定文件，它从标准输入流（STDIN）中读取数据。
最简单地用法如下：

```
pt-query-digest slow.logs
```

输出信息大致如下:

```

```































