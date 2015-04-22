# SQLite Indexed By


"INDEXED BY index-name" 子句规定必须需要命名的索引来查找前面表中值。

如果索引名 index-name 不存在或不能用于查询，然后 SQLite 语句的准备失败。

"NOT INDEXED" 子句规定当访问前面的表（包括由 UNIQUE 和 PRIMARY KEY 约束创建的隐式索引）时，没有使用索引。

然而，即使指定了 "NOT INDEXED"，INTEGER PRIMARY KEY 仍然可以被用于查找条目。

## 语法

下面是 INDEXED BY 子句的语法，它可以与 DELETE、UPDATE 或 SELECT 语句一起使用：

```
    SELECT|DELETE|UPDATE column1, column2...
    INDEXED BY (index_name)
    table_name
    WHERE (CONDITION);
```

## 实例

假设有表 COMPANY，我们将创建一个索引，并用它进行 INDEXED BY 操作。

```
    sqlite> CREATE INDEX salary_index ON COMPANY(salary);
    sqlite>
```

现在使用 INDEXED BY 子句从表 COMPANY 中选择数据，如下所示：

```
    sqlite> SELECT * FROM COMPANY INDEXED BY salary_index WHERE salary > 5000;
```