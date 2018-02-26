## 本节重点

* 掌握触发器的基本使用

> **本节时长需控制在5分钟内**

### 一 触发器

使用触发器可以定制用户对表进行【增、删、改】操作时前后的行为，注意：没有查询

#### **一 创建触发器**

```
# 插入前
CREATE TRIGGER tri_before_insert_tb1 BEFORE INSERT ON tb1 FOR EACH ROW
BEGIN
    ...
END

# 插入后
CREATE TRIGGER tri_after_insert_tb1 AFTER INSERT ON tb1 FOR EACH ROW
BEGIN
    ...
END

# 删除前
CREATE TRIGGER tri_before_delete_tb1 BEFORE DELETE ON tb1 FOR EACH ROW
BEGIN
    ...
END

# 删除后
CREATE TRIGGER tri_after_delete_tb1 AFTER DELETE ON tb1 FOR EACH ROW
BEGIN
    ...
END

# 更新前
CREATE TRIGGER tri_before_update_tb1 BEFORE UPDATE ON tb1 FOR EACH ROW
BEGIN
    ...
END

# 更新后
CREATE TRIGGER tri_after_update_tb1 AFTER UPDATE ON tb1 FOR EACH ROW
BEGIN
    ...
END
```

```
#准备表
CREATE TABLE cmd (
    id INT PRIMARY KEY auto_increment,
    USER CHAR (32),
    priv CHAR (10),
    cmd CHAR (64),
    sub_time datetime, #提交时间
    success enum ('yes', 'no') #0代表执行失败
);

CREATE TABLE errlog (
    id INT PRIMARY KEY auto_increment,
    err_cmd CHAR (64),
    err_time datetime
);

#创建触发器
delimiter //
CREATE TRIGGER tri_after_insert_cmd AFTER INSERT ON cmd FOR EACH ROW
BEGIN
    IF NEW.success = 'no' THEN #等值判断只有一个等号
            INSERT INTO errlog(err_cmd, err_time) VALUES(NEW.cmd, NEW.sub_time) ; #必须加分号
      END IF ; #必须加分号
END//
delimiter ;


#往表cmd中插入记录，触发触发器，根据IF的条件决定是否插入错误日志
INSERT INTO cmd (
    USER,
    priv,
    cmd,
    sub_time,
    success
)
VALUES
    ('egon','0755','ls -l /etc',NOW(),'yes'),
    ('egon','0755','cat /etc/passwd',NOW(),'no'),
    ('egon','0755','useradd xxx',NOW(),'no'),
    ('egon','0755','ps aux',NOW(),'yes');


#查询错误日志，发现有两条
mysql> select * from errlog;
+----+-----------------+---------------------+
| id | err_cmd         | err_time            |
+----+-----------------+---------------------+
|  1 | cat /etc/passwd | 2017-09-14 22:18:48 |
|  2 | useradd xxx     | 2017-09-14 22:18:48 |
+----+-----------------+---------------------+
rows in set (0.00 sec)

插入后触发触发器
```

**特别的：NEW表示即将插入的数据行，OLD表示即将删除的数据行。**

#### **二 使用触发器**

触发器无法由用户直接调用，而知由于对表的【增/删/改】操作被动引发的。

#### **三 删除触发器**

```
drop trigger tri_after_insert_cmd;
```



