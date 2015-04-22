# SQLite – Java

## 安装

在 Java 程序中使用 SQLite 之前，我们需要确保机器上已经有 SQLite JDBC Driver 驱动程序和 Java。可以查看 Java 教程了解如何在计算机上安装 Java。现在，我们来看看如何在机器上安装 SQLite JDBC 驱动程序。

* 从 [sqlite-jdbc](https://bitbucket.org/xerial/sqlite-jdbc/downloads) 库下载 _sqlite-jdbc-(VERSION).jar_ 的最新版本。
* 在您的 class 路径中添加下载的 jar 文件 _sqlite-jdbc-(VERSION).jar_，或者在 -classpath 选项中使用它，这将在后面的实例中进行讲解。

在学习下面部分的知识之前，您必须对 Java JDBC 概念有初步了解。如果您还未了解相关知识，那么建议您可以先花半个小时学习下 JDBC 教程相关知识，这将有助于您学习接下来讲解的知识。

## 连接数据库

下面的 Java 程序显示了如何连接到一个现有的数据库。如果数据库不存在，那么它就会被创建，最后将返回一个数据库对象。

```
    import java.sql.*;

    public class SQLiteJDBC
    {
      public static void main( String args[] )
      {
        Connection c = null;
        try {
          Class.forName("org.sqlite.JDBC");
          c = DriverManager.getConnection("jdbc:sqlite:test.db");
        } catch ( Exception e ) {
          System.err.println( e.getClass().getName() + ": " + e.getMessage() );
          System.exit(0);
        }
        System.out.println("Opened database successfully");
      }
    }
```

现在，让我们来编译和运行上面的程序，在当前目录中创建我们的数据库 **test.db**。您可以根据需要改变路径。我们假设当前路径下可用的 JDBC 驱动程序的版本是 _sqlite-jdbc-3.7.2.jar_。

```
    $javac SQLiteJDBC.java
    $java -classpath ".:sqlite-jdbc-3.7.2.jar" SQLiteJDBC
    Open database successfully
```

如果您想要使用 Windows 机器，可以按照下列所示编译和运行您的代码：

```
    $javac SQLiteJDBC.java
    $java -classpath ".;sqlite-jdbc-3.7.2.jar" SQLiteJDBC
    Opened database successfully
```

## 创建表

下面的 Java 程序将用于在先前创建的数据库中创建一个表：

```
    import java.sql.*;

    public class SQLiteJDBC
    {
      public static void main( String args[] )
      {
        Connection c = null;
        Statement stmt = null;
        try {
          Class.forName("org.sqlite.JDBC");
          c = DriverManager.getConnection("jdbc:sqlite:test.db");
          System.out.println("Opened database successfully");

          stmt = c.createStatement();
          String sql = "CREATE TABLE COMPANY " +
                       "(ID INT PRIMARY KEY     NOT NULL," +
                       " NAME           TEXT    NOT NULL, " +
                       " AGE            INT     NOT NULL, " +
                       " ADDRESS        CHAR(50), " +
                       " SALARY         REAL)";
          stmt.executeUpdate(sql);
          stmt.close();
          c.close();
        } catch ( Exception e ) {
          System.err.println( e.getClass().getName() + ": " + e.getMessage() );
          System.exit(0);
        }
        System.out.println("Table created successfully");
      }
    }
```

上述程序编译和执行时，它会在 **test.db** 中创建 COMPANY 表，最终文件列表如下所示：

```
    -rw-r--r--. 1 root root 3201128 Jan 22 19:04 sqlite-jdbc-3.7.2.jar
    -rw-r--r--. 1 root root    1506 May  8 05:43 SQLiteJDBC.class
    -rw-r--r--. 1 root root     832 May  8 05:42 SQLiteJDBC.java
    -rw-r--r--. 1 root root    3072 May  8 05:43 test.db
```

## INSERT 操作

下面的 Java 代码显示了如何在上面创建的 COMPANY 表中创建记录：

```
    import java.sql.*;

    public class SQLiteJDBC
    {
      public static void main( String args[] )
      {
        Connection c = null;
        Statement stmt = null;
        try {
          Class.forName("org.sqlite.JDBC");
          c = DriverManager.getConnection("jdbc:sqlite:test.db");
          c.setAutoCommit(false);
          System.out.println("Opened database successfully");

          stmt = c.createStatement();
          String sql = "INSERT INTO COMPANY (ID,NAME,AGE,ADDRESS,SALARY) " +
                       "VALUES (1, 'Paul', 32, 'California', 20000.00 );";
          stmt.executeUpdate(sql);

          sql = "INSERT INTO COMPANY (ID,NAME,AGE,ADDRESS,SALARY) " +
                "VALUES (2, 'Allen', 25, 'Texas', 15000.00 );";
          stmt.executeUpdate(sql);

          sql = "INSERT INTO COMPANY (ID,NAME,AGE,ADDRESS,SALARY) " +
                "VALUES (3, 'Teddy', 23, 'Norway', 20000.00 );";
          stmt.executeUpdate(sql);

          sql = "INSERT INTO COMPANY (ID,NAME,AGE,ADDRESS,SALARY) " +
                "VALUES (4, 'Mark', 25, 'Rich-Mond ', 65000.00 );";
          stmt.executeUpdate(sql);

          stmt.close();
          c.commit();
          c.close();
        } catch ( Exception e ) {
          System.err.println( e.getClass().getName() + ": " + e.getMessage() );
          System.exit(0);
        }
        System.out.println("Records created successfully");
      }
    }
```

上述程序编译和执行时，它会在 COMPANY 表中创建给定记录，并会显示以下两行：

```
    Opened database successfully
    Records created successfully
```

## SELECT 操作

下面的 Java 程序显示了如何从前面创建的 COMPANY 表中获取并显示记录：

```
    import java.sql.*;

    public class SQLiteJDBC
    {
      public static void main( String args[] )
      {
        Connection c = null;
        Statement stmt = null;
        try {
          Class.forName("org.sqlite.JDBC");
          c = DriverManager.getConnection("jdbc:sqlite:test.db");
          c.setAutoCommit(false);
          System.out.println("Opened database successfully");

          stmt = c.createStatement();
          ResultSet rs = stmt.executeQuery( "SELECT * FROM COMPANY;" );
          while ( rs.next() ) {
             int id = rs.getInt("id");
             String  name = rs.getString("name");
             int age  = rs.getInt("age");
             String  address = rs.getString("address");
             float salary = rs.getFloat("salary");
             System.out.println( "ID = " + id );
             System.out.println( "NAME = " + name );
             System.out.println( "AGE = " + age );
             System.out.println( "ADDRESS = " + address );
             System.out.println( "SALARY = " + salary );
             System.out.println();
          }
          rs.close();
          stmt.close();
          c.close();
        } catch ( Exception e ) {
          System.err.println( e.getClass().getName() + ": " + e.getMessage() );
          System.exit(0);
        }
        System.out.println("Operation done successfully");
      }
    }
```

上述程序编译和执行时，它会产生以下结果：

```
    Opened database successfully
    ID = 1
    NAME = Paul
    AGE = 32
    ADDRESS = California
    SALARY = 20000.0

    ID = 2
    NAME = Allen
    AGE = 25
    ADDRESS = Texas
    SALARY = 15000.0

    ID = 3
    NAME = Teddy
    AGE = 23
    ADDRESS = Norway
    SALARY = 20000.0

    ID = 4
    NAME = Mark
    AGE = 25
    ADDRESS = Rich-Mond
    SALARY = 65000.0

    Operation done successfully
```

## UPDATE 操作

下面的 Java 代码显示了如何使用 UPDATE 语句来更新任何记录，然后从 COMPANY 表中获取并显示更新的记录：

```
    import java.sql.*;

    public class SQLiteJDBC
    {
      public static void main( String args[] )
      {
        Connection c = null;
        Statement stmt = null;
        try {
          Class.forName("org.sqlite.JDBC");
          c = DriverManager.getConnection("jdbc:sqlite:test.db");
          c.setAutoCommit(false);
          System.out.println("Opened database successfully");

          stmt = c.createStatement();
          String sql = "UPDATE COMPANY set SALARY = 25000.00 where ID=1;";
          stmt.executeUpdate(sql);
          c.commit();

          ResultSet rs = stmt.executeQuery( "SELECT * FROM COMPANY;" );
          while ( rs.next() ) {
             int id = rs.getInt("id");
             String  name = rs.getString("name");
             int age  = rs.getInt("age");
             String  address = rs.getString("address");
             float salary = rs.getFloat("salary");
             System.out.println( "ID = " + id );
             System.out.println( "NAME = " + name );
             System.out.println( "AGE = " + age );
             System.out.println( "ADDRESS = " + address );
             System.out.println( "SALARY = " + salary );
             System.out.println();
          }
          rs.close();
          stmt.close();
          c.close();
        } catch ( Exception e ) {
          System.err.println( e.getClass().getName() + ": " + e.getMessage() );
          System.exit(0);
        }
        System.out.println("Operation done successfully");
      }
    }
```

上述程序编译和执行时，它会产生以下结果：

```
    Opened database successfully
    ID = 1
    NAME = Paul
    AGE = 32
    ADDRESS = California
    SALARY = 25000.0

    ID = 2
    NAME = Allen
    AGE = 25
    ADDRESS = Texas
    SALARY = 15000.0

    ID = 3
    NAME = Teddy
    AGE = 23
    ADDRESS = Norway
    SALARY = 20000.0

    ID = 4
    NAME = Mark
    AGE = 25
    ADDRESS = Rich-Mond
    SALARY = 65000.0

    Operation done successfully
```

## DELETE 操作

下面的 Java 代码显示了如何使用 DELETE 语句删除任何记录，然后从 COMPANY 表中获取并显示剩余的记录：

```
    import java.sql.*;

    public class SQLiteJDBC
    {
      public static void main( String args[] )
      {
        Connection c = null;
        Statement stmt = null;
        try {
          Class.forName("org.sqlite.JDBC");
          c = DriverManager.getConnection("jdbc:sqlite:test.db");
          c.setAutoCommit(false);
          System.out.println("Opened database successfully");

          stmt = c.createStatement();
          String sql = "DELETE from COMPANY where ID=2;";
          stmt.executeUpdate(sql);
          c.commit();

          ResultSet rs = stmt.executeQuery( "SELECT * FROM COMPANY;" );
          while ( rs.next() ) {
             int id = rs.getInt("id");
             String  name = rs.getString("name");
             int age  = rs.getInt("age");
             String  address = rs.getString("address");
             float salary = rs.getFloat("salary");
             System.out.println( "ID = " + id );
             System.out.println( "NAME = " + name );
             System.out.println( "AGE = " + age );
             System.out.println( "ADDRESS = " + address );
             System.out.println( "SALARY = " + salary );
             System.out.println();
          }
          rs.close();
          stmt.close();
          c.close();
        } catch ( Exception e ) {
          System.err.println( e.getClass().getName() + ": " + e.getMessage() );
          System.exit(0);
        }
        System.out.println("Operation done successfully");
      }
    }
```

上述程序编译和执行时，它会产生以下结果：

```
    Opened database successfully
    ID = 1
    NAME = Paul
    AGE = 32
    ADDRESS = California
    SALARY = 25000.0

    ID = 3
    NAME = Teddy
    AGE = 23
    ADDRESS = Norway
    SALARY = 20000.0

    ID = 4
    NAME = Mark
    AGE = 25
    ADDRESS = Rich-Mond
    SALARY = 65000.0

    Operation done successfully
```