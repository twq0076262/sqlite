# SQLite Delete 语句 


SQLite 的 **DELETE** 查询用于删除表中已有的记录。可以使用带有 WHERE 子句的 DELETE 查询来删除选定行，否则所有的记录都会被删除。


## 语法
带有 WHERE 子句的 DELETE 查询的基本语法如下：

```
    DELETE FROM table_name
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

下面是一个实例，它会删除 ID 为 7 的客户：

```
    sqlite> DELETE FROM COMPANY WHERE ID = 7;
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
    6           Kim         22          South-Hall  45000.0
```

如果您想要从 COMPANY 表中删除所有记录，则不需要使用 WHERE 子句，DELETE 查询如下：

```
    sqlite> DELETE FROM COMPANY;
```

现在，COMPANY 表中没有任何的记录，因为所有的记录已经通过 DELETE 语句删除。 