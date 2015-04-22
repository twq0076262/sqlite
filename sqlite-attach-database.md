# SQLite 附加数据库

假设这样一种情况，当在同一时间有多个数据库可用，您想使用其中的任何一个。SQLite 的 **ATTACH DTABASE** 语句是用来选择一个特定的数据库，使用该命令后，所有的 SQLite 语句将在附加的数据库下执行。

## 语法
SQLite 的 ATTACH DATABASE 语句的基本语法如下：

```
    ATTACH DATABASE 'DatabaseName' As 'Alias-Name';
```

## 实例
如果数据库尚未被创建，上面的命令将创建一个数据库，如果数据库已存在，则把数据库文件名称与逻辑数据库 'Alias-Name' 绑定在一起。

如果想附加一个现有的数据库 **testDB.db**，则 ATTACH DATABASE 语句将如下所示：

```
    sqlite> ATTACH DATABASE 'testDB.db' as 'TEST';
```

使用 SQLite **.database** 命令来显示附加的数据库。

```
    sqlite> .database
    seq  name             file
    ---  ---------------  ----------------------
    0    main             /home/sqlite/testDB.db
    2    test             /home/sqlite/testDB.db
```

数据库名称 **main** 和 **temp** 被保留用于主数据库和存储临时表及其他临时数据对象的数据库。这两个数据库名称可用于每个数据库连接，且不应该被用于附加，否则将得到一个警告消息，如下所示：

```
    sqlite>  ATTACH DATABASE 'testDB.db' as 'TEMP';
    Error: database TEMP is already in use
    sqlite>  ATTACH DATABASE 'testDB.db' as 'main';
    Error: database TEMP is already in use
```