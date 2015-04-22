# SQLite 索引

索引（Index）是一种特殊的查找表，数据库搜索引擎用来加快数据检索。简单地说，索引是一个指向表中数据的指针。一个数据库中的索引与一本书后边的索引是非常相似的。

例如，如果您想在一本讨论某个话题的书中引用所有页面，您首先需要指向索引，索引按字母顺序列出了所有主题，然后指向一个或多个特定的页码。

索引有助于加快 SELECT 查询和 WHERE 子句，但它会减慢使用 UPDATE 和 INSERT 语句时的数据输入。索引可以创建或删除，但不会影响数据。

使用 CREATE INDEX 语句创建索引，它允许命名索引，指定表及要索引的一列或多列，并指示索引是升序排列还是降序排列。

索引也可以是唯一的，与 UNIQUE 约束类似，在列上或列组合上防止重复条目。

## CREATE INDEX 命令

**CREATE INDEX** 的基本语法如下：

```
    CREATE INDEX index_name ON table_name;
```

## 单列索引

单列索引是一个只基于表的一个列上创建的索引。基本语法如下：

```
    CREATE INDEX index_name
    ON table_name (column_name);
```

## 唯一索引

使用唯一索引不仅是为了性能，同时也为了数据的完整性。唯一索引不允许任何重复的值插入到表中。基本语法如下：

```
    CREATE INDEX index_name
    on table_name (column_name);
```

## 组合索引

组合索引是基于一个表的两个或多个列上创建的索引。基本语法如下：

```
    CREATE INDEX index_name
    on table_name (column1, column2);
```

是否要创建一个单列索引还是组合索引，要考虑到您在作为查询过滤条件的 WHERE 子句中使用非常频繁的列。

如果值使用到一个列，则选择使用单列索引。如果在作为过滤的 WHERE 子句中有两个或多个列经常使用，则选择使用组合索引。

## 隐式索引

隐式索引是在创建对象时，由数据库服务器自动创建的索引。索引自动创建为主键约束和唯一约束。

## 实例

下面是一个例子，我们将在 COMPANY 表的 salary 列上创建一个索引：

```
    sqlite> CREATE INDEX salary_index ON COMPANY (salary);
```

现在，让我们使用 **.indices** 命令列出 COMPANY 表上所有可用的索引，如下所示：

```
    sqlite> .indices COMPANY
```

这将产生如下结果，其中 _sqlite_autoindex_COMPANY_1_ 是创建表时创建的隐式索引。

```
    salary_index
    sqlite_autoindex_COMPANY_1
```

您可以列出数据库范围的所有索引，如下所示：

```
    sqlite> SELECT * FROM sqlite_master WHERE type = 'index';
```

## DROP INDEX 命令

一个索引可以使用 SQLite 的 **DROP** 命令删除。当删除索引时应特别注意，因为性能可能会下降或提高。

基本语法如下：

```
    DROP INDEX index_name;
```

您可以使用下面的语句来删除之前创建的索引：

```
    sqlite> DROP INDEX salary_index;
```

## 什么情况下要避免使用索引？

虽然索引的目的在于提高数据库的性能，但这里有几个情况需要避免使用索引。使用索引时，应重新考虑下列准则：

* 索引不应该使用在较小的表上。
* 索引不应该使用在有频繁的大批量的更新或插入操作的表上。
* 索引不应该使用在含有大量的 NULL 值的列上。
* 索引不应该使用在频繁操作的列上。  