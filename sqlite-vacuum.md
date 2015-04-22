# SQLite Vacuum

VACUUM 命令通过复制主数据库中的内容到一个临时数据库文件，然后清空主数据库，并从副本中重新载入原始的数据库文件。这消除了空闲页，把表中的数据排列为连续的，另外会清理数据库文件结构。

如果表中没有明确的整型主键（INTEGER PRIMARY KEY），VACUUM 命令可能会改变表中条目的行 ID（ROWID）。VACUUM 命令只适用于主数据库，附加的数据库文件是不可能使用 VACUUM 命令。

如果有一个活动的事务，VACUUM 命令就会失败。VACUUM 命令是一个用于内存数据库的任何操作。由于 VACUUM 命令从头开始重新创建数据库文件，所以 VACUUM 也可以用于修改许多数据库特定的配置参数。

## 手动 VACUUM

下面是在命令提示符中对整个数据库发出 VACUUM 命令的语法：

```
    $sqlite3 database_name "VACUUM;"
```

您也可以在 SQLite 提示符中运行 VACUUM，如下所示：

```
    sqlite> VACUUM;
```

您也可以在特定的表上运行 VACUUM，如下所示：

```
    sqlite> VACUUM table_name;
```

## 自动 VACCUM（Auto-VACUUM）

SQLite 的 Auto-VACUUM 与 VACUUM 不大一样，它只是把空闲页移到数据库末尾，从而减小数据库大小。通过这样做，它可以明显地把数据库碎片化，而 VACUUM 则是反碎片化。所以 Auto-VACUUM 只会让数据库更小。

在 SQLite 提示符中，您可以通过下面的编译运行，启用/禁用 SQLite 的 Auto-VACUUM：

```
    sqlite> PRAGMA auto_vacuum = NONE;  -- 0 means disable auto vacuum
    sqlite> PRAGMA auto_vacuum = INCREMENTAL;  -- 1 means enable incremental vacuum
    sqlite> PRAGMA auto_vacuum = FULL;  -- 2 means enable full auto vacuum
```

您可以从命令提示符中运行下面的命令来检查 auto-vacuum 设置：

```
    $sqlite3 database_name "PRAGMA auto_vacuum;"
```
  