MySQL是一个**[关系型数据库管理系统](https://baike.baidu.com/item/关系型数据库管理系统/696511)****，**由瑞典MySQL AB 公司开发，属于 [Oracle](https://baike.baidu.com/item/Oracle) 旗下产品。MySQL 是最流行的[关系型数据库管理系统](https://baike.baidu.com/item/关系型数据库管理系统/696511)之一，在 WEB 应用方面，MySQL是最好的 [RDBMS](https://baike.baidu.com/item/RDBMS/1048260) (Relational Database Management System，关系数据库管理系统) 应用软件之一。

![img](https://img2020.cnblogs.com/i-beta/1953455/202003/1953455-20200313110724986-991783316.png)

 

 

 

一，数据库列的类型：
数值：
tinyint 十分小的类型 1个字节
smallint 较小的数据 2个字节
**int      存放整数   4个字节（常用的）相当于Java的int**
bigint   较大的数据 8个字节 相当于Java的long类型
float    浮点数    4个字节
double  浮点数    8个字节 （精度问题）
**decimal 字符串形式的浮点数  计算金融计算的时候，一般使用decimal**

 

字符串：
char 字符串固定大小 0~255
**varchar  可变字符串 0~65535  （常用的）相当于Java的String类**
tinytext 微型文本  2^8-1(二的八次方见一) 可以用来写一偏博客
text    文本串    2^16-1 （保存大的文本相当于一本书）

 

时间日期： Java中 java.util.Date
date  YYY-MM-DD,日期 年月日
time   HH:mm:ss 时间格式 十分秒
**datetime YYY-MM-DD HH:MM:SS 年月日十分秒 （最常用的时间格式）**
**timestamp 时间戳， 1970.1.1到现在的毫秒数！(也是比较常用的)**
year 年份表示


null：
没有值，未知
注：不要用null进行运算，结果为null

 

二，数据库的字段属性（重点）

Unsigned:
无符号的整数
声明了该列不能声明负数


zerofill：
0填充
就是不足的位数，使用0来填充，int（3）填一个5 变为 ：005

 


自增：
通常理解为自增，自动在上一条记录的基础上+1（默认）
通常用来设计主键~index，必须是整数类型
可以自定义设置主键的自增的初始值和步长

 


非空：NULL not null
假设设置为not null ，如果不进行给他赋值，就会报错！
NULL，不写值，默认就是null！

**演示：**

默认:
设置默认值！
gender，默认值男 ，如果不指定该列的值，则会有默认值男！

```sql
CREATE TABLE `shcool`.`student`  (
  `id` int(15) ZEROFILL NOT NULL,               
  `name` varchar(10) NULL,
  `age` varchar(2) NULL DEFAULT "男",
  PRIMARY KEY (`id`)
);  --ZEROFILL:填充0主键填充零  --PRIMARY KEY (`id`)  id设置为主键，主键一般一张表只有一个所有放最后面就知道这张表的主键是什么了   --DEFAULT "男"设置默认值为男
```

演示二：

```sql
--创建shcool数据库
CREATE DATABASE `shcool` CHARACTER SET 'utf8' COLLATE 'utf8_general_ci'

--创建一个student表(列，字段)使用sql创建
--学号int 登录密码varchar(30),性别varchar(2) ,出生年月(datetime)家庭住址，Email
--注意点，使用英文的(),表的名称字段，尽量使用``(Tab键上面)括起来因为很有可能你创建的字段变为关键字了
--所有的语句后面加,(英文的)最后一个字段不用加
USE `school`;
CREATE TABLE IF NOT EXISTS `student`(
  `id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
    `name` VARCHAR(30) NOT NULL DEFAULT '匿名' COMMENT '姓名',
    `pwd`VARCHAR(45) NOT NULL DEFAULT '123' COMMENT '密码',
   `gender` VARCHAR(2) NOT NULL DEFAULT '女'     COMMENT '性别',
    `birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
    `address` VARCHAR(100) DEFAULT NULL COMMENT'家庭住址',
    `email` VARCHAR(50)  DEFAULT NULL COMMENT'邮箱',
    PRIMARY KEY (`id`)
    )ENGINE=INNODB DEFAULT CHARSET=utf8----AUTO_INCREMENT：默认在原来的数据自动+1----PRIMARY KEY (`id`)：id设置为主键  一般放在表的字段最后面，通常情况每个表只有一个主键这样更加可观。
```

可以看出他们的格式是：

格式：
1.
CREATE TABLE IF NOT EXISTS `表名`(
    `字段名` 列类型  [属性] [索引] [注释],
    `字段名` 列类型 [属性] [索引] [注释],
   '字段名' 列类型 [属性] [索引] [注释],
    .....
  '字段名' 列类型 [属性] [索引] [注释]

) [表类型][表字符集设置] [注释]



拓展：

阿里巴巴规范手册中：每一个表，都必须存在以下的字段！表示一个记录存在的意义
id ：主键
version 做乐观锁的
is_delete 伪删除
gmt_create 创建时间
gmt_update 修改时间

 

 

**博客到此，分享一下我学习编程的途径希望大家循序渐进，共同进步：**

[How2J 的 Java教程](https://how2j.cn/?p=80103)：当下Java小白的引路人，以有趣和好理解的方式展示Java和Web的内容拥有当今流行的java路线。

[哔哩哔哩 (゜-゜)つロ 干杯~-bilibili](https://www.bilibili.com/)：中国最大的学习平台没有之一，拥有海量的资源有时间的小伙伴可以免去重金花钱培训。

[廖雪峰的官方网站](https://www.liaoxuefeng.com/)：*廖雪峰*,十年软件开发经验,业余产品经理,精通Java/Python/Ruby/Scheme/Objective C等,对开源框架有深入研究..

 

[菜鸟教程 - 学的不仅是技术,更是梦想!](https://www.runoob.com/)：提供了编程的基础技术教程, 介绍了HTML、CSS、Javascript、Python,Java,Ruby,C,PHP , MySQL等各种编程语言的基础知识。