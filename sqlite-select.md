# SQLite Select 语句

SQLite 的 **SELECT** 语句用于从 SQLite 数据库表中获取数据，以结果表的形式返回数据。这些结果表也被称为结果集。

## 语法
SQLite 的 SELECT 语句的基本语法如下：

```
    SELECT column1, column2, columnN FROM table_name;
```

在这里，column1, column2...是表的字段，他们的值即是您要获取的。如果您想获取所有可用的字段，那么可以使用下面的语法：

```
    SELECT * FROM table_name;
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
```

下面是一个实例，使用 SELECT 语句获取并显示所有这些记录。在这里，前三个命令被用来设置正确格式化的输出。

```
    sqlite>.header on
    sqlite>.mode column
    sqlite> SELECT * FROM COMPANY;
```

最后，将得到以下的结果：

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

如果只想获取 COMPANY 表中指定的字段，则使用下面的查询：

```
    sqlite> SELECT ID, NAME, SALARY FROM COMPANY;
```

上面的查询会产生以下结果：

```
    ID          NAME        SALARY
    ----------  ----------  ----------
    1           Paul        20000.0
    2           Allen       15000.0
    3           Teddy       20000.0
    4           Mark        65000.0
    5           David       85000.0
    6           Kim         45000.0
    7           James       10000.0
```

## 设置输出列的宽度
有时，由于要显示的列的默认宽度导致 **.mode column**，这种情况下，输出被截断。此时，您可以使用 **.width num, num....** 命令设置显示列的宽度，如下所示：

```
    sqlite>.width 10, 20, 10
    sqlite>SELECT * FROM COMPANY;
```

上面的 **.width** 命令设置第一列的宽度为 10，第二列的宽度为 20，第三列的宽度为 10。因此上述 SELECT 语句将得到以下结果：

```
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

## Schema 信息
因为所有的**点命令**只在 SQLite 提示符中可用，所以当您进行带有 SQLite 的编程时，您要使用下面的带有 **sqlite_master** 表的 SELECT 语句来列出所有在数据库中创建的表：

```
    sqlite> SELECT tbl_name FROM sqlite_master WHERE type = 'table';
```

假设在 testDB.db 中已经存在唯一的 COMPANY 表，则将产生以下结果：

```
    tbl_name
    ----------
    COMPANY
```

您可以列出关于 COMPANY 表的完整信息，如下所示：

```
    sqlite> SELECT sql FROM sqlite_master WHERE type = 'table' AND tbl_name = 'COMPANY';
```

假设在 testDB.db 中已经存在唯一的 COMPANY 表，则将产生以下结果：

```
    CREATE TABLE COMPANY(
       ID INT PRIMARY KEY     NOT NULL,
       NAME           TEXT    NOT NULL,
       AGE            INT     NOT NULL,
       ADDRESS        CHAR(50),
       SALARY         REAL
    )
```