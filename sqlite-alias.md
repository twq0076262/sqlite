# SQLite 别名

您可以暂时把表或列重命名为另一个名字，这被称为**别名**。使用表别名是指在一个特定的 SQLite 语句中重命名表。重命名是临时的改变，在数据库中实际的表的名称不会改变。

列别名用来为某个特定的 SQLite 语句重命名表中的列。

## 语法

**表** 别名的基本语法如下：

```
    SELECT column1, column2....
    FROM table_name AS alias_name
    WHERE [condition];
```

**列** 别名的基本语法如下：

```
    SELECT column_name AS alias_name
    FROM table_name
    WHERE [condition];
```

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

现在，下面是 **表别名** 的用法，在这里我们使用 C 和 D 分别作为 COMPANY 和 DEPARTMENT 表的别名：

```
    sqlite> SELECT C.ID, C.NAME, C.AGE, D.DEPT
            FROM COMPANY AS C, DEPARTMENT AS D
            WHERE  C.ID = D.EMP_ID;
```

上面的 SQLite 语句将产生下面的结果：

```
    ID          NAME        AGE         DEPT
    ----------  ----------  ----------  ----------
    1           Paul        32          IT Billing
    2           Allen       25          Engineerin
    3           Teddy       23          Engineerin
    4           Mark        25          Finance
    5           David       27          Engineerin
    6           Kim         22          Finance
    7           James       24          Finance
```

让我们看一个 **列别名** 的实例，在这里 COMPANY_ID 是 ID 列的别名，COMPANY_NAME 是 name 列的别名：

```
    sqlite> SELECT C.ID AS COMPANY_ID, C.NAME AS COMPANY_NAME, C.AGE, D.DEPT
            FROM COMPANY AS C, DEPARTMENT AS D
            WHERE  C.ID = D.EMP_ID;
```

上面的 SQLite 语句将产生下面的结果：

```
    COMPANY_ID  COMPANY_NAME  AGE         DEPT
    ----------  ------------  ----------  ----------
    1           Paul          32          IT Billing
    2           Allen         25          Engineerin
    3           Teddy         23          Engineerin
    4           Mark          25          Finance
    5           David         27          Engineerin
    6           Kim           22          Finance
    7           James         24          Finance
```