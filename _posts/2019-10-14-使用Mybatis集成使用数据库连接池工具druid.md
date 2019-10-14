---
layout:     post
title:      使用Mybatis集成使用数据库连接池工具druid
date:       2019-10-14
author:     codywsy
header-img: img/post-bg-mybatis.jpg
catalog: true
tags:
    - mybatis
    - java
---

> 记录首次使用Mybatis+druid访问mysql8.0

参考链接 [使用MyBatis集成阿里巴巴druid连接池（不使用spring）](https://www.cnblogs.com/helloIT/p/7676505.html)

### 环境
---
mysql 8.0.17

### 数据库
---

建立数据表和数据

```sql
CREATE DATABASE test default charset=utf8;

USE test;

CREATE TABLE `user` (
  `name` varchar(64) DEFAULT NULL,
  `age` int(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

insert  into `user`(`name`,`age`) values ('叶莜落',27),('张三丰',128);
```

### 坑
---

1. 根据maven工程的目录结构安放文件。例如配置文件之类的资源，需要放置在```src/main/resources```

2. 数据库使用了mysql 8.0+版本，所以对应的依赖和配置也需要升级
    - 驱动mysql-connector-java的版本需要使用8.0.*版本
    - 配置中的驱动drive值，由```com.mysql.jdbc.Driver```（mysql5.6+版本）升级成```com.mysql.cj.jdbc.Driver```（mysql8.0+版本）
    - 配置中的连接url需要加上useSSL和serverTimezone配置，即```jdbc:mysql://localhost:3306/test?useSSL=true&serverTimezone=GMT```
