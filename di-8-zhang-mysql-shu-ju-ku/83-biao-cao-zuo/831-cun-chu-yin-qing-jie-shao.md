## 本节重点

* 了解存储引擎

> **本节时长需控制在10分钟内**

### 一 什么是存储引擎

mysql中建立的库===&gt;文件夹

库中建立的表===&gt;文件

现实生活中我们用来存储数据的文件有不同的类型，每种文件类型对应各自不同的处理机制：比如处理文本用txt类型，处理表格用excel，处理图片用png等

数据库中的表也应该有不同的类型，表的类型不同，会对应mysql不同的存取机制，表类型又称为存储引擎。

存储引擎说白了就是如何存储数据、如何为存储的数据建立索引和如何更新、查询数据等技术的实现方  
法。因为在关系数据库中数据的存储是以表的形式存储的，所以存储引擎也可以称为表类型（即存储和  
操作此表的类型）

在Oracle 和SQL Server等数据库中只有一种存储引擎，所有数据存储管理机制都是一样的。而MySql  
数据库提供了多种存储引擎。用户可以根据不同的需求为数据表选择不同的存储引擎，用户也可以根据  
自己的需要编写自己的存储引擎

![](/assets/chapter8/存储引擎.png)

SQL 解析器、SQL 优化器、缓冲池、存储引擎等组件在每个数据库中都存在,但不是每 个数据库都有这么多存储引擎。MySQL 的插件式存储引擎可以让存储引擎层的开发人员设 计他们希望的存储层,例如,有的应用需要满足事务的要求,有的应用则不需要对事务有这 么强的要求 ;有的希望数据能持久存储,有的只希望放在内存中,临时并快速地提供对数据 的查询。

### 二 mysql支持的存储引擎

```
MariaDB [(none)]> show engines\G  #查看所有支持的存储引擎

MariaDB [(none)]> show variables like 'storage_engine%'; #查看正在使用的存储引擎
```

**1、InnoDB 存储引擎**

支持事务,其设计目标主要面向联机事务处理\(OLTP\)的应用。其

特点是行锁设计、支持外键,并支持类似 Oracle 的非锁定读,即默认读取操作不会产生锁。 从 MySQL 5.5.8 版本开始是默认的存储引擎。

InnoDB 存储引擎将数据放在一个逻辑的表空间中,这个表空间就像黑盒一样由 InnoDB 存储引擎自身来管理。从 MySQL 4.1\(包括 4.1\)版本开始,可以将每个 InnoDB 存储引擎的 表单独存放到一个独立的 ibd 文件中。此外,InnoDB 存储引擎支持将裸设备\(row disk\)用 于建立其表空间。

InnoDB 通过使用多版本并发控制\(MVCC\)来获得高并发性,并且实现了 SQL 标准 的 4 种隔离级别,默认为 REPEATABLE 级别,同时使用一种称为 netx-key locking 的策略来 避免幻读\(phantom\)现象的产生。除此之外,InnoDB 存储引擎还提供了插入缓冲\(insert buffer\)、二次写\(double write\)、自适应哈希索引\(adaptive hash index\)、预读\(read ahead\) 等高性能和高可用的功能。

对于表中数据的存储,InnoDB 存储引擎采用了聚集\(clustered\)的方式,每张表都是按 主键的顺序进行存储的,如果没有显式地在表定义时指定主键,InnoDB 存储引擎会为每一 行生成一个 6 字节的 ROWID,并以此作为主键。

InnoDB 存储引擎是 MySQL 数据库最为常用的一种引擎,Facebook、Google、Yahoo 等 公司的成功应用已经证明了 InnoDB 存储引擎具备高可用性、高性能以及高可扩展性。对其 底层实现的掌握和理解也需要时间和技术的积累。如果想深入了解 InnoDB 存储引擎的工作 原理、实现和应用,可以参考《MySQL 技术内幕:InnoDB 存储引擎》一书。

**2、MyISAM 存储引擎**

不支持事务、表锁设计、支持全文索引,主要面向一些 OLAP 数 据库应用,在 MySQL 5.5.8 版本之前是默认的存储引擎\(除 Windows 版本外\)。数据库系统 与文件系统一个很大的不同在于对事务的支持,MyISAM 存储引擎是不支持事务的。究其根 本,这也并不难理解。用户在所有的应用中是否都需要事务呢?在数据仓库中,如果没有 ETL 这些操作,只是简单地通过报表查询还需要事务的支持吗?此外,MyISAM 存储引擎的 另一个与众不同的地方是,它的缓冲池只缓存\(cache\)索引文件,而不缓存数据文件,这与 大多数的数据库都不相同。

**3、NDB 存储引擎**

年,MySQL AB 公司从 Sony Ericsson 公司收购了 NDB 存储引擎。 NDB 存储引擎是一个集群存储引擎,类似于 Oracle 的 RAC 集群,不过与 Oracle RAC 的 share everything 结构不同的是,其结构是 share nothing 的集群架构,因此能提供更高级别的 高可用性。NDB 存储引擎的特点是数据全部放在内存中\(从 5.1 版本开始,可以将非索引数 据放在磁盘上\),因此主键查找\(primary key lookups\)的速度极快,并且能够在线添加 NDB 数据存储节点\(data node\)以便线性地提高数据库性能。由此可见,NDB 存储引擎是高可用、 高性能、高可扩展性的数据库集群系统,其面向的也是 OLTP 的数据库应用类型。

**4、Memory 存储引擎**

正如其名,Memory 存储引擎中的数据都存放在内存中,数据库重 启或发生崩溃,表中的数据都将消失。它非常适合于存储 OLTP 数据库应用中临时数据的临时表,也可以作为 OLAP 数据库应用中数据仓库的维度表。Memory 存储引擎默认使用哈希 索引,而不是通常熟悉的 B+ 树索引。

**5、Infobright 存储引擎**

第三方的存储引擎。其特点是存储是按照列而非行的,因此非常 适合 OLAP 的数据库应用。其官方网站是 [http://www.infobright.org/,上面有不少成功的数据](http://www.infobright.org/,上面有不少成功的数据) 仓库案例可供分析。

**6、NTSE 存储引擎**

网易公司开发的面向其内部使用的存储引擎。目前的版本不支持事务, 但提供压缩、行级缓存等特性,不久的将来会实现面向内存的事务支持。

**7、BLACKHOLE**

黑洞存储引擎，可以应用于主备复制中的分发主库。

MySQL 数据库还有很多其他存储引擎,上述只是列举了最为常用的一些引擎。如果 你喜欢,完全可以编写专属于自己的引擎,这就是开源赋予我们的能力,也是开源的魅 力所在。

### 三 使用存储引擎

方法1：建表时指定

```
MariaDB [db1]> create table innodb_t1(id int,name char)engine=innodb;
MariaDB [db1]> create table innodb_t2(id int)engine=innodb;
MariaDB [db1]> show create table innodb_t1;
MariaDB [db1]> show create table innodb_t2;
```

方法2：在配置文件中指定默认的存储引擎

```
/etc/my.cnf
[mysqld]
default-storage-engine=INNODB
innodb_file_per_table=1
```

查看

```
[root@egon db1]# cd /var/lib/mysql/db1/
[root@egon db1]# ls
db.opt  innodb_t1.frm  innodb_t1.ibd  innodb_t2.frm  innodb_t2.ibd
```

练习

创建四个表，分别使用innodb，myisam，memory，blackhole存储引擎，进行插入数据测试

```
MariaDB [db1]> create table t1(id int)engine=innodb;
MariaDB [db1]> create table t2(id int)engine=myisam;
MariaDB [db1]> create table t3(id int)engine=memory;
MariaDB [db1]> create table t4(id int)engine=blackhole;
MariaDB [db1]> quit
[root@egon db1]# ls /var/lib/mysql/db1/ #发现后两种存储引擎只有表结构，无数据
db.opt  t1.frm  t1.ibd  t2.MYD  t2.MYI  t2.frm  t3.frm  t4.frm

#memory，在重启mysql或者重启机器后，表内数据清空
#blackhole，往表内插入任何数据，都相当于丢入黑洞，表内永远不存记录
```



