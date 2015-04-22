# SQLite Update 语句


SQLite 的 **UPDATE** 查询用于修改表中已有的记录。可以使用带有 WHERE 子句的 UPDATE 查询来更新选定行，否则所有的行都会被更新。

## 语法
带有 WHERE 子句的 UPDATE 查询的基本语法如下：

```
    UPDATE table_name
    SET column1 = value1, column2 = value2...., columnN = valueN
    WHERE [condition];
```

您可以使用 AND 或 OR 运算符来结合 N 个数量的条件。

## 实例
假设 COMPANY 表有以下记录：

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

下面是一个实例，它会更新 ID 为 6 的客户地址：

```
    sqlite> UPDATE COMPANY SET ADDRESS = 'Texas' WHERE ID = 6;
```

现在，COMPANY 表有以下记录：

```
    ID          NAME        AGE         ADDRESS     SALARY
    ----------  ----------  ----------  ----------  ----------
    1           Paul        32          California  20000.0
    2           Allen       25          Texas       15000.0
    3           Teddy       23          Norway      20000.0
    4           Mark        25          Rich-Mond   65000.0
    5           David       27          Texas       85000.0
    6           Kim         22          Texas       45000.0
    7           James       24          Houston     10000.0
```

如果您想修改 COMPANY 表中 ADDRESS 和 SALARY 列的所有值，则不需要使用 WHERE 子句，UPDATE 查询如下：

```
    sqlite> UPDATE COMPANY SET ADDRESS = 'Texas', SALARY = 20000.00;
```

现在，COMPANY 表有以下记录：

```
    ID          NAME        AGE         ADDRESS     SALARY
    ----------  ----------  ----------  ----------  ----------
    1           Paul        32          Texas       20000.0
    2           Allen       25          Texas       20000.0
    3           Teddy       23          Texas       20000.0
    4           Mark        25          Texas       20000.0
    5           David       27          Texas       20000.0
    6           Kim         22          Texas       20000.0
    7           James       24          Texas       20000.0
```