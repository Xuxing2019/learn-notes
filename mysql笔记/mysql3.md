对于表的操作：

> **修改表**

```sql
--修改表的名称 ALTER TABLE 旧的表名 RENAME AS 新的表名
ALTER TABLE teacher RENAME AS teacher1
--增加表的字段  ALTER TABLE 表名 ADD 字段名 属性
ALTER TABLE TEACHER1 ADD workage INT(4)

--修改表的字段约束(修改约束！）ALTER TABLE 表名 MODIFY 字段 新约束
ALTER TABLE teacher1 MODIFY age VARCHAR(11)--modify修改字段的约束 把age是int类型改成VARCGAR
--修改表的字段名称（重命名）ALTER TABLE 表名 CHANGE 旧表名 新表名 约束 
ALTER TABLE teacher1 CHANGE age age1 int(3) --change修改表的字段名称（重命名）
--modify和change区别：modify是修改字段的约束，change是给字段重命名

--删除表的字段   ALTER TABLE 表名 DROP 字段名
ALTER TABLE teacher1 DROP workage
```

>**删除表**

```sql
--删除表
DROP TABLE teacher1
--如果表存在就删除（如果表存在再删除）
DROP TABLE IF EXISTS teacher1
```

**注：**所有的创建跟删除操作尽量加上判断(IF EXISTS)，以免报错~

**注意点：**

- `` 字段名使用这个括起来(Tab上面的符号)
- 注释 --/**/
- sql关键字不区分大小写
- 所有符号用英文

#### 3.Mysql中的数据管理：

**1.外键**（了解即可）

>方式一，在创建表的时候，增加约束（麻烦比较复杂）

先创建gread表：

```sql
CREATE TABLE `gread`(
   `gradeid` INT(10) NOT NULL AUTo_INCREMENT COMMENT '年级id',
	 `gradname` VARCHAR(50) NOT NULL COMMENT '年级名称',
	PRIMARY KEY (`gradeid`)
	 )ENGINE=INNODB DEFAULT CHARSET=utf8
```

student与gradeid关联起来

```sql
CREATE TABLE IF NOT EXISTS `student`(
  `id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
	`name` VARCHAR(30) NOT NULL DEFAULT '匿名' COMMENT '姓名',
	`pwd`VARCHAR(45) NOT NULL DEFAULT '123' COMMENT '密码',
   `gender` VARCHAR(2) NOT NULL DEFAULT '女' 	COMMENT '性别',
	`birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
	 `gradeid` INT(10) NOT NULL COMMENT '学生的年级', 
	`address` VARCHAR(100) DEFAULT NULL COMMENT'家庭住址',
	`email` VARCHAR(50)  DEFAULT NULL COMMENT'邮箱',
	PRIMARY KEY (`id`),
	KEY `FK_gradeid`(`gradeid`),
	CONSTRAINT `FK_gradeid` FOREIGN KEY (`gradeid`) REFERENCES `gread`(`gradeid`)
	)ENGINE=INNODB DEFAULT CHARSET=utf8
--定义外键：KEY `FK_gradeid`(`gradeid`) 
--给这个外键添加约束(执行引用) references 引用   加入引用表名称gread
```

定义外键：KEY `FK_gradeid`(`gradeid`) 
给这个外键添加约束(执行引用) references 引用   加入引用表名称gread

注：删除有外键关系的表的时候，必须要先删除引用别人的表（从表），再删除引用表（主表）

方式二：

> 创建表成功之后，添加外键约束
>
> 公式：ALTER TABLE 表 ADD CONSTRAINT 约束名 FOREIGN KEY(作为外键的列) REFERENCES 那个表(那个字段);

```sql
la
CREATE TABLE `gread`(
   `gradeid` INT(10) NOT NULL AUTo_INCREMENT COMMENT '年级id',
	 `gradname` VARCHAR(50) NOT NULL COMMENT '年级名称',
	PRIMARY KEY (`gradeid`)
	 )ENGINE=INNODB DEFAULT CHARSET=utf8
	 

CREATE TABLE IF NOT EXISTS `student`(
  `id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
	`name` VARCHAR(30) NOT NULL DEFAULT '匿名' COMMENT '姓名',
	`pwd`VARCHAR(45) NOT NULL DEFAULT '123' COMMENT '密码',
   `gender` VARCHAR(2) NOT NULL DEFAULT '女' 	COMMENT '性别',
	`birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
	 `gradeid` INT(10) NOT NULL COMMENT '学生的年级', 
	`address` VARCHAR(100) DEFAULT NULL COMMENT'家庭住址',
	`email` VARCHAR(50)  DEFAULT NULL COMMENT'邮箱',
	PRIMARY KEY (`id`)
	)ENGINE=INNODB DEFAULT CHARSET=utf8

--创建表的时候没有外键关系 
--公式：ALTER TABLE 表 ADD CONSTRAINT 约束名 FOREIGN KEY(作为外键的列) REFERENCES 那个表(那个字段);
ALTER TABLE `student`
ADD CONSTRAINT `FK_gradeid` FOREIGN KEY(`gradeid`) REFERENCES `gread`(`gradeid`);
--CONSTRAINT 添加约束， 外键是gradeid ， REFERENCES引用表gread 字段`gradeid`
```

--CONSTRAINT 添加约束， 外键是gradeid ， REFERENCES引用表gread 字段`gradeid`

**注：**以上操作都是物理外键，不建议使用！（避免避免数据库过多造成困扰，这里了解即可）

最佳方式：

数据库就是单纯的表，只用来存数据，只有行（数据）和列（字段）

我们想使用多张表的数据，想用外键（程序去实现）



下面转载于 https://www.cnblogs.com/shadowdoor/p/9097361.html 

# 数据库建表，该不该使用外键？

**一：使用外键**

优点：

（1）实现表与关联表之间的数据一致性；

（2）可以迅速的建立一个可靠性非常高的数据库结构，而不用让应用程序层去做过多的检查；

（3）可以提高系统鲁棒性、健壮性；

（4）可以实现开发人员和数据库设计人员的分工；

 

　　缺点：

（1）数据库需要维护外键的内部管理；

（2）外键等于把数据的一致性事务实现，全部交给数据库服务器完成；

（3）有了外键，当做一些涉及外键字段的增，删，更新操作之后，需要触发相关操作去检查，而不得不消耗资源；

（4）外键还会因为需要请求对其他表内部加锁而容易出现死锁情况；

（5）容易出现数据库I/O的瓶颈；

 

 

 

**二：不使用外键**

优点：

（1）减少了数据库表与表之间各种关联的复杂性；

（2）牺牲应用服务器资源，换取数据库服务器的性能；

（3）将主动权把控在自己手里；

（4）去掉外键相当于优化数据库性能；

 

　　缺点：

（1）所有外键的约束，需要自己在逻辑层自己实现；

（2）会出现数据错误覆写，错误数据进库的情况；

（3）消耗了服务器的性能；

（4）业务层里夹带持久层特性，耦合；

 

 

**总结：**

1. 互联网行业：不推荐使用外键。

　　　　理由：1）用户量大，并发度高，为此数据库服务器很容易成为性能瓶颈，尤其受IO能力限制，且不能轻易地水平扩展；

　　　　　　　2）若是把数据一致性的控制放到事务中，即让应用服务器承担此部分的压力；

　　　　　　  3）应用服务器一般都是可以做到轻松地水平的伸缩；

 

2. 传统行业：可以使用。

　理由：1）软件应用的人数有限，换句话说是可控的；

　　　　2  数据库服务器的数据量也一般不会超大，且活跃数据有限；

 

**2.DML语言（全部记住并且背下来）**

***\*博客到此，分享一下我学习编程的途径希望大家循序渐进，共同进步：\****

[How2J 的 Java教程](https://how2j.cn?p=80103)：当下Java小白的引路人，以有趣和好理解的方式展示Java和Web的内容拥有当今流行的java路线。

[哔哩哔哩 (゜-゜)つロ 干杯~-bilibili](https://www.bilibili.com/)：中国最大的学习平台没有之一，拥有海量的资源有时间的小伙伴可以免去重金花钱培训。

[廖雪峰的官方网站](https://www.liaoxuefeng.com)：**廖雪峰**,十年软件开发经验,业余产品经理,精通Java/Python/Ruby/Scheme/Objective C等,对开源框架有深入研究..

 

[菜鸟教程 - 学的不仅是技术,更是梦想!](https://www.runoob.com/)：提供了编程的基础技术教程, 介绍了HTML、CSS、Javascript、Python,Java,Ruby,C,PHP , MySQL等各种编程语言的基础知识。