# PythonBug

## 目录

- [PythonBug](#PythonBug)
  - [目录](#目录)
    - [bug总结](#bug总结)
    - [注意事项]
    - [项目启动中注意事项](#项目启动中注意事项)
    - [pytest-check学习](#pytest-check学习)
      - [案例](#案例)
      - [pytest-check有的方法](#pytest-check有的方法)
      - [操作](#操作)
    - [转义字符](#转义字符)

### python 项目环境克隆

1. **克隆环境创建一个新虚拟环境**  
如果像克隆base 环境名就是 base  

```powershell
conda create --name 新环境的名称 --clone 老环境名称
```

2. **安装打包工具**  

安装conda-forge和conda-pack  
conda-pack是打包工具  

```powershell
conda install -c conda-forge conda-pack
```

3. **打包新环境**  
添加-o参数，例如将上述环境导出为新环境.tar.gz压缩包  

```powershell
conda pack -n 新环境名称 -o 新环境名称.tar.gz
```  

4. **将压缩包放到目标主机的同版本Anaconda路径下的envs文件夹内，解压**  
*注意：需要相同版本的Anaconda*  

5. **在目标主机上激活环境**  

```powershell
conda activate 新环境
```

6. **新环境bug**  

pip 不可以使用

- 卸载PIP的命令：python -m pip uninstall pip
- 重装PIP的命令：python -m ensurepip
- 升级PIP的命令：python -m pip install --upgrade pip

### 项目启动中注意事项

- 1、产测模式可以修改 **MAC**，**STBID**  
- 2、串口需要打开不然终端不能控制机顶盒  
- 3、机顶盒终端控制使用命令行控制（类似Linux操作）  
- 4、机顶盒已经烧录完成不需要重新进行烧录(机顶盒上U盘里的文件都是无用文件可以删除)  
- 5、无法识别图像，连接机顶盒的线松动了
- 7、机顶盒进行模拟遥控操作需要放在黑色盒子里
- 6、数据库连接失败是由于网络连接错，没有连接内网
- 7、param.py文件里除了串口正确其他都不可以不修改（有需求的时候可以特定修改）
- 8、U盘挂载路径：1）U盘路径 2）方法：get_usb_path()
- 9、直播点播：直播点播功能只能在湖北电信机顶盒在特定网络下才可以连接播放页面

### pytest-check学习

>pytest 测试断言方法
>比较 check 和 assert
>assert python 自带的断言方法　特点：判断错误进程就结束了
>check pytest 单元测试框架方法 特点：判断错误也不会结束进程

#### 案例

```python
import pytest_check as check

def test_example():
    a = 1
    b = 2
    c = [2, 4, 6]
    check.greater(a, b)
    check.less_equal(b, a)
    check.is_in(a, c, "Is 1 in the list")
    check.is_not_in(b, c, "make sure 2 isn't in list")
```

#### pytest-check有的方法

- check.equal - a == b
- check.not_equal - a != b
- check.is_ - a is b
- check.is_not - a is not b
- check.is_true - bool(x) is True
- check.is_false - bool(x) is False
- check.is_none - x is None
- check.is_not_none - x is not None
- check.is_in - a in b
- check.is_not_in - a not in b
- check.is_instance - isinstance(a, b)
- check.is_not_instance - not isinstance(a, b)
- check.almost_equal - a == pytest.approx(b, rel, abs) see at: pytest.approx
- check.not_almost_equal - a != pytest.approx(b, rel, abs) see at: pytest.approx
- check.greater - a > b
- check.greater_equal - a >= b
- check.less - a < b
- check.less_equal - a <= b
- check.raises - func raises given exception similar to pytest.raises

#### 操作

1、创建 test_youName.py
![创建 test_youName.py](https://img-blog.csdnimg.cn/56b712f3a5f9414e9fe372acccf7be10.png)

### 转义字符

| 转义字符 | 意义 | ASCII码值（十进制）|
| :---: | --- | :---: |
|\a|响铃(BEL)|7|
|\b|退格(BS) ，将当前位置移到前一列|8|
|\f|换页(FF)，将当前位置移到下页开头12|
|\n|换行(LF) ，将当前位置移到下一行开头|10|
|\r|回车(CR) ，将当前位置移到本行开头|13|
|\t|水平制表(HT)（跳到下一个TAB位置）|9|
|\v|垂直制表(VT)|11|
|\\|代表一个反斜线字符''\'|92|
|\'|代表一个单引号（撇号）字符|39|
|\"|代表一个双引号字符|34|
|\?|代表一个问号|63|
|\0|空字符(NULL)|0|
|\ooo|1到3位八进制数所代表的任意字符|三位八进制|
|\xhh|1到2位十六进制所代表的任意字符|二位十六进制|

您可以通过在标题行中的连字符的左侧，右侧或两侧添加冒号（:），将列中的文本对齐到左侧，右侧或中心。
| Syntax      | Description | Test Text     |
| :---        |    :----:   |          ---: |
| Header      | Title       | Here's this   |
| Paragraph   | Text        | And more      |

## BUG总结

### 1. SyntaxError: (unicode error) 'utf-8' codec can't decode byte 0xa3 in position 1: invalid start 

语法错误：有中文不能识别

#### 解决方法

方法一
> 删除UTF-8编码，使用ASCII编码  
> 删除所有中文编码

方法二
> 注明脚本编译方式
> 在python注明脚本编译方式

``` python
#!/usr/bin/python
# -*- coding: UTF-8 -*-
```

### 2、IndentationError: unexpected indent 意外缩进

// python 代码运行到这里就停止，相当于断点
import pdb
pdb.set_trace()

### 3、如何设置pycharm，才能使代码按照相对路径查找文件成功

选中项目工程根目录，右键，选择Mark Directory as ，选择 Sources Root，程序里面就可以按照相对路径查找了。

### 4、Error synchronizing data with database

原因：SQL 错误 [1062] [23000]: Duplicate entry '1163-STB-0110' for key 'case_list.PRIMARY'
即插入数据时，要插入数据的主键数据(…)已经存在，不能再重复添加了。例：Duplicate entry '1163-STB-0110' for key ‘PRIMARY是指主键为'1163-STB-0110'的数据已经存在，不能再插入主键值为0的数据了。

### 5、permission denied（linux）没有权限错误

### 6、AttributeError: 'NoneType' object has no attribute 'find_all'

爬虫错误：数据类型找不到

### 7、UnicodeDecodeError: 'gbk' codec can't decode byte 0xa3 in position 4593: illegal multibyte sequence "gdk"编码错误

方法一：
>每页代码最上行添加 # -*- coding: "utf-8" -*-

方法二：
>看报错信息  
>找有 open 函数的代码 
![在这里插入图片描述](https://img-blog.csdnimg.cn/92e80c4bbd0844a9910f35982497b436.jpeg)
>添加 encoding='utf-8'
![在这里插入图片描述](https://img-blog.csdnimg.cn/2e9ca22002c44bf6867412a34a4326c2.png)