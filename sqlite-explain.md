# SQLite Explain（解释）

在 SQLite 语句之前，可以使用 "EXPLAIN" 关键字或 "EXPLAIN QUERY PLAN" 短语，用于描述表的细节。

如果省略了 EXPLAIN 关键字或短语，任何的修改都会引起 SQLite 语句的查询行为，并返回有关 SQLite 语句如何操作的信息。

* 来自 EXPLAIN 和 EXPLAIN QUERY PLAN 的输出只用于交互式分析和排除故障。
* 输出格式的细节可能会随着 SQLite 版本的不同而有所变化。
* 应用程序不应该使用 EXPLAIN 或 EXPLAIN QUERY PLAN，因为其确切的行为是可变的且只有部分会被记录。

## 语法

**EXPLAIN** 的语法如下：

```
    EXPLAIN [SQLite Query]
```

**EXPLAIN QUERY PLAN** 的语法如下：

```
    EXPLAIN  QUERY PLAN [SQLite Query]
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

现在，让我们检查 SELECT 语句中的 **Explain** 使用：

```
    sqlite> EXPLAIN SELECT *  FROM COMPANY  WHERE Salary >= 20000;
```

这将产生以下结果：

```
    addr        opcode      p1          p2          p3
    ----------  ----------  ----------  ----------  ----------
    0           Goto        0           19
    1           Integer     0           0
    2           OpenRead    0           8
    3           SetNumColu  0           5
    4           Rewind      0           17
    5           Column      0           4
    6           RealAffini  0           0
    7           Integer     20000       0
    8           Lt          357         16          collseq(BI
    9           Rowid       0           0
    10          Column      0           1
    11          Column      0           2
    12          Column      0           3
    13          Column      0           4
    14          RealAffini  0           0
    15          Callback    5           0
    16          Next        0           5
    17          Close       0           0
    18          Halt        0           0
    19          Transactio  0           0
    20          VerifyCook  0           38
    21          Goto        0           1
    22          Noop        0           0
```

现在，让我们检查 SELECT 语句中的 **Explain Query Plan** 使用：

```
    SQLite> EXPLAIN QUERY PLAN SELECT * FROM COMPANY WHERE Salary >= 20000;

    order       from        detail
    ----------  ----------  -------------
    0           0           TABLE COMPANY
```