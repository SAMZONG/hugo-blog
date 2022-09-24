# 每日备份MySQL单表数据


最近愈近年底，客户业务涉及对账操作，所以同事提出需求需要单独备份某张表数据，并且每日备份；思考之后解决办法如下：

1. mysqldump导出单张表的表结构及数据
2. 新增数据库，专做临时每日数据备份库
3. 导入该表数据到新增数据库内
4. 重命名导入的表名（预防计划任务下次导入时数据覆盖）
5. 编写脚本，添加Linux计划任务



#### 1. mysqldump导出但张表的表结构及数据

```
mysqldump -h dbServer -PdbServerPort -u db_user -p -d dbName tbName > tbName.sql
```



#### 2. 新增数据库，专做临时每日数据备份库

```
# loginTo your DBserver
mysql> create database bakdbName character set utf8;
```



#### 3. 导入该表数据到新增数据库内

```
mysql -h dbServer -P dbServerPort -u db_user -p bakdbName < tbName.sql
```



#### 4 . 重命名导入的表名

```
mysql -u db_user -p -e "rename table bakdbName.tbName to bakdbName.tbName_$DATE"
```



#### 5. 编写脚本



```
[root@testServer01 ~]# cat /usr/local/bin/bakTable.sh
#!/bin/bash

#Create by SAMZONG

DATE=`date +%Y%m%d`
TMPDIR=/tmp/baksql

# modify your DB configure
DBSERVER1=localhost
DBSERVER1_PORT=3306
DBSERVER1_USER=root
DBSERVER1_PASSWORD=password
MASTER_DBNAME=zabbix
MASTER_TBNAME=users

DBSERVER2=localhost
DBSERVER2_PORT=3306
DBSERVER2_USER=root
DBSERVER2_PASSWORD=password
BAKDBNAME=z3

# creat tmp folder
if [ ! -d $TMPDIR ]; then
	mkdir $TMPDIR
fi

# dump tbName
mysqldump -h $DBSERVER1 -P $DBSERVER1_PORT -u $DBSERVER1_USER -p"$DBSERVER1_PASSWORD" -d $MASTER_DBNAME  $MASTER_TBNAME > $TMPDIR/$MASTER_TBNAME.sql


# insert tbNAME to bakdbName
if [ $? -eq 0  ]; then
	mysql -h $DBSERVER2 -P $DBSERVER2_PORT -u $DBSERVER2_USER -p"$DBSERVER2_PASSWORD" $BAKDBNAME < $TMPDIR/$MASTER_TBNAME.sql

	if [ $? -eq 0 ]; then
		# rename tbName
		mysql -h $DBSERVER2 -P $DBSERVER2_PORT -u $DBSERVER2_USER -p"$DBSERVER2_PASSWORD" -e "rename table "$BAKDBNAME"."$MASTER_TBNAME" to "$BAKDBNAME"."$MASTER_TBNAME"_"$DATE";"
	fi

fi
```



#### 6. 添加到Linux计划任务

```
00 00 * * * /usr/local/bin/bakTable.sh
```


