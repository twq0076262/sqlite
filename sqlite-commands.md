# SQLite 命令


本章将向您讲解 SQLite 编程人员所使用的简单却有用的命令。些命令被称为 SQLite 的点命令，这些命令的不同之处在于它们不以分号（;）结束。

让我们在命令提示符下键入一个简单的 **sqlite3** 命令，在 SQLite 命令提示符下，您可以使用各种 SQLite 命令。

```
$sqlite3
SQLite version 3.3.6
Enter ".help" for instructions
sqlite>
```

如需获取可用的点命令的清单，可以在任何时候输入 ".help"。例如：

```
sqlite>.help
```

上面的命令会显示各种重要的 SQLite 点命令的列表，如下所示：
 
 
</p> <table > <tr> <th style="width:30%">命令</th><th style="width:70%">描述</th> </tr> <tr><td>.backup ?DB? FILE</td><td>备份 DB 数据库（默认是 "main"）到 FILE 文件。</td></tr> <tr><td>.bail ON|OFF</td><td>发生错误后停止。默认为 OFF。</td></tr> <tr><td>.databases</td><td>列出附加数据库的名称和文件。</td></tr> <tr><td>.dump ?TABLE?</td><td>以 SQL 文本格式转储数据库。如果指定了 TABLE 表，则只转储匹配 LIKE 模式的 TABLE 表。</td></tr> <tr><td>.echo ON|OFF</td><td>开启或关闭 echo 命令。</td></tr> <tr><td>.exit</td><td>退出 SQLite 提示符。</td></tr> <tr><td>.explain ON|OFF</td><td>开启或关闭适合于 EXPLAIN 的输出模式。如果没有带参数，则为 EXPLAIN on，及开启 EXPLAIN。</td></tr> <tr><td>.header(s) ON|OFF</td><td>开启或关闭头部显示。</td></tr> <tr><td>.help</td><td>显示消息。</td></tr> <tr><td>.import FILE TABLE</td><td>导入来自 FILE 文件的数据到 TABLE 表中。</td></tr> <tr><td>.indices ?TABLE?</td><td>显示所有索引的名称。如果指定了 TABLE 表，则只显示匹配 LIKE 模式的 TABLE 表的索引。</td></tr> <tr><td>.load FILE ?ENTRY?</td><td>加载一个扩展库。</td></tr> <tr><td>.log FILE|off</td><td>开启或关闭日志。FILE 文件可以是 stderr（标准错误）/stdout（标准输出）。</td></tr> <tr><td>.mode MODE</td><td>设置输出模式，MODE 可以是下列之一： <ul > <li><p><b>csv</b> 逗号分隔的值</p></li> <li><p><b>column</b> 左对齐的列</p></li> <li><p><b>html</b> HTML 的 &lt;table&gt; 代码</p></li> <li><p><b>insert</b> TABLE 表的 SQL 插入（insert）语句</p></li> <li><p><b>line</b> 每行一个值</p></li> <li><p><b>list</b> 由 .separator 字符串分隔的值</p></li> <li><p><b>tabs</b> 由 Tab 分隔的值</p></li> <li><p><b>tcl</b> TCL 列表元素</p></li> </ul> </td></tr> <tr><td>.nullvalue STRING</td><td>在 NULL 值的地方输出 STRING 字符串。</td></tr> <tr><td>.output FILENAME</td><td>发送输出到 FILENAME 文件。</td></tr> <tr><td>.output stdout</td><td>发送输出到屏幕。</td></tr> <tr><td>.print STRING...</td><td>逐字地输出 STRING 字符串。</td></tr> <tr><td>.prompt MAIN CONTINUE</td><td>替换标准提示符。</td></tr> <tr><td>.quit</td><td>退出 SQLite 提示符。</td></tr> <tr><td>.read FILENAME</td><td>执行 FILENAME 文件中的 SQL。</td></tr> <tr><td>.schema ?TABLE?</td><td>显示 CREATE 语句。如果指定了 TABLE 表，则只显示匹配 LIKE 模式的 TABLE 表。</td></tr> <tr><td>.separator STRING</td><td>改变输出模式和 .import 所使用的分隔符。</td></tr> <tr><td>.show</td><td>显示各种设置的当前值。</td></tr> <tr><td>.stats ON|OFF</td><td>开启或关闭统计。</td></tr> <tr><td>.tables ?PATTERN?</td><td>列出匹配 LIKE 模式的表的名称。</td></tr> <tr><td>.timeout MS</td><td>尝试打开锁定的表 MS 微秒。</td></tr> <tr><td>.width NUM NUM</td><td>为 "column" 模式设置列宽度。</td></tr> <tr><td>.timer ON|OFF </td><td>开启或关闭 CPU 定时器测量。</td></tr> </table> <p>


让我们尝试使用 **.show** 命令，来查看 SQLite 命令提示符的默认设置。

```
sqlite>.show
     echo: off
  explain: off
  headers: off
     mode: column
nullvalue: ""
   output: stdout
separator: "|"
    width:
sqlite>
```

> 确保 sqlite> 提示符与点命令之间没有空格，否则将无法正常工作。

## 格式化输出

您可以使用下列的点命令来格式化输出为本教程下面所列出的格式：

```
sqlite>.header on
sqlite>.mode column
sqlite>.timer on
sqlite>
```

上面设置将产生如下格式的输出：

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
CPU Time: user 0.000000 sys 0.000000
```

## sqlite_master 表格

主表中保存数据库表的关键信息，并把它命名为 **sqlite_master**。如要查看表概要，可按如下操作：

```
sqlite>.schema sqlite_master
```

这将产生如下结果：

```
CREATE TABLE sqlite_master (
  type text,
  name text,
  tbl_name text,
  rootpage integer,
  sql text
);
```