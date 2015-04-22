# SQLite Unions 子句


SQLite的 **UNION** 子句/运算符用于合并两个或多个 SELECT 语句的结果，不返回任何重复的行。

为了使用 UNION，每个 SELECT 被选择的列数必须是相同的，相同数目的列表达式，相同的数据类型，并确保它们有相同的顺序，但它们不必具有相同的长度。

## 语法

**UNION** 的基本语法如下：

```
    SELECT column1 [, column2 ]
    FROM table1 [, table2 ]
    [WHERE condition]

    UNION

    SELECT column1 [, column2 ]
    FROM table1 [, table2 ]
    [WHERE condition]
```

这里给定的条件根据需要可以是任何表达式。

## 实例

假设有下面两个表，（1）COMPANY 表如下所示：

```
    sqlite> select * from COMPANY;
    ID          NAME                  AGE         ADDRESS     SALARY
    ----------  --------------------  ----------  ----------  ----------
    1           Paul                  32          California  20000.0
    2           Allen                 25          Texas       15000.0
    3           Teddy                 23          Norway      20000.0
    4           Mark                  25          Rich-Mond   65000.0
    5           David                 27          Texas       85000.0
    6           Kim                   22          South-Hall  45000.0
    7           James                 24          Houston     10000.0
```

（2）另一个表是 DEPARTMENT，如下所示：

```
    ID          DEPT                  EMP_ID
    ----------  --------------------  ----------
    1           IT Billing            1
    2           Engineering           2
    3           Finance               7
    4           Engineering           3
    5           Finance               4
    6           Engineering           5
    7           Finance               6
```

现在，让我们使用 SELECT 语句及 UNION 子句来连接两个表，如下所示：

```
    sqlite> SELECT EMP_ID, NAME, DEPT FROM COMPANY INNER JOIN DEPARTMENT
            ON COMPANY.ID = DEPARTMENT.EMP_ID
       UNION
         SELECT EMP_ID, NAME, DEPT FROM COMPANY LEFT OUTER JOIN DEPARTMENT
            ON COMPANY.ID = DEPARTMENT.EMP_ID;

```
这将产生以下结果：

```
    EMP_ID      NAME                  DEPT
    ----------  --------------------  ----------
    1           Paul                  IT Billing
    2           Allen                 Engineerin
    3           Teddy                 Engineerin
    4           Mark                  Finance
    5           David                 Engineerin
    6           Kim                   Finance
    7           James                 Finance
```

UNION ALL 运算符用于结合两个 SELECT 语句的结果，包括重复行。

适用于 UNION 的规则同样适用于 UNION ALL 运算符。

## 语法

**UNION ALL** 的基本语法如下：

```
    SELECT column1 [, column2 ]
    FROM table1 [, table2 ]
    [WHERE condition]

    UNION ALL

    SELECT column1 [, column2 ]
    FROM table1 [, table2 ]
    [WHERE condition]
```

这里给定的条件根据需要可以是任何表达式。

## 实例

现在，让我们使用 SELECT 语句及 UNION ALL 子句来连接两个表，如下所示：

```
    sqlite> SELECT EMP_ID, NAME, DEPT FROM COMPANY INNER JOIN DEPARTMENT
            ON COMPANY.ID = DEPARTMENT.EMP_ID
       UNION ALL
         SELECT EMP_ID, NAME, DEPT FROM COMPANY LEFT OUTER JOIN DEPARTMENT
            ON COMPANY.ID = DEPARTMENT.EMP_ID;
```

这将产生以下结果：

```
    EMP_ID      NAME                  DEPT
    ----------  --------------------  ----------
    1           Paul                  IT Billing
    2           Allen                 Engineerin
    3           Teddy                 Engineerin
    4           Mark                  Finance
    5           David                 Engineerin
    6           Kim                   Finance
    7           James                 Finance
    1           Paul                  IT Billing
    2           Allen                 Engineerin
    3           Teddy                 Engineerin
    4           Mark                  Finance
    5           David                 Engineerin
    6           Kim                   Finance
    7           James                 Finance
```