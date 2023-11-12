# MySQL OBDC驱动下载安装

## 一、[下载](https://dev.mysql.com/downloads/connector/odbc/)ODBC驱动安装包

1、选择自己电脑 MySQL 版本 OBDC 驱动
  
2、点击 ***No thanks，just start my download*** 即可开始下载

3、下载完安装包后，双击打开安装包，按照默认选项进行安装即可。

## 二、配置数据源

1、打开控制面板 -> 系统和安全 -> windous 工具 ->ODBC数据原 （选择电脑位数 ODBC 数据源）  

2、找到[**添加**]按钮，然后选择***MySQL ODBC 8.0 Unicode Driver***
> 【注意】  

* MySQL ODBC 8.0 ANSI Driver 只针对有限的字符集的范围；
* MySQL ODBC 8.0 Unicode Driver 提供了更多字符集的支持，也就是提供了多语言的支持。

3、填写配置信息

前两个选项可根据项目功能信息填写；然后按具体情况填写TCP/IP Server和Port；然后是MySQL用户名、密码、数据库名称。
>【说明】  

Data Source Name：数据源名称，可自拟  
Description：数据源的描述，可不填写  
TCP/IP Server：服务器名称，可以填写 ***localhost***  
Port：MySQL服务的端口号，默认是3306  
User：用户名，默认是root  
Password：密码  
Database：数据库名称，自己选择数据库

填写完后可点击【Test】按钮，测试一下连接是否配置成功！如果成功会有成功提示！

若测试成功，再点击【OK】按钮即可！
