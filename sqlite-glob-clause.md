# SQLite Glob 子句


SQLite 的 **GLOB** 运算符是用来匹配通配符指定模式的文本值。如果搜索表达式与模式表达式匹配，GLOB 运算符将返回真（true），也就是 1。与 LIKE 运算符不同的是，GLOB 是大小写敏感的，对于下面的通配符，它遵循 UNIX 的语法。

* 星号 （*）
* 问号 （?）

星号（*）代表零个、一个或多个数字或字符。问号（?）代表一个单一的数字或字符。这些符号可以被组合使用。

## 语法

* 和 ? 的基本语法如下：

```
    SELECT FROM table_name
    WHERE column GLOB 'XXXX*'

    or

    SELECT FROM table_name
    WHERE column GLOB '*XXXX*'

    or

    SELECT FROM table_name
    WHERE column GLOB 'XXXX?'

    or

    SELECT FROM table_name
    WHERE column GLOB '?XXXX'

    or

    SELECT FROM table_name
    WHERE column GLOB '?XXXX?'

    or

    SELECT FROM table_name
    WHERE column GLOB '????'
```

您可以使用 AND 或 OR 运算符来结合 N 个数量的条件。在这里，XXXX 可以是任何数字或字符串值。

## 实例
下面一些实例演示了 带有 '*' 和 '?' 运算符的 GLOB 子句不同的地方：
 
</p> <table > <tr><th style="width:35%">语句</th><th style="width:65%">描述</th></tr> <tr><td>WHERE SALARY GLOB '200*'</td><td>查找以 200 开头的任意值</td></tr> <tr><td>WHERE SALARY GLOB '*200*'</td><td>查找任意位置包含 200 的任意值</td></tr> <tr><td>WHERE SALARY GLOB '?00*'</td><td>查找第二位和第三位为 00 的任意值</td></tr> <tr><td>WHERE SALARY GLOB '2??'</td><td>查找以 2 开头，且长度至少为 3 个字符的任意值</td></tr> <tr><td>WHERE SALARY GLOB '*2'</td><td>查找以 2 结尾的任意值</td></tr> <tr><td>WHERE SALARY GLOB '?2*3'</td><td>查找第二位为 2，且以 3 结尾的任意值</td></tr> <tr><td>WHERE SALARY GLOB '2???3'</td><td>查找长度为 5 位数，且以 2 开头以 3 结尾的任意值</td></tr> </table> <p>


让我们举一个实际的例子，假设 COMPANY 表有以下记录：

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

下面是一个实例，它显示 COMPANY 表中 AGE 以 2 开头的所有记录：

```
    sqlite> SELECT * FROM COMPANY WHERE AGE  GLOB '2*';
```

这将产生以下结果：

```
    ID          NAME        AGE         ADDRESS     SALARY
    ----------  ----------  ----------  ----------  ----------
    2           Allen       25          Texas       15000.0
    3           Teddy       23          Norway      20000.0
    4           Mark        25          Rich-Mond   65000.0
    5           David       27          Texas       85000.0
    6           Kim         22          South-Hall  45000.0
    7           James       24          Houston     10000.0
```

下面是一个实例，它显示 COMPANY 表中 ADDRESS 文本里包含一个连字符（-）的所有记录：

```
    sqlite> SELECT * FROM COMPANY WHERE ADDRESS  GLOB '*-*';
```

这将产生以下结果：

```
    ID          NAME        AGE         ADDRESS     SALARY
    ----------  ----------  ----------  ----------  ----------
    4           Mark        25          Rich-Mond   65000.0
    6           Kim         22          South-Hall  45000.0
```