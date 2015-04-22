# SQLite Having 子句


HAVING 子句允许指定条件来过滤将出现在最终结果中的分组结果。

WHERE 子句在所选列上设置条件，而 HAVING 子句则在由 GROUP BY 子句创建的分组上设置条件。

## 语法
下面是 HAVING 子句在 SELECT 查询中的位置：

```
    SELECT
    FROM
    WHERE
    GROUP BY
    HAVING
    ORDER BY
```

在一个查询中，HAVING 子句必须放在 GROUP BY 子句之后，必须放在 ORDER BY 子句之前。下面是包含 HAVING 子句的 SELECT 语句的语法：

```
    SELECT column1, column2
    FROM table1, table2
    WHERE [ conditions ]
    GROUP BY column1, column2
    HAVING [ conditions ]
    ORDER BY column1, column2
```
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
    8           Paul        24          Houston     20000.0
    9           James       44          Norway      5000.0
    10          James       45          Texas       5000.0
```

下面是一个实例，它将显示名称计数小于 2 的所有记录：

```
    sqlite > SELECT * FROM COMPANY GROUP BY name HAVING count(name) < 2;
```

这将产生以下结果：

```
    ID          NAME        AGE         ADDRESS     SALARY
    ----------  ----------  ----------  ----------  ----------
    2           Allen       25          Texas       15000
    5           David       27          Texas       85000
    6           Kim         22          South-Hall  45000
    4           Mark        25          Rich-Mond   65000
    3           Teddy       23          Norway      20000
```

下面是一个实例，它将显示名称计数大于 2 的所有记录：

```
    sqlite > SELECT * FROM COMPANY GROUP BY name HAVING count(name) > 2;
```

这将产生以下结果：

```
    ID          NAME        AGE         ADDRESS     SALARY
    ----------  ----------  ----------  ----------  ----------
    10          James       45          Texas       5000
```
  