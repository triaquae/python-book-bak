## 本节重点

* 掌握事物的基本使用

> **本节时长需控制在5分钟内**

### 一 事物

事务用于将某些操作的多个SQL作为原子性操作，一旦有某一个出现错误，即可回滚到原来的状态，从而保证数据库数据完整性。

```
create table user(
id int primary key auto_increment,
name char(32),
balance int
);

insert into user(name,balance)
values
('wsb',1000),
('egon',1000),
('ysb',1000);

#原子操作
start transaction;
update user set balance=900 where name='wsb'; #买支付100元
update user set balance=1010 where name='egon'; #中介拿走10元
update user set balance=1090 where name='ysb'; #卖家拿到90元
commit;

#出现异常，回滚到初始状态
start transaction;
update user set balance=900 where name='wsb'; #买支付100元
update user set balance=1010 where name='egon'; #中介拿走10元
uppdate user set balance=1090 where name='ysb'; #卖家拿到90元,出现异常没有拿到
rollback;
commit;
mysql> select * from user;
+----+------+---------+
| id | name | balance |
+----+------+---------+
|  1 | wsb  |    1000 |
|  2 | egon |    1000 |
|  3 | ysb  |    1000 |
+----+------+---------+
rows in set (0.00 sec)
```

```
#介绍
delimiter //
            create procedure p4(
                out status int
            )
            BEGIN
                1. 声明如果出现异常则执行{
                    set status = 1;
                    rollback;
                }
                   
                开始事务
                    -- 由秦兵账户减去100
                    -- 方少伟账户加90
                    -- 张根账户加10
                    commit;
                结束
                
                set status = 2;
                
                
            END //
            delimiter ;

#实现
delimiter //
create PROCEDURE p5(
    OUT p_return_code tinyint
)
BEGIN 
    DECLARE exit handler for sqlexception 
    BEGIN 
        -- ERROR 
        set p_return_code = 1; 
        rollback; 
    END; 

    DECLARE exit handler for sqlwarning 
    BEGIN 
        -- WARNING 
        set p_return_code = 2; 
        rollback; 
    END; 

    START TRANSACTION; 
        DELETE from tb1; #执行失败
        insert into blog(name,sub_time) values('yyy',now());
    COMMIT; 

    -- SUCCESS 
    set p_return_code = 0; #0代表执行成功

END //
delimiter ;

#在mysql中调用存储过程
set @res=123;
call p5(@res);
select @res;

#在python中基于pymysql调用存储过程
cursor.callproc('p5',(123,))
print(cursor.fetchall()) #查询select的查询结果

cursor.execute('select @_p5_0;')
print(cursor.fetchall())

事务
```



