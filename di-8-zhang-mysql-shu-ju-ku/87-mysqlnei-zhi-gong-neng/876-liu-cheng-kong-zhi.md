## 本节重点

* 掌握流程控制的基本使用

> **本节时长需控制在5分钟内**

### 一 流程控制

```
delimiter //
CREATE PROCEDURE proc_if ()
BEGIN
    
    declare i int default 0;
    if i = 1 THEN
        SELECT 1;
    ELSEIF i = 2 THEN
        SELECT 2;
    ELSE
        SELECT 7;
    END IF;

END //
delimiter ;

if条件语句
```

#### **二 循环语句**

```
delimiter //
CREATE PROCEDURE proc_while ()
BEGIN

    DECLARE num INT ;
    SET num = 0 ;
    WHILE num < 10 DO
        SELECT
            num ;
        SET num = num + 1 ;
    END WHILE ;

END //
delimiter ;

while循环
```

```
delimiter //
CREATE PROCEDURE proc_repeat ()
BEGIN

    DECLARE i INT ;
    SET i = 0 ;
    repeat
        select i;
        set i = i + 1;
        until i >= 5
    end repeat;

END //
delimiter ;

 repeat循环
```

```
BEGIN
    
    declare i int default 0;
    loop_label: loop
        
        set i=i+1;
        if i<8 then
            iterate loop_label;
        end if;
        if i>=10 then
            leave loop_label;
        end if;
        select i;
    end loop loop_label;

END

loop
```



