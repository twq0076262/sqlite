# SQLite 日期 & 时间

SQLite 支持以下五个日期和时间函数：

<table>
<tbody>
<tr>
<th>序号</th>

<th style="width:39%">函数</th>

<th style="width:59%">实例</th>

</tr>

<tr>
<td>1</td>

<td>date(timestring, modifiers...)</td>

<td>以 YYYY-MM-DD 格式返回日期。</td>

</tr>

<tr>
<td>2</td>

<td>time(timestring, modifiers...)</td>

<td>以 HH:MM:SS 格式返回时间。</td>

</tr>

<tr>
<td>3</td>

<td>datetime(timestring, modifiers...)</td>

<td>以 YYYY-MM-DD HH:MM:SS 格式返回。</td>

</tr>

<tr>
<td>4</td>

<td>julianday(timestring, modifiers...)</td>

<td>这将返回从格林尼治时间的公元前 4714 年 11 月 24 日正午算起的天数。</td>

</tr>

<tr>
<td>5</td>

<td>strftime(timestring, modifiers...)</td>

<td>这将根据第一个参数指定的格式字符串返回格式化的日期。具体格式见下边讲解。</td>

</tr>

</tbody>

</table>

上述五个日期和时间函数把时间字符串作为参数。时间字符串后跟零个或多个 modifiers 修饰符。strftime() 函数也可以把格式字符串作为其第一个参数。下面将为您详细讲解不同类型的时间字符串和修饰符。

## 时间字符串

一个时间字符串可以采用下面任何一种格式：

<table>
<tbody>
<tr>
<th>序号</th>

<th style="width:39%">时间字符串</th>

<th style="width:59%">实例</th>

</tr>

<tr>
<td>1</td>

<td>YYYY-MM-DD</td>

<td>2010-12-30</td>

</tr>

<tr>
<td>2</td>

<td>YYYY-MM-DD HH:MM</td>

<td>2010-12-30 12:10</td>

</tr>

<tr>
<td>3</td>

<td>YYYY-MM-DD HH:MM:SS.SSS</td>

<td>2010-12-30 12:10:04.100</td>

</tr>

<tr>
<td>4</td>

<td>MM-DD-YYYY HH:MM</td>

<td>30-12-2010 12:10</td>

</tr>

<tr>
<td>5</td>

<td>HH:MM</td>

<td>12:10</td>

</tr>

<tr>
<td>6</td>

<td>YYYY-MM-DD**T**HH:MM</td>

<td>2010-12-30 12:10</td>

</tr>

<tr>
<td>7</td>

<td>HH:MM:SS</td>

<td>12:10:01</td>

</tr>

<tr>
<td>8</td>

<td>YYYYMMDD HHMMSS</td>

<td>20101230 121001</td>

</tr>

<tr>
<td>9</td>

<td>now</td>

<td>2013-05-07</td>

</tr>

</tbody>

</table>

您可以使用 "T" 作为分隔日期和时间的文字字符。

## 修饰符（Modifiers）

时间字符串后边可跟着零个或多个的修饰符，这将改变有上述五个函数返回的日期和/或时间。任何上述五大功能返回时间。修饰符应从左到右使用，下面列出了可在 SQLite 中使用的修饰符：

*   NNN days

*   NNN hours

*   NNN minutes

*   NNN.NNNN seconds

*   NNN months

*   NNN years

*   start of month

*   start of year

*   start of day

*   weekday N

*   unixepoch

*   localtime

*   utc

## 格式化

SQLite 提供了非常方便的函数 **strftime()** 来格式化任何日期和时间。您可以使用以下的替换来格式化日期和时间：

|替换     |描述
|--------|--------------------------
|%d      |一月中的第几天，01-31
|%f      |带小数部分的秒，SS.SSS
|%H      |小时，00-23
|%j      |一年中的第几天，001-366
|%J      |儒略日数，DDDD.DDDD
|%m      |月，00-12
|%M      |分，00-59
|%s      |从 1970-01-01 算起的秒数
|%S      |秒，00-59
|%w      |一周中的第几天，0-6 (0 is Sunday)
|%W      |一年中的第几周，01-53
|%Y      |年，YYYY
|%%      |% symbol

## 实例

现在让我们使用 SQLite 提示符尝试不同的实例。下面是计算当前日期：

```
    sqlite> SELECT date('now');
    2013-05-07
```

下面是计算当前月份的最后一天：

```
    sqlite> SELECT date('now','start of month','+1 month','-1 day');
    2013-05-31
```

下面是计算给定 UNIX 时间戳 1092941466 的日期和时间：

```
    sqlite> SELECT datetime(1092941466, 'unixepoch');
    2004-08-19 18:51:06
```

下面是计算给定 UNIX 时间戳 1092941466 相对本地时区的日期和时间：

```
    sqlite> SELECT datetime(1092941466, 'unixepoch', 'localtime');
    2004-08-19 11:51:06
```

下面是计算当前的 UNIX 时间戳：

```
    sqlite> SELECT datetime(1092941466, 'unixepoch', 'localtime');
    1367926057
```

下面是计算美国"独立宣言"签署以来的天数：

```
    sqlite> SELECT julianday('now') - julianday('1776-07-04');
    86504.4775830326
```

下面是计算从 2004 年某一特定时刻以来的秒数：

```
    sqlite> SELECT strftime('%s','now') - strftime('%s','2004-01-01 02:34:56');
    295001572
```

下面是计算当年 10 月的第一个星期二的日期：

```
    sqlite> SELECT date('now','start of year','+9 months','weekday 2');
    2013-10-01
```

下面是计算从 UNIX 纪元算起的以秒为单位的时间（类似 strftime('%s','now') ，不同的是这里有包括小数部分）：

```
    sqlite> SELECT (julianday('now') - 2440587.5)*86400.0;
    1367926077.12598
```

在 UTC 与本地时间值之间进行转换，当格式化日期时，使用 utc 或 localtime 修饰符，如下所示：

```
    sqlite> SELECT time('12:00', 'localtime');
    05:00:00

    sqlite>  SELECT time('12:00', 'utc');
    19:00:00
```
  