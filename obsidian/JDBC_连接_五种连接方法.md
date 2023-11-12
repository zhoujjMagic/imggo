# JDBC

## 1.JDBC概念

JDBC（Java Data Base Connectivity,java数据库连接）是一种用于执行SQL语句的Java API，可以为多种关系数据库提供统一访问，它由一组用Java语言编写的类和接口组成。JDBC提供了一种基准，据此可以构建更高级的工具和接口，使数据库开发人员能够编写数据库应用程序。

## 2.数据库驱动

我们安装好数据库之后，我们的应用程序也是不能直接使用数据库的，必须要通过相应的数据库驱动程序，通过驱动程序去和数据库打交道。其实也就是数据库厂商的JDBC接口实现，即对Connection等接口的实现类的jar文件。

## JDBC 程序实例

1、MySQL驱动下载：[MySQL Download](https://downloads.mysql.com/archives/c-j/) //选择驱动版本，你的 MySQL是 8.0版本就下载 8.0驱动，不需要和数据库完全一致  
2、创建普通 Java项目,在项目中建文件夹 lib将 MySQL驱动 jar包放在里面并且***在 IDEA中右键点击 mysql.jar选择 add to Library (加入到项目中)***  

### JDBC 步骤

* 注册驱动
* 得到连接
* 实现对数据库操作
* 关闭连接资源

~~~ java
import com.mysql.cj.jdbc.Driver;

import java.sql.Connection;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Properties;

public class jdbc_connect {
    public static void main(String[] args) throws SQLException {
        //1. 注册驱动
        Driver driver = new Driver();//创建driver 对象

        // 2. 得到连接
        String url="jdbc:mysql://127.0.0.1:3306/jdbc?" +
                "useUnicode=true&characterEncoding=UTF-8&userSSL=false&serverTimezone=GMT%2B8";
        //将用户名和密码放入到Properties对象
        Properties info = new Properties();
        info.setProperty("user", "root");// 用户
        info.setProperty("password", "root"); //密码
        Connection connect = driver.connect(url, info);

        //3. 执行sql
        String sql = "insert into studnets value (1001,'令狐冲','男','560-12-12')";
        //statement 用于执行静态SQL语句并返回其生成的结果的对象
        Statement statement = connect.createStatement();
        int rows = statement.executeUpdate(sql); // dml(update insert delete)语句，返回的就是影响行数
        System.out.println(rows > 0 ? "成功" : "失败");

        //4. 关闭连接资源
        statement.close();
        connect.close();
    }
}
~~~

## JDBC五种连接方法

### 方法一

~~~ java
Driver driver = new com.mysql.cj.jdbc.Driver();
String url="jdbc:mysql://127.0.0.1:3306/jdbc?" +
            "useUnicode=true&characterEncoding=UTF-8&userSSL=false&serverTimezone=GMT%2B8";
    
//将用户名和密码放入到Properties对象
Properties properties = new Properties();
properties.setProperty("user", "root");// 用户
properties.setProperty("password", "root"); //密码
Connection connect = driver.connect(url, properties);
~~~

### 方法二

~~~ java
// 使用反射加载Driver 类，动态加载，更加灵活，减少依赖
Class<?> aClass = Class.forName("com.mysql.cj.jdbc.Driver");
Driver driver = (Driver) aClass.newInstance();
//将用户名和密码放入到Properties对象
String url="jdbc:mysql://127.0.0.1:3306/jdbc?" +
        "useUnicode=true&characterEncoding=UTF-8&userSSL=false&serverTimezone=GMT%2B8";

Properties properties = new Properties();
properties.setProperty("user","root");
properties.setProperty("password","root");
//得到连接
Connection connection = driver.connect(url, properties);
~~~

### 方法三

~~~ java
Class<?> aClass = Class.forName("com.mysql.cj.jdbc.Driver");
Driver driver = (Driver) aClass.newInstance();
// 创建 url, user, password
String url="jdbc:mysql://127.0.0.1:3306/jdbc?" +
        "useUnicode=true&characterEncoding=UTF-8&userSSL=false&serverTimezone=GMT%2B8";
String user = "root";
String password = "root";
// 使用 DriverManager注册驱动
DriverManager.registerDriver(driver);
Connection connection = DriverManager.getConnection(url, user, password);
~~~

### 方法四

~~~ java
Class<?> aClass = Class.forName("com.mysql.cj.jdbc.Driver");
Driver driver = (Driver) aClass.newInstance();

// 创建 url, user, password
String url="jdbc:mysql://127.0.0.1:3306/jdbc?" +
        "useUnicode=true&characterEncoding=UTF-8&userSSL=false&serverTimezone=GMT%2B8";
String user = "root";
String password = "root";

// 使用 DriverManager方法时，有 static方法注册了驱动
Connection connection = DriverManager.getConnection(url, user, password);
~~~

### 方法五

~~~ java
Properties properties = new Properties();
properties.load(new FileInputStream("src//mysql.properties"));
String url = properties.getProperty("url");
String user = properties.getProperty("user");
String password = properties.getProperty("password");
String driver = properties.getProperty("driver");
//1. 注册驱动
// Class.forName(driver); // 建议写上
// 2. 得到连接
Connection connection = DriverManager.getConnection(url, user, password);
~~~
