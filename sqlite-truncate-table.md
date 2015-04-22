# SQLite Truncate Table

在 SQLite 中，并没有 TRUNCATE TABLE 命令，但可以使用 SQLite 的 **DELETE** 命令从已有的表中删除全部的数据，但建议使用 DROP TABLE 命令删除整个表，然后再重新创建一遍。

## 语法

DELETE 命令的基本语法如下：

```
    sqlite> DELETE FROM table_name;
```

DROP TABLE 的基本语法如下：

```
    sqlite> DROP TABLE table_name;
```

如果您使用 DELETE TABLE 命令删除所有记录，建议使用 **VACUUM** 命令清除未使用的空间。

## 实例

假设 COMPANY 表有如下记录：

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

下面为删除上表记录的实例：

```
    SQLite> DELETE FROM COMPANY;
    SQLite> VACUUM;
```

现在，COMPANY 表中的记录完全被删除，使用 SELECT 语句将没有任何输出。  