# SQLite Insert 语句

SQLite 的 **INSERT INTO** 语句用于向数据库的某个表中添加新的数据行。

## 语法
INSERT INTO 语句有两种基本语法，如下所示：

```
    INSERT INTO TABLE_NAME (column1, column2, column3,...columnN)]
    VALUES (value1, value2, value3,...valueN);
```

在这里，column1, column2,...columnN 是要插入数据的表中的列的名称。

如果要为表中的所有列添加值，您也可以不需要在 SQLite 查询中指定列名称。但要确保值的顺序与列在表中的顺序一致。SQLite 的 INSERT INTO 语法如下：

```
    INSERT INTO TABLE_NAME VALUES (value1,value2,value3,...valueN);
```

## 实例
假设您已经在 testDB.db 中创建了 COMPANY表，如下所示：

```
    sqlite> CREATE TABLE COMPANY(
       ID INT PRIMARY KEY     NOT NULL,
       NAME           TEXT    NOT NULL,
       AGE            INT     NOT NULL,
       ADDRESS        CHAR(50),
       SALARY         REAL
    );
```

现在，下面的语句将在 COMPANY 表中创建六个记录：

```
    INSERT INTO COMPANY (ID,NAME,AGE,ADDRESS,SALARY)
    VALUES (1, 'Paul', 32, 'California', 20000.00 );

    INSERT INTO COMPANY (ID,NAME,AGE,ADDRESS,SALARY)
    VALUES (2, 'Allen', 25, 'Texas', 15000.00 );

    INSERT INTO COMPANY (ID,NAME,AGE,ADDRESS,SALARY)
    VALUES (3, 'Teddy', 23, 'Norway', 20000.00 );

    INSERT INTO COMPANY (ID,NAME,AGE,ADDRESS,SALARY)
    VALUES (4, 'Mark', 25, 'Rich-Mond ', 65000.00 );

    INSERT INTO COMPANY (ID,NAME,AGE,ADDRESS,SALARY)
    VALUES (5, 'David', 27, 'Texas', 85000.00 );

    INSERT INTO COMPANY (ID,NAME,AGE,ADDRESS,SALARY)
    VALUES (6, 'Kim', 22, 'South-Hall', 45000.00 );
```

您也可以使用第二种语法在 COMPANY 表中创建一个记录，如下所示：

```
    INSERT INTO COMPANY VALUES (7, 'James', 24, 'Houston', 10000.00 );
```

上面的所有语句将在 COMPANY 表中创建下列记录。下一章会教您如何从一个表中显示所有这些记录。

```
    ID          NAME        AGE         ADDRESS     SALARY
    ----------  ----------  ----------  ----------  ----------
    1           Paul        32          California  20000.0
    2           Allen       25          Texas       15000.0
    3           Teddy       23          Norway      20000.0
    4           Mark        25          Rich-Mond   65000.0
    5           David       27          Texas       85000.0
    6           Kim         22          South-Hall  45000.0
    7           James       24          Houston     10000.0
```

## 使用一个表来填充另一个表
您可以通过在一个有一组字段的表上使用 select 语句，填充数据到另一个表中。下面是语法：

```
    INSERT INTO first_table_name [(column1, column2, ... columnN)]
       SELECT column1, column2, ...columnN
       FROM second_table_name
       [WHERE condition];
```

您暂时可以先跳过上面的语句，可以先学习后面章节中介绍的 SELECT 和 WHERE 子句。  