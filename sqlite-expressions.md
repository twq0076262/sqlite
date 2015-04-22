# SQLite 表达式

表达式是一个或多个值、运算符和计算值的SQL函数的组合。

SQL 表达式与公式类似，都写在查询语言中。您还可以使用特定的数据集来查询数据库。

## 语法
假设 SELECT 语句的基本语法如下：

```
    SELECT column1, column2, columnN
    FROM table_name
    WHERE [CONTION | EXPRESSION];
```

有不同类型的 SQLite 表达式，具体讲解如下：

## SQLite - 布尔表达式
SQLite 的布尔表达式在匹配单个值的基础上获取数据。语法如下：

```
    SELECT column1, column2, columnN
    FROM table_name
    WHERE SINGLE VALUE MATCHTING EXPRESSION;
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
```

下面的实例演示了 SQLite 布尔表达式的用法：

```
    sqlite> SELECT * FROM COMPANY WHERE SALARY = 10000;
    ID          NAME        AGE         ADDRESS     SALARY
    ----------  ----------  ----------  ----------  ----------
    4           James        24          Houston   10000.0
```

## SQLite - 数值表达式
这些表达式用来执行查询中的任何数学运算。语法如下：

```
    SELECT numerical_expression as  OPERATION_NAME
    [FROM table_name WHERE CONDITION] ;
```

在这里，numerical_expression 用于数学表达式或任何公式。下面的实例演示了 SQLite 数值表达式的用法：

```
    sqlite> SELECT (15 + 6) AS ADDITION
    ADDITION = 21
```

有几个内置的函数，比如 avg()、sum()、count()，等等，执行被称为对一个表或一个特定的表列的汇总数据计算。

```
    sqlite> SELECT COUNT(*) AS "RECORDS" FROM COMPANY;
    RECORDS = 7
```

## SQLite - 日期表达式
日期表达式返回当前系统日期和时间值，这些表达式将被用于各种数据操作。

```
    sqlite>  SELECT CURRENT_TIMESTAMP;
    CURRENT_TIMESTAMP = 2013-03-17 10:43:35
```
