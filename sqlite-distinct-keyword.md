# SQLite Distinct


SQLite 的 **DISTINCT** 关键字与 SELECT 语句一起使用，来消除所有重复的记录，并只获取唯一一次记录。

有可能出现一种情况，在一个表中有多个重复的记录。当提取这样的记录时，DISTINCT 关键字就显得特别有意义，它只获取唯一一次记录，而不是获取重复记录。

用于消除重复记录的 DISTINCT 关键字的基本语法如下：

```
    SELECT DISTINCT column1, column2,.....columnN
    FROM table_name
    WHERE [condition]
```

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
    8           Paul        24          Houston     20000.0
    9           James       44          Norway      5000.0
    10          James       45          Texas       5000.0
```

首先，让我们来看看下面的 SELECT 查询，它将返回重复的工资记录：

```
    sqlite> SELECT name FROM COMPANY;
```

这将产生以下结果：

```
    NAME
    ----------
    Paul
    Allen
    Teddy
    Mark
    David
    Kim
    James
    Paul
    James
    James
```

现在，让我们在上述的 SELECT 查询中使用 **DISTINCT** 关键字：

```
    sqlite> SELECT DISTINCT name FROM COMPANY;
```

这将产生以下结果，没有任何重复的条目：

```
    NAME
    ----------
    Paul
    Allen
    Teddy
    Mark
    David
    Kim
    James
```