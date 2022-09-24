---
title: SQL 对时间整点的处理
toc: true
author: samzong.lu
author_id: defaultAuthorId
language: en
tags:
  - MySQL
  - ClickHouse
categories:
  - 数据库
abbrlink: 55009
date: 2022-04-15 18:55:00
---
## 需要取值整点时间

项目上需要取值上一个整点的数据查询处理，落表，然后实现按小时更新

> ClickHouse

```sql
subtractHours(date_trunc('hour',now()),1)
```

> MySQL

```sql
and auth_time >= DATE_SUB(DATE_FORMAT(now(),'%Y-%m-%d %H:00:00'),interval 1 hour)
and auth_time < DATE_FORMAT(now(),'%Y-%m-%d %H:00:00')
```