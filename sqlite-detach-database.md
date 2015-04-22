# SQLite 分离数据库


SQLite的 **DETACH DTABASE** 语句是用来把命名数据库从一个数据库连接分离和游离出来，连接是之前使用 ATTACH 语句附加的。如果同一个数据库文件已经被附加上多个别名，DETACH 命令将只断开给定名称的连接，而其余的仍然有效。您无法分离 **main** 或 **temp** 数据库。

> 如果数据库是在内存中或者是临时数据库，则该数据库将被摧毁，且内容将会丢失。

SQLite 的 DETACH DATABASE 'Alias-Name' 语句的基本语法如下：

```
    DETACH DATABASE 'Alias-Name';
```
在这里，'Alias-Name' 与您之前使用 ATTACH 语句附加数据库时所用到的别名相同。

假设在前面的章节中您已经创建了一个数据库，并给它附加了 'test' 和 'currentDB'，使用 .database 命令，我们可以看到：

```
    sqlite>.databases
    seq  name             file
    ---  ---------------  ----------------------
    0    main             /home/sqlite/testDB.db
    2    test             /home/sqlite/testDB.db
    3    currentDB        /home/sqlite/testDB.db
```

现在，让我们尝试把 'currentDB' 从 testDB.db 中分离出来，如下所示：

```
    sqlite> DETACH DATABASE 'currentDB';
```

现在，如果检查当前附加的数据库，您会发现，testDB.db 仍与 'test' 和 'main' 保持连接。

```
    sqlite>.databases
    seq  name             file
    ---  ---------------  ----------------------
    0    main             /home/sqlite/testDB.db
    2    test             /home/sqlite/testDB.db
```