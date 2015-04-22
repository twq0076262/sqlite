# SQLite Autoincrement

SQLite 的 **AUTOINCREMENT** 是一个关键字，用于表中的字段值自动递增。我们可以在创建表时在特定的列名称上使用 **AUTOINCREMENT** 关键字实现该字段值的自动增加。

关键字 **AUTOINCREMENT** 只能用于整型（INTEGER）字段。

## 语法

**AUTOINCREMENT** 关键字的基本用法如下：

```
    CREATE TABLE table_name(
       column1 INTEGER AUTOINCREMENT,
       column2 datatype,
       column3 datatype,
       .....
       columnN datatype,
    );
```

## 实例

假设要创建的 COMPANY 表如下所示：

```
    sqlite> CREATE TABLE COMPANY(
       ID INTEGER PRIMARY KEY   AUTOINCREMENT,
       NAME           TEXT      NOT NULL,
       AGE            INT       NOT NULL,
       ADDRESS        CHAR(50),
       SALARY         REAL
    );
```

现在，向 COMPANY 表插入以下记录：

```
    INSERT INTO COMPANY (NAME,AGE,ADDRESS,SALARY)
    VALUES ( 'Paul', 32, 'California', 20000.00 );

    INSERT INTO COMPANY (NAME,AGE,ADDRESS,SALARY)
    VALUES ('Allen', 25, 'Texas', 15000.00 );

    INSERT INTO COMPANY (NAME,AGE,ADDRESS,SALARY)
    VALUES ('Teddy', 23, 'Norway', 20000.00 );

    INSERT INTO COMPANY (NAME,AGE,ADDRESS,SALARY)
    VALUES ( 'Mark', 25, 'Rich-Mond ', 65000.00 );

    INSERT INTO COMPANY (NAME,AGE,ADDRESS,SALARY)
    VALUES ( 'David', 27, 'Texas', 85000.00 );

    INSERT INTO COMPANY (NAME,AGE,ADDRESS,SALARY)
    VALUES ( 'Kim', 22, 'South-Hall', 45000.00 );

    INSERT INTO COMPANY (NAME,AGE,ADDRESS,SALARY)
    VALUES ( 'James', 24, 'Houston', 10000.00 );
```

这将向 COMPANY 表插入 7 个元组，此时 COMPANY 表的记录如下：

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