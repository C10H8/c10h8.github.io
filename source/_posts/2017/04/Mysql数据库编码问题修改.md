---
title: Mysql数据库编码问题修改
date: 2017-04-05 13:19:10
categories: Mysql
tags: [mysql,编码]
---

- - -
<!--more-->
Mysql数据库编码问题修改
---


## 1.问题描述
```

问题： 当向新建的表中插入数据时（包含中文的数据），发现  ERROR 1366 (HY000): Incorrect string value: '\xE8\xAF\x8
```

## 2.查看字符编码问题

```
$mysql> show create table Deals\G
*************************** 1. row ***************************
       Table: Deals
Create Table: CREATE TABLE `Deals` (
  `id` int(4) NOT NULL AUTO_INCREMENT,
  `date` date DEFAULT NULL,
  `code` int(4) DEFAULT NULL,
  `name` varchar(128) DEFAULT NULL,
  `price` double(16,2) DEFAULT NULL,
  `num` double(16,2) DEFAULT NULL,
  `totalPrice` double(16,2) DEFAULT NULL,
  `buyer` varchar(255) DEFAULT NULL,
  `seller` varchar(255) DEFAULT NULL,
  `type` varchar(128) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT CHARSET=latin1
1 row in set (0.00 sec)
```
* 通过看表的字符，发现创建表使用的是latin1编码，这就是问题的关键

## 3.查看数据库配置编码

```
mysql> SHOW VARIABLES LIKE 'character%';
+--------------------------+---------------------------------------------------------+
| Variable_name            | Value                                                   |
+--------------------------+---------------------------------------------------------+
| character_set_client     | utf8                                                    |
| character_set_connection | latin1                                                  |
| character_set_database   | latin1                                                  |
| character_set_filesystem | binary                                                  |
| character_set_results    | utf8                                                    |
| character_set_server     | latin1                                                  |
| character_set_system     | utf8                                                    |
| character_sets_dir       | /usr/local/mysql-5.7.16-osx10.11-x86_64/share/charsets/ |
+--------------------------+---------------------------------------------------------+
8 rows in set (0.03 sec)
```

* 通过这个配置，可以看出，`character_set_connection`,`character_set_database`, `character_set_server`  这几个配置都是`latin1`编码。
* 配置如下

	```
	mysql> SET character_set_client = utf8 ;
	mysql> SET character_set_connection = utf8 ;
	mysql> SET character_set_database = utf8 ;
	mysql> SET character_set_results = utf8 ;
	mysql> SET character_set_server = utf8 ;
	mysql> SET collation_connection = utf8 ;
	mysql> SET collation_database = utf8 ;
	mysql> SET collation_server = utf8 ;	
	修改完成后，我重启了应用，再次提交中文，搞定了！
	```
	
## 4.然而这样并没有解决问题
对于现在已经创建的表格，字符依然是latin1，所以需要修改表的字符编码

* 查看数据库编码：

   ```
	SHOW CREATE DATABASE db_name;
	mysql>  SHOW CREATE DATABASE BigDeal;
+----------+--------------------------------------------------------------------+
| Database | Create Database                                                    |
+----------+--------------------------------------------------------------------+
| BigDeal  | CREATE DATABASE `BigDeal` /*!40100 DEFAULT CHARACTER SET latin1 */ |
+----------+--------------------------------------------------------------------+
   ```
* 查看表编码：

   ```
	SHOW CREATE TABLE tbl_name;
	mysql> SHOW CREATE TABLE Deals\G
*************************** 1. row ***************************
       Table: Deals
Create Table: CREATE TABLE `Deals` (
  `id` int(4) NOT NULL AUTO_INCREMENT,
  `date` date DEFAULT NULL,
  `code` int(4) DEFAULT NULL,
  `name` varchar(128) DEFAULT NULL,
  `price` double(16,2) DEFAULT NULL,
  `num` double(16,2) DEFAULT NULL,
  `totalPrice` double(16,2) DEFAULT NULL,
  `buyer` varchar(255) DEFAULT NULL,
  `seller` varchar(255) DEFAULT NULL,
  `type` varchar(128) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=43 DEFAULT CHARSET=utf8
1 row in set (0.00 sec)
   ```
* 查看字段编码：

	```
	SHOW FULL COLUMNS FROM tbl_name;
	mysql> SHOW FULL COLUMNS FROM Deals;
	```
   
* 把表默认的字符集和所有字符列（CHAR,VARCHAR,TEXT）改为新的字符集（和下面的区别，把默认修改为新的字符集）：

   ```
	ALTER TABLE tbl_name CONVERT TO CHARACTER SET character_name [COLLATE ...]
	如：ALTER TABLE logtest CONVERT TO CHARACTER SET utf8 COLLATE utf8_general_ci;
   ```

* 只是修改表的默认字符集(修改默认)：

   ``` 
	ALTER TABLE tbl_name DEFAULT CHARACTER SET character_name [COLLATE...];
	如：ALTER TABLE logtest DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
   ```
* 修改字段的字符集：
   
   ```   
	ALTER TABLE tbl_name CHANGE c_name c_name CHARACTER SET character_name [COLLATE ...];
    如：ALTER TABLE logtest CHANGE title title VARCHAR(100) CHARACTER SET utf8 COLLATE utf8_general_ci;
   ```

## 参考
* [mysql修改表、字段、库的字符集](http://fatkun.com/2011/05/mysql-alter-charset.html)
* [MySQL相关的中文编码错误解决](http://blog.sina.com.cn/s/blog_673faff10100qbyh.html)
 

