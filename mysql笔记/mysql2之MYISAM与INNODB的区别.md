### MYISAM与INNODB的区别：

常用的命令：

```sql
SHOW CREATE DATABASE shcool --查看创建数据库的语句
SHOW CREATE TABLE student --查看创建数据库表的语句
DESC student --显示表的结构
```

#### 二，数据表的类型：

```sql
--关于数据的引擎
/*
INNODB 默认使用
MYISAM 早些年使用
*/
```

|              | MYISAM | INNODB                 |
| ------------ | ------ | ---------------------- |
| 事务支持     | 不支持 | 支持                   |
| 数据行锁定   | 不支持 | 支持                   |
| 外键约束     | 不支持 | 支持                   |
| 全文索引     | 支持   | 不支持（mysql8.0支持） |
| 表空间的大小 | 较小   | 较大，约为2倍          |

常规的操作：

-   MYISAM 节约空间，速度较快
-   INNODB  安全性高，事务的处理，多表多用户操作InnoDB存储引擎是Mysql的默认存储引擎。InnoDB存储引擎提供了具有提交、回滚、崩溃恢复能力的事务安全。但是对比MyISAM的存储引擎，InnoDB写的处理效率差一些，并且会占用更多的磁盘空间以保留数据和索引。

InnoDB存储引擎不同于其他存储引擎的特点

> **物理空间存在的位置**

所有的数据库文件都在data的目录下面,一个文件夹对应一个数据库

本质还是文件存储

- Mysql引擎在物理文件上的区别

- InnoDB在数据库表中只有一个*.frm文件，以及上级目录下的ibdata1文件

- InnoDB 存储表和索引有以下两种方式 ： 

  ①. 使用共享表空间存储， 这种方式创建的表的表结构保存在.frm文件中， 数据和索引保存在 innodb_data_home_dir 和 innodb_data_file_path定义的表空间中，可以是多个文件。

  ②. 使用多表空间存储， 这种方式创建的表的表结构仍然存在 .frm 文件中，但是每个表的数据和索引单独保存在 .ibd 中。

**MyISAM 对应文件**

-  *.from  -表结构的定义文件
- *.MYD  数据文件(data)
- *.MYI  索引文件(index)

> 设置数据表的字符集编码

```sql
CHARSET=utf8
```

不设置的话，会是mysql默认的字符集编码~（不支持中文）

在Mysql安装的目录my.ini文件中设置默认编码

```sql
character-set-server=utf8
```

#### 存储引擎的选择：

在选择存储引擎时，应该根据应用系统的特点选择合适的存储引擎。对于复杂的应用系统，还可以根据实际情况选择多种存储引擎进行组合。以下是几种常用的存储引擎的使用环境。

- InnoDB : 是Mysql的默认存储引擎，用于事务处理应用程序，支持外键。如果应用对事务的完整性有比较高的要求，在并发条件下要求数据的一致性，数据操作除了插入和查询意外，还包含很多的更新、删除操作，那么InnoDB存储引擎是比较合适的选择。InnoDB存储引擎除了有效的降低由于删除和更新导致的锁定， 还可以确保事务的完整提交和回滚，对于类似于计费系统或者财务系统等对数据准确性要求比较高的系统，InnoDB是最合适的选择。
- MyISAM ： 如果应用是以读操作和插入操作为主，只有很少的更新和删除操作，并且对事务的完整性、并发性要求不是很高，那么选择这个存储引擎是非常合适的。
- MEMORY：将所有数据保存在RAM中，在需要快速定位记录和其他类似数据环境下，可以提供几块的访问。MEMORY的缺陷就是对表的大小有限制，太大的表无法缓存在内存中，其次是要确保表的数据可以恢复，数据库异常终止后表中的数据是可以恢复的。MEMORY表通常用于更新不太频繁的小表，用以快速得到访问结果。
- MERGE：用于将一系列等同的MyISAM表以逻辑方式组合在一起，并作为一个对象引用他们。MERGE表的优点在于可以突破对单个MyISAM表的大小限制，并且通过将不同的表分布在多个磁盘上，可以有效的改善MERGE表的访问效率。这对于存储诸如数据仓储等VLDB环境十分合适。



***\*博客到此，分享一下我学习编程的途径希望大家循序渐进，共同进步：\****

[How2J 的 Java教程](https://how2j.cn?p=80103)：当下Java小白的引路人，以有趣和好理解的方式展示Java和Web的内容拥有当今流行的java路线。

[哔哩哔哩 (゜-゜)つロ 干杯~-bilibili](https://www.bilibili.com/)：中国最大的学习平台没有之一，拥有海量的资源有时间的小伙伴可以免去重金花钱培训。

[廖雪峰的官方网站](https://www.liaoxuefeng.com)：**廖雪峰**,十年软件开发经验,业余产品经理,精通Java/Python/Ruby/Scheme/Objective C等,对开源框架有深入研究..

 

[菜鸟教程 - 学的不仅是技术,更是梦想!](https://www.runoob.com/)：提供了编程的基础技术教程, 介绍了HTML、CSS、Javascript、Python,Java,Ruby,C,PHP , MySQL等各种编程语言的基础知识。