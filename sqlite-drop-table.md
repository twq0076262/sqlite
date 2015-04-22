# SQLite 删除表

SQLite 的 **DROP TABLE** 语句用来删除表定义及其所有相关数据、索引、触发器、约束和该表的权限规范。

> 使用此命令时要特别注意，因为一旦一个表被删除，表中所有信息也将永远丢失。

DROP TABLE 语句的基本语法如下。您可以选择指定带有表名的数据库名称，如下所示：

```
    DROP TABLE database_name.table_name;
```

让我们先确认 COMPANY 表已经存在，然后我们将其从数据库中删除。

```
    sqlite>.tables
    COMPANY       test.COMPANY
```

这意味着 COMPANY 表已存在数据库中，接下来让我们把它从数据库中删除，如下：

```
    sqlite>DROP TABLE COMPANY;
    sqlite>
```

现在，如果尝试 .TABLES 命令，那么将无法找到 COMPANY 表了：

```
    sqlite>.tables
    sqlite>
```

显示结果为空，意味着已经成功从数据库删除表。  