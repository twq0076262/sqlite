# SQLite 创建表

SQLite 的 **CREATE TABLE** 语句用于在任何给定的数据库创建一个新表。创建基本表，涉及到命名表、定义列及每一列的数据类型。

CREATE TABLE 语句的基本语法如下：

```
    CREATE TABLE database_name.table_name(
       column1 datatype  PRIMARY KEY(one or more columns),
       column2 datatype,
       column3 datatype,
       .....
       columnN datatype,
    );
```

CREATE TABLE 是告诉数据库系统创建一个新表的关键字。CREATE TABLE 语句后跟着表的唯一的名称或标识。您也可以选择指定带有 _table_name_ 的 _ database_name_。

下面是一个实例，它创建了一个 COMPANY 表，ID 作为主键，NOT NULL 的约束表示在表中创建纪录时这些字段不能为 NULL：

```
    sqlite> CREATE TABLE COMPANY(
       ID INT PRIMARY KEY     NOT NULL,
       NAME           TEXT    NOT NULL,
       AGE            INT     NOT NULL,
       ADDRESS        CHAR(50),
       SALARY         REAL
    );
```

让我们再创建一个表，我们将在随后章节的练习中使用：

```
    sqlite> CREATE TABLE DEPARTMENT(
       ID INT PRIMARY KEY      NOT NULL,
       DEPT           CHAR(50) NOT NULL,
       EMP_ID         INT      NOT NULL
    );
```

您可以使用 SQLIte 命令中的 **.tables** 命令来验证表是否已成功创建，该命令用于列出附加数据库中的所有表。

```
    sqlite>.tables
    COMPANY     DEPARTMENT
```

在这里，可以看到 COMPANY 表出现两次，一个是主数据库的 COMPANY 表，一个是为 testDB.db 创建的 'test' 别名的 test.COMPANY 表。您可以使用 SQLite **.schema** 命令得到表的完整信息，如下所示：

```
    sqlite>.schema COMPANY
    CREATE TABLE COMPANY(
       ID INT PRIMARY KEY     NOT NULL,
       NAME           TEXT    NOT NULL,
       AGE            INT     NOT NULL,
       ADDRESS        CHAR(50),
       SALARY         REAL
    );
```