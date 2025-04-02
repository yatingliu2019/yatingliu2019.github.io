+++
title = "SQL学习笔记"
author = "lyt"
date = "2023-12-26"
description = "A learning record of sqwl"
tags = [
    "mysql",
    "sql",
]
weight = 12
+++
> 课程链接：
> [【数据库】SQL 3小时快速入门 #数据库教程 #SQL教程 #MySQL教程 #database#Python连接数据库](https://www.bilibili.com/video/BV1PT4y1e7UU/?share_source=copy_web&vd_source=e1dd89dfeb5a2b320cd06a8ff9f19dc5)

## 一、SQL
### 1.**资料库管理系统**（Database Management System，简称DBMS）
是整理资料的软件。其主要功能包括数据的存储、检索、更新和删除，以及对数据进行安全性、完整性和一致性的管理。以下是资料库管理系统的一些重要特征和功能：

a. 数据定义语言（Data Definition Language，DDL）：用于定义数据库中的数据结构，包括表、字段、索引等。

b. 数据操作语言（Data Manipulation Language，DML）：用于对数据库中的数据进行增加、删除、修改和查询等操作。

c. 数据库查询语言（Database Query Language，如SQL）：用于向数据库发出查询请求，以检索所需的数据。

d. 数据库事务管理：确保数据库操作的原子性、一致性、隔离性和持久性，以支持并发访问和数据的完整性。

e. 数据库安全性管理：包括用户认证、授权和权限管理，以确保只有授权用户可以访问和操作数据库。

f. 数据备份与恢复：提供定期备份数据库的功能，并能够在需要时将数据库恢复到先前的状态。

g. 数据库性能优化：通过索引、查询优化、分区等技术提高数据库的性能和效率。

h. 数据库监控与管理：监控数据库的运行状态、性能指标和资源利用情况，并进行必要的管理和调整。


### 2.**SQL**（Structured Query Language，结构化查询语言）
是一种用于管理关系数据库系统的标准化语言。它允许用户定义、操作和管理数据库中的数据，以及执行各种数据库操作，如查询、插入、更新和删除数据等。具有以下几个主要方面的功能：

a. 数据查询（Query）：SQL允许用户通过使用SELECT语句从数据库中检索数据。SELECT语句可以根据用户的需求从一个或多个表中选择特定的列，并根据特定的条件过滤所需的行。

b. 数据操作（Manipulation）：SQL包括INSERT、UPDATE和DELETE语句，用于向数据库中添加、更新或删除数据。这些语句使用户能够对数据库中的数据进行修改，以保持数据的最新状态。

c. 数据定义（Definition）：SQL提供了一组用于定义数据库结构的语句，如CREATE TABLE、ALTER TABLE和DROP TABLE等。这些语句允许用户创建新表、修改现有表的结构，或删除不再需要的表。

d. 数据控制（Control）：SQL包括用于控制对数据库对象的访问权限的语句，如GRANT和REVOKE。这些语句允许数据库管理员管理用户对数据库的访问权限，以确保数据的安全性和完整性。

e. 事务控制（Transaction Control）：SQL支持事务处理，通过BEGIN TRANSACTION、COMMIT和ROLLBACK等语句，允许用户在数据库中执行一系列操作，并将它们作为一个原子单元进行提交或回滚。


## 二、基础
### 1.安装：
环境：Windows系统，官网链接: [MySQL Community Downloads](https://dev.mysql.com/downloads/windows/installer/8.0.html链接)

### 2.table and keys：
主键和外键

### 3.创建资料库：
关于database：
```sql
-- 创建 指定数据库
CREATE DATABASE `sq_tutroial`;
-- 显示 所有的数据库
SHOW DATABASES;
-- 丢掉 指定数据库
DROP DATABASE `sq_tutroial`;
-- 使用 指定数据库
USE `sq_tutroial`;
```

关于table：
```sql
-- 创建 指定表格
CREATE TABLE `student`(
	`student_id` INT PRIMARY KEY AUTO_INCREMENT,
    `name` VARCHAR(20) NOT NULL,
    `major` VARCHAR(20) UNIQUE
    );
-- 描述 指定表格的结构
DESCRIBE TABLE `student`;
-- 删除 指定表格
DROP TABLE `student`;
-- 返回 指定表格所有数据
SELECT * FROM `student`;
-- 修改 指定表格数据 添加
ALTER TABLE `student` ADD gpa DECIMAL(3,2);
```

关于数据格式：
```sql
-- 格式
INT				-- 整数
DECIMAL(m,n)	-- 有小数点的数
VARCHAR(n)		-- 字串
BLOB			-- （Binary Large Object）图片 影片 档案...
DATE			-- 'YYYY-MM-DD'
TIMESTAMP		-- 'YYYY-MM-DD HH:MM:SS'
```


## 三、实例

> 注意：先创建主体的 Employee 和 Branch 表格，再补上 Employee 的 branch_id的foreign key设定，∵有创建顺序，后者的主键是前者的外键

### 1.创建
```sql
-- 创建公司表格资料库
CREATE DATABASE `sq_test`;
USE `sq_test`;
SET SQL_SAFE_UPDATES = 0;
```

```sql
-- 创建 employee 和 branch 表格
CREATE TABLE `employee` (
	`emp_id` INT PRIMARY KEY,
    `name` VARCHAR(20),
    `birth_date` DATE,
    `sex` VARCHAR(1),
    `salary` INT,
    `branch_id` INT,
    `sup_id` INT
    );
CREATE TABLE `branch` (
	`branch_id` INT PRIMARY KEY,
    `branch_name` VARCHAR(20),
    `manager_id` INT,
    FOREIGN KEY (`manager_id`) REFERENCES `employee`(`emp_id`) ON DELETE SET NULL
    );
```

```sql
-- 补上foreign key的设定
ALTER TABLE `employee`
ADD FOREIGN KEY(`branch_id`)
REFERENCES `branch`(`branch_id`)
ON DELETE SET NULL;
ALTER TABLE `employee`
ADD FOREIGN KEY(`sup_id`)
REFERENCES `employee`(`emp_id`)
ON DELETE SET NULL;
```

```sql
-- 创建 client 和 works_with 表格
CREATE TABLE `client` (
	`client_id` INT PRIMARY KEY,
    `client_name` VARCHAR(20),
    `phone` VARCHAR(20)
    );
    
CREATE TABLE `works_with` (
	`emp_id` INT,
    `client_id` INT,
    `total_sales` INT,
    PRIMARY KEY(`emp_id`, `client_id`),
    FOREIGN KEY(`emp_id`) REFERENCES `employee`(`emp_id`) ON DELETE CASCADE,
    FOREIGN KEY(`client_id`) REFERENCES `client`(`client_id`) ON DELETE CASCADE
    );
```

```sql
-- 增加部门资料
INSERT INTO `branch` VALUES(1, '研发', 206);
INSERT INTO `branch` VALUES(2, '行政', 207);
INSERT INTO `branch` VALUES(3, '咨询', 208);

-- 增加员工资料
INSERT INTO `employee` VALUES(206, '小黄', '1998-10-08', 'F', 50000, 1, NULL);
INSERT INTO `employee` VALUES(207, '小绿', '1985-09-16', 'M', 29000, 2, 206);
INSERT INTO `employee` VALUES(208, '小黑', '2000-12-19', 'M', 35000, 3, 206);
INSERT INTO `employee` VALUES(209, '小白', '1997-01-22', 'F', 39000, 3, 207);
INSERT INTO `employee` VALUES(210, '小蓝', '1925-11-10', 'F', 84000, 1, 207);

-- 增加客户资料
INSERT INTO `client` VALUES(400,'阿狗','254354335');
INSERT INTO `client` VALUES(401,'阿猫','25633899');
INSERT INTO `client` VALUES(402,'旺来','45354345');
INSERT INTO `client` VALUES(403,'露西','54354365');
INSERT INTO `client` VALUES(404,'艾瑞克','18783783');

-- 增加合作资料
INSERT INTO `works_with` VALUES(206,400,'70000');
INSERT INTO `works_with` VALUES(207,401,'24000');
INSERT INTO `works_with` VALUES(208,400,'9800');
INSERT INTO `works_with` VALUES(208,403,'24000');
INSERT INTO `works_with` VALUES(210,404,'87940');
```

### 2.练习：

```sql
-- 1.取得所有员工的资料
SELECT * FROM `employee`;
-- 2.取得所有客户的资料
SELECT * FROM `client`;
-- 3.按照薪水低到高取得员工资料
SELECT * FROM `employee` ORDER BY `salary`;
-- 4.取得薪水前3高的员工的资料
SELECT * FROM `employee` ORDER BY `salary` DESC LIMIT 3;
-- 5.取得所有员工的名字
SELECT * FROM `employee` ORDER BY `name`;
```

```sql
-- aggregate function 聚合函数
-- 1.取得员工人数
SELECT COUNT(*) FROM `employee`;
-- 2.取得所有出生于1970-01-01之后的女性员工人数 
SELECT COUNT(*) FROM `employee` 
WHERE `birth_date` > '1970-01-01' AND `sex` = 'F';
-- 3.取得所有员工的平均薪水 
SELECT AVG(`salary`) FROM `employee`;
-- 4.取得所有员工薪水的总和 
SELECT SUM(`salary`) FROM `employee`;
-- 5.取得薪水最高的员工 
SELECT MAX(`salary`) FROM `employee`;
-- 6.取得薪水最低的员工
SELECT MIN(`salary`) FROM `employee`;
```

```sql
-- wildcards 万用子元  % 代表多个子元， _ 代表一个子元
-- 1.取得电话号码尾数是355的客户
SELECT * FROM `client` 
WHERE `phone` LIKE '%335';
-- 取得电话号码开头是123的客户
-- SELECT * FROM `client` WHERE `phone` LIKE '123%';
-- 取得电话号码包含是123的客户
-- SELECT * FROM `client` WHERE `phone` LIKE '%123%';
-- 2.取得姓艾的客户
SELECT * FROM `client` 
WHERE `client_name` LIKE '艾%';
-- 3.取得生日在12月的员工
SELECT * FROM `employee` 
WHERE `birth_date` LIKE '_____12%';
```

```sql
-- union 联合查询 并集
-- 1.员工名字 union 客户名字 1+1 同属性
SELECT `name` FROM `employee` 
UNION 
SELECT `client_name` FROM `client`;
-- 2.员工id + 员工名字 union 客户id + 客户名字
SELECT `emp_id` AS `total_id`, `name` AS `total_name` FROM `employee` 
UNION 
SELECT `client_id`, `client_name` FROM `client`;
-- 3.员工薪水 union 销售金额
SELECT `salary` AS `total_salary` FROM `employee` 
UNION 
SELECT `total_sales` FROM `works_with`;
```

```sql
-- join 连接
INSERT INTO `branch` VALUES(4, '偷懒', NULL);
-- 取得所有部门经理的名字
SELECT `employee`.`emp_id`, `employee`.`name`, `branch`.`branch_name` 
FROM `employee` LEFT JOIN `branch` 
ON `employee`.`emp_id` = `branch`.`manager_id`;
-- 不论 on 的条件成立与否,左面的表格都会回传全部资料,只有条件成立右边的表格才会回传资料,其他则是NULL
-- SELECT `employee`.`emp_id`, `employee`.`name`, `branch`.`branch_name` 
-- FROM `employee` RIGHT JOIN `branch` 
-- ON `employee`.`emp_id` = `branch`.`manager_id`;
```

```sql
-- subquery 子查询
-- 1.找出研发部门的经理名字
SELECT `name` FROM `employee` WHERE `emp_id` = (
	SELECT `manager_id` FROM `branch` WHERE `branch_name` = '研发'
);
-- 2.找出对单一位客户销售金额超过50000的员工的名字
SELECT `name` FROM `employee` WHERE `emp_id` IN (
	SELECT `emp_id` FROM `works_with` WHERE `total_sales` > 50000 
);
-- 因为超过两笔 所以用 IN
```

```sql
-- on delete
-- 	ON DELETE  SET NULL
-- CREATE TABLE `branch` (
-- 	`branch_id` INT PRIMARY KEY,
--     `branch_name` VARCHAR(20),
--     `manager_id` INT,
--     FOREIGN KEY (`manager_id`) REFERENCES `employee`(`emp_id`) ON DELETE SET NULL
--     );
-- manager_id 对应的 emp_id 被删掉了 就把manager_id设为NULL
--	 ON DELETE CASCADE 级联删除
-- CREATE TABLE `works_with` (
-- 	`emp_id` INT,
--     `client_id` INT,
--     `total_sales` INT,
--     PRIMARY KEY(`emp_id`, `client_id`),
--     FOREIGN KEY(`emp_id`) REFERENCES `employee`(`emp_id`) ON DELETE CASCADE,
--     FOREIGN KEY(`client_id`) REFERENCES `client`(`client_id`) ON DELETE CASCADE
--     );
-- CASCADE针对左表关联列为首要键所在的列，且由于首要键列不得为NULL，所以采取CASCADE的清空本行的
-- 如果某一个值同时是primary key 或者 foreign key就不能用ON DELETE SET NULL
```

### 3.sql连接python：
选用：Vscode，终端安装包：`pip install mysql-connector-python`，打开Vscode，

```python
import mysql.connector
```
打开指定的连接
```python
connection = mysql.connector.connect(
    host='localhost',
    port='3306',
    user='root',
    password='密码',
    database='指定的database名字'
)
cursor = connection.cursor()
```

```python
# 创建资料库
cursor.execute("CREATE DATABASE `指定的table名字`;")
```

```python
# 取得所有资料库名称
cursor.execute("SHOW DATABASES;")
records = cursor.fetchall()
for r in records:
    print(r)
```

```python
# 选择资料库
cursor.execute("USE `指定的资料库名字`;")
```

```python
# 创建表格
cursor.execute("CREATE TABLE `指定的database名字`(指定的database名字 INT);")
```

```python
# 查看`branch`表里面数据
cursor.execute("SELECT * FROM `branch`;")
records = cursor.fetchall()
for r in records:
    print(r)
```

```python
# 新增 table 数据
cursor.execute("INSERT INTO `branch` VALUES(5, 'qq', NULL);")
```

```python
# 修改 table 数据
cursor.execute("UPDATE `branch` SET `manager_id = NULL WHERE `branch_id` = 4;")
```

```python
# 删除 table 数据
cursor.execute("DELETE FROM `branch` WHERE `branch_id` = 5;")
cursor.close()
connection.commit() #改动资料就要加上这一句
connection.close()
```
