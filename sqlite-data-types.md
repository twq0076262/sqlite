# SQLite 数据类型


SQLite 数据类型是一个用来指定任何对象的数据类型的属性。SQLite 中的每一列，每个变量和表达式都有相关的数据类型。

您可以在创建表的同时使用这些数据类型。SQLite 使用一个更普遍的动态类型系统。在 SQLite 中，值的数据类型与值本身是相关的，而不是与它的容器相关。


## SQLite 存储类

每个存储在 SQLite 数据库中的值都具有以下存储类之一：
 
</p> <table > <tr><th style="width:30%">存储类</th><th style="width:70%">描述</th></tr> <tr><td>NULL</td><td>值是一个 NULL 值。</td></tr> <tr><td>INTEGER</td><td>值是一个带符号的整数，根据值的大小存储在 1、2、3、4、6 或 8 字节中。</td></tr> <tr><td>REAL</td><td>值是一个浮点值，存储为 8 字节的 IEEE 浮点数字。</td></tr> <tr><td>TEXT</td><td>值是一个文本字符串，使用数据库编码（UTF-8、UTF-16BE 或 UTF-16LE）存储。</td></tr> <tr><td>BLOB</td><td>值是一个 blob 数据，完全根据它的输入存储。</td></tr> </table> <p>

SQLite 的存储类稍微比数据类型更普遍。INTEGER 存储类，例如，包含 6 种不同的不同长度的整数数据类型。
## SQLite Affinity 类型

SQLite 支持列上的_类型 affinity_ 概念。任何列仍然可以存储任何类型的数据，但列的首选存储类是它的 **affinity**。在 SQLite3 数据库中，每个表的列分配为以下类型的 affinity 之一：

</p> <table > <tr><th style="width:30%">Affinity</th><th style="width:70%">描述</th></tr> <tr><td>TEXT</td><td>该列使用存储类 NULL、TEXT 或 BLOB 存储所有数据。</td></tr> <tr><td>NUMERIC</td><td>该列可以包含使用所有五个存储类的值。</td></tr> <tr><td>INTEGER</td><td>与带有 NUMERIC affinity 的列相同，在 CAST 表达式中带有异常。</td></tr> <tr><td>REAL</td><td>与带有 NUMERIC affinity 的列相似，不同的是，它会强制把整数值转换为浮点表示。</td></tr> <tr><td>NONE</td><td>带有 affinity NONE 的列，不会优先使用哪个存储类，也不会尝试把数据从一个存储类强制转换为另一个存储类。</td></tr> </table> 

## SQLite Affinity 及类型名称

下表列出了当创建 SQLite3 表时可使用的各种数据类型名称，同时也显示了相应的应用 Affinity：

</p> <table > <tr><th style="width:30%">数据类型</th><th style="width:70%">Affinity</th></tr> <tr><td> <ul > <li><p>INT</p></li> <li><p>INTEGER</p></li> <li><p>TINYINT</p></li> <li><p>SMALLINT</p></li> <li><p>MEDIUMINT</p></li> <li><p>BIGINT</p></li> <li><p>UNSIGNED BIG INT</p></li> <li><p>INT2</p></li> <li><p>INT8</p></li> </ul> </td><td>INTEGER</td></tr> <tr><td> <ul > <li><p>CHARACTER(20)</p></li> <li><p>VARCHAR(255)</p></li> <li><p>VARYING CHARACTER(255)</p></li> <li><p>NCHAR(55)</p></li> <li><p>NATIVE CHARACTER(70)</p></li> <li><p>NVARCHAR(100)</p></li> <li><p>TEXT</p></li> <li><p>CLOB</p></li> </ul> </td><td>TEXT</td></tr> <tr><td> <ul > <li><p>BLOB</p></li> <li><p>no datatype specified</p></li> </ul> </td><td>NONE</td></tr> <tr><td> <ul > <li><p>REAL</p></li> <li><p>DOUBLE</p></li> <li><p>DOUBLE PRECISION</p></li> <li><p>FLOAT</p></li> </ul> </td><td>REAL</td></tr> <tr><td> <ul > <li><p>NUMERIC</p></li> <li><p>DECIMAL(10,5)</p></li> <li><p>BOOLEAN</p></li> <li><p>DATE</p></li> <li><p>DATETIME</p></li> </ul> </td><td>NUMERIC</td></tr> </table> 


## Boolean 数据类型

SQLite 没有单独的 Boolean 存储类。相反，布尔值被存储为整数 0（false）和 1（true）。

## Date 与 Time 数据类型

SQLite 没有一个单独的用于存储日期和/或时间的存储类，但 SQLite 能够把日期和时间存储为 TEXT、REAL 或 INTEGER 值。

</p> <table > <tr><th style="width:30%">存储类</th><th style="width:70%">日期格式</th></tr> <tr><td>TEXT</td><td>格式为 "YYYY-MM-DD HH:MM:SS.SSS" 的日期。</td></tr> <tr><td>REAL</td><td>从公元前 4714 年 11 月 24 日格林尼治时间的正午开始算起的天数。</td></tr> <tr><td>INTEGER</td><td>从 1970-01-01 00:00:00 UTC 算起的秒数。</td></tr> </table> <p>

您可以以任何上述格式来存储日期和时间，并且可以使用内置的日期和时间函数来自由转换不同格式。