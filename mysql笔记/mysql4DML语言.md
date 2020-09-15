### DML语言重要需要背下来：



**一，添加**（insert）

> insert



```sql
--创建gread表与stdent表
CREATE TABLE `gread` (
  `gradeid` int(10) NOT NULL AUTO_INCREMENT COMMENT '年级id',
  `gradname` varchar(50) NOT NULL COMMENT '年级名称',
  PRIMARY KEY (`gradeid`)
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8

--student表
CREATE TABLE `student` (
  `id` int(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
  `name` varchar(30) NOT NULL DEFAULT '匿名' COMMENT '姓名',
  `pwd` varchar(45) NOT NULL DEFAULT '123' COMMENT '密码',
  `gender` varchar(2) NOT NULL DEFAULT '女' COMMENT '性别',
  `birthday` datetime DEFAULT NULL COMMENT '出生日期',
  `gradeid` int(10) NOT NULL COMMENT '学生的年级',
  `address` varchar(100) DEFAULT NULL COMMENT '家庭住址',
  `email` varchar(50) DEFAULT NULL COMMENT '邮箱',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8


---插入语句（添加）
--insert into 表名([字段名1,字段名2,字段名3])values('值1'),('值2'),('值3'),(......)
--往gread表的gradname字段插入`大二`这个值
insert into `gread`(`gradname`)values('大二')
--由于主键自增我们可以省略（如果不写表的字段他们会意义匹配）
--一般写插入语句，我们一定要数据和字段一一对应！
--插入多个字段
insert into `gread`(`gradname`)VALUES('大一'),('大二')

--给sudent插入字段数据
INSERT INTO `student`(`name`,`pwd`,`gender`)VALUES('张三','aaaaa','男')

INSERT INTO `student`(`name`,`pwd`,`gender`)VALUES('李四','bbbbb','男'),('程序媛','cccccc','女')
```

**格式语法：**

> **insert into 表名([字段名1,字段名2,字段名3])values('值1'),('值2'),('值3'),(......)**

注意事项：

1.字段和字段之间使用  英文逗号 隔开

2.字段是可以省略的，但是后面的值必须一一对应

3.可以同时插入多条数据，values后面的值，需要使用逗号隔开即可values(),()....

**二，修改**（update）

>update 修改谁 （条件） set原来的值=新值

```SQL
---修改  
--把id=5的name设置为'金融啊'    set设置 wehere在哪里
UPDATE `student` set `name`='金融啊'WHERE id=5

--如果不带条件where表中的name全部就会变成'金融啊'
UPDATE `student` set `name`='金融啊'
--如果在公司写了这样的sql那就赶紧跑路吧（没开日志）

--修改多个属性,逗号隔开
UPDATE `student` set `name`='王五1',`email`='12548@qq.com' WHERE id=4
```

**语法格式：** 

>UPDATE 表名 set colnum_name=value WHERE  [条件]
>
>（UPDATE 表名  set  字段名（列名） =值 WHERE 条件）
>
>-----多个条件
>
>UPDATE 表名 set colnum_name,colnum_name,colnum_name.....=value WHERE  [条件]
>
>

**条件：**where 子句 运算符 id等于某个值，大于某个值，在某个区间内修改

操作符会返回布尔值：

**注意：**

- colnum_name 是数据库的列，尽量带上``(Tab键上面)
- 条件，筛选的条件，如果没有指定，则会修改全部列
- value,是一个具体的值，也可以是一个变量(比如日期)
- 多个设置的属性之间，使用英文逗号隔开

```sql
UPDATE `student` set `birthday`=CURRENT_TIME WHERE NAME='程序媛' OR `gender` ='女'
```



**三，删除**（delete）

> delete命令

```sql
--删除数据（避免这样写）
DELETE FORM 'student'

--指定的删除
--删除student表中id为1的数据
DELETE FORM 'student' WHERE id=1
```

**语法格式：**

> DELETE FORM 表名 [where 条件]



**我们清空表中的数据的时候不要用上面的delete，用TRUNCATE**

> TRUNCATE 命令

**作用：**完全清空一张数据库表，表的结构和约束不会表！

```sql
--清空student表
TRUNCATE `student`
```



> delete 和TRUNCATE区别

- **相同点：**都能删除数据，都不会删除表的结构
- **不同：**

​             TRUNCATE 重新设置自增列计算器会归零

​             TRUNCATE 不会影响事务

> 测试：

```sql
--测试delete和TRUNCATE区别
CREATE TABLE `test`(

  `id` INT(4) NOT NULL AUTO_INCREMENT,
   `coll` VARCHAR(20) NOT NULL,
	
  PRIMARY KEY(`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8	

INSERT INTO `test`(`coll`)VALUES('1'),('2'),('3'),('4'),('5')

delete from `test`  --不会影响自增

TRUNCATE TABLE `test` --自增会归零
```

了解即可：**delete删除问题**，重启数据库，现象

InnoDB 自增列会重1开始（存在内存当中，断电丢失）

MyISAM 继续往上一个自增量开始（存在文件中，不会丢失）





***\*分享一下我学习编程的途径希望大家循序渐进，共同进步：\****

[How2J 的 Java教程](https://how2j.cn?p=80103)：当下Java小白的引路人，以有趣和好理解的方式展示Java和Web的内容拥有当今流行的java路线。

[哔哩哔哩 (゜-゜)つロ 干杯~-bilibili](https://www.bilibili.com/)：中国最大的学习平台没有之一，拥有海量的资源有时间的小伙伴可以免去重金花钱培训。

[廖雪峰的官方网站](https://www.liaoxuefeng.com)：**廖雪峰**,十年软件开发经验,业余产品经理,精通Java/Python/Ruby/Scheme/Objective C等,对开源框架有深入研究..

 

[菜鸟教程 - 学的不仅是技术,更是梦想!](https://www.runoob.com/)：提供了编程的基础技术教程, 介绍了HTML、CSS、Javascript、Python,Java,Ruby,C,PHP , MySQL等各种编程语言的基础知识。