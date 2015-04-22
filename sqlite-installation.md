# SQLite 安装


SQLite 的一个重要的特性是零配置的，这意味着不需要复杂的安装或管理。本章将讲解 Windows、Linux 和 Mac OS X 上的安装设置。


## 在 Windows 上安装 SQLite

*   请访问 [SQLite 下载页面](http://www.sqlite.org/download.html)，从 Windows 区下载预编译的二进制文件。

*   您需要下载 **sqlite-shell-win32-*.zip** 和 **sqlite-dll-win32-*.zip** 压缩文件。

    *   创建文件夹 C:\>sqlite，并在此文件夹下解压上面两个压缩文件，将得到 sqlite3.def、sqlite3.dll 和 sqlite3.exe 文件。

    *   添加 C:\>sqlite 到 PATH 环境变量，最后在命令提示符下，使用 **sqlite3** 命令，将显示如下结果。

```
C:\>sqlite3
SQLite version 3.7.15.2 2013-01-09 11:53:05
Enter ".help" for instructions
Enter SQL statements terminated with a ";"
sqlite>
```

## 在 Linux 上安装 SQLite

目前，几乎所有版本的 Linux 操作系统都附带 SQLite。所以，只要使用下面的命令来检查您的机器上是否已经安装了 SQLite。

```
$sqlite3
SQLite version 3.7.15.2 2013-01-09 11:53:05
Enter ".help" for instructions
Enter SQL statements terminated with a ";"
sqlite>
```

如果没有看到上面的结果，那么就意味着没有在 Linux 机器上安装 SQLite。因此，让我们按照下面的步骤安装 SQLite：

*   请访问 [SQLite 下载页面](http://www.sqlite.org/download.html)，从源代码区下载 **sqlite-autoconf-*.tar.gz**。

*   步骤如下：

```
$tar xvfz sqlite-autoconf-3071502.tar.gz
$cd sqlite-autoconf-3071502
$./configure --prefix=/usr/local
$make
$make install
```

上述步骤将在 Linux 机器上安装 SQLite，您可以按照上述讲解的进行验证。

## 在 Mac OS X 上安装 SQLite

最新版本的 Mac OS X 会预安装 SQLite，但是如果没有可用的安装，只需按照如下步骤进行：

*   请访问 [SQLite 下载页面](http://www.sqlite.org/download.html)，从源代码区下载 **sqlite-autoconf-*.tar.gz**。

*   步骤如下：

```
$tar xvfz sqlite-autoconf-3071502.tar.gz
$cd sqlite-autoconf-3071502
$./configure --prefix=/usr/local
$make
$make install
```

上述步骤将在 Mac OS X 机器上安装 SQLite，您可以使用下列命令进行验证：

```
$sqlite3
SQLite version 3.7.15.2 2013-01-09 11:53:05
Enter ".help" for instructions
Enter SQL statements terminated with a ";"
sqlite>
```

最后，在 SQLite 命令提示符下，使用 SQLite 命令做练习。