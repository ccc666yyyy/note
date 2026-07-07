# MySql

启动MySql服务:

直接在此电脑-管理-服务中打开和关闭

以管理员身份运行cmd输入`net start MySQL80`停止`net stop MySQL80`



### 什么是数据库

存储数据的仓库，用户可以对数据库中的数据进行增删改查询

### 数据库管理系统DBMS

**用于创建、管理、维护和操作数据库的软件系统**，MySql就是其中一种

![image-20260706141345188](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260706141345188.png)

### sql-结构化查询语言

- **SQL语言分类**：
  - **DDL（数据定义语言）**：操作表结构（如 `CREATE`， `ALTER`）。
  - **DML（数据操作语言）**：操作数据（如 `INSERT`， `UPDATE`， `DELETE`）。
  - **DQL（数据查询语言）**：最核心的查询（`SELECT`）。
  - **DCL（数据控制语言）**：管理权限（如 `GRANT`）。

![image-20260706141746924](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260706141746924.png)

语法：

可单行多行书写，以分号结尾；空格目的是增加可读性；不区分大小写；关键字建议大写提高执行速度

![image-20260706095144419](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260706095144419.png)

后面的参数是显示长度

![image-20260706095227853](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260706095227853.png)

decimal(m,d)**一种精确数值类型，用于存储需要绝对精确的小数，不会出现浮点数（如 `FLOAT`/`DOUBLE`）的精度丢失问题。**

![image-20260706095308618](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260706095308618.png)

最好用varchar

![image-20260706095635170](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260706095635170.png)

| 分类           | 命令（全小写）                          | 说明 / 示例                    |
| :------------- | :-------------------------------------- | :----------------------------- |
| **连接与退出** | `mysql -u root -p`                      | 连接本地数据库（回车后输密码） |
|                | `mysql -h 127.0.0.1 -p 3306 -u root -p` | 连接远程/指定端口数据库        |
|                | `exit;` 或 `quit;`                      | 退出 mysql 命令行客户端        |

或者可以直接winR选择调用

### DDL语句，做架构

| **数据库操作** | `show databases;`                                        | 查看所有数据库           |
| -------------- | -------------------------------------------------------- | ------------------------ |
|                | `create database db_name default character set utf8mb4;` | 创建数据库               |
|                | `show create database db_name`                           | 显示该数据库定义信息     |
|                | `use db_name;`                                           | 切换到指定数据库         |
|                | `select database();`                                     | 查看当前正在使用的库名   |
|                | `drop database db_name;`                                 | 删除数据库               |
|                | `creat database if not exits name`                       | 判断是否存在并创建数据库 |

| **表操作** | `show tables;`                                               | 查看当前库中的所有表           |
| ---------- | ------------------------------------------------------------ | ------------------------------ |
|            | `desc table_name;`                                           | 查看表结构（字段信息）         |
|            | `show create table table_name;`                              | 查看建表语句（含引擎、字符集） |
|            | `create table t (id int);`                                   | 创建表（括号内定义字段）       |
|            | `creat table new_name like table_name`                       | 创建一个与已存在表结构相同的表 |
|            | `alter table t add col varchar(10);`                         | 增加字段(列)                   |
|            | `alter table t modify col int;`                              | 修改字段类型                   |
|            | `alter table t drop col;`                                    | 删除字段                       |
|            | `rename table t to t_new;`或`alter table employee rename employee1;` | 重命名表                       |
|            | `alter table table_name character set ..`                    | 修改表的字符集                 |
|            | `drop table t;`                                              | 删除表                         |
|            | `drop table if exists table_name`                            | 如果存在则删除表               |
|            | `truncate table emp;`                                        | 删除整张表保留结构             |

修改列名：`alter table table_name change column old_name new_name 类型`

注：也可以不加column,效果一样

### DML-对表中数据进行操作

##### 插入字段

`insert into table_name (字段名1，字段名2...) values(值1，值2...)`

注意：要一一对应；非字符型加单引号；如果插入全部字段可以省略字段

`select * from table_name`查询数据

##### 复制表内数据(蠕虫复制)

`insert into table_name1 select * from table_name2`

`insert into table_name1(字段1，字段2..) select 字段1，字段2.. from table_name2`

##### 更新表记录

`update table_name set 字段名1='值'，字段名2='值' where 限定条件`

##### 删除表记录

`delete from table_name where 限定条件`

delete不加限定条件：将表中数据一条一条删除

`truncate table table_name`:是将整张表摧毁，然后创建一个与原来结构相同的表

### DQL-查询表中数据

一种显示数据的方式，不修改数据

`select *(列名) from table_name;`

##### 别名查询

`select 字段名1 as 别名,... from table_name`

时显示出来的表列名为你指定的别名

##### 清除重复值

`select distinct 字段名，.. from table_name;`

##### 查询结果参与运算（只能为数值类型）

`select 列名1+列名2（或者固定值） from table_name`

这里也可以取别名as可以省略



### 条件查询

主要修改where后面的条件

比较运算符

逻辑运算符：and or not

in 关键字：`select * from table_name where 列名 in(值1，值2..)`

范围：`列名 值1 and 值2`-->值1<=列名<=值2

### 模糊查询-like

`select * from 表名 where 字段名 like '通配符字符串'`

通配符：

`%` 表示0个或多个字符（%笔记本%匹配`**笔记本**`）

`_`表示一个字符

### 排序-order by

`select (字段名)/* from 表名 where （字段=值,条件自定义可写可不写） order by 字段名 asc/desc`

`asc`:升序，默认升序

`desc`:降序

多列排序先按第一列，再按第二列：`SELECT * FROM students ORDER BY age ASC, score DESC;`

### 聚合函数

纵向查询，队列进行查询

![image-20260706171119598](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260706171119598.png)

`select count(列名) from table_name`不统计空值

`select count(*) from table_name`统计空值

### 分组查询-group by

基本语法：`select * from table_name group by 列名`,按照指定的列名进行分组，返回每一组的第一条数据

搭配聚合函数使用：`select sum(age) from table_name group by 列名`(统计每组年龄总和)

显示信息更易读：`select 列名,sum(age) from table_name group by 列名`

对分组后的数据进行条件限制-`having`:`select 列名,count(*) from table_name where age>=30 group by 列名 having count(*)>2`

**where是对分组前的数据进行限定，where后面不可以加聚合函数**



### 限制查询条数-limit语句

limit语句放在所有语句之后，便于读取

`select * from table_name limit offset,length`从offset（默认是0）条开始查，查length条



### 约束

**“约束”就是施加在表或字段上的“强制规则”**，用来保证数据的准确性和可靠性（比如不允许为空、不能重复等）。

| 约束类型   | 关键词        | 核心作用（白话解释）                                         |
| :--------- | :------------ | :----------------------------------------------------------- |
| **主键**   | `primary key` | 唯一标识一行数据，**既不能重复也不能为空**（一张表只能有1个） |
| **外键**   | `foreign key` | 强制表与表之间的关联关系（比如订单里的用户ID，必须在用户表里存在）**可以有重复也可以有空值** |
| **唯一键** | `unique`      | 确保该列所有数据**不能重复**（但允许有多个 `null` 空值）     |
| **非空**   | `not null`    | 强制该列**必须有值**，插入时不写会报错                       |
| **默认值** | `default`     | 如果插入时没给值，自动填入设定的默认值（比如状态默认 1）     |
| **检查**   | `check`       | 自定义逻辑校验（比如年龄必须 > 0）。8.0以上版本              |



### 主键约束：

创建表时直接指定：

`create table b1(id int primary key,name varchar(20));`

`create table b1(id int primary key auto_increment,name varchar(20));`

表已经创建添加主键列：

`alter table emp add primary key(id);`

**设置自动增长:**

条件：唯一自动增长列；该列类型为整形；只能添加在具备主键约束和唯一性约束的列上

`alter table emp modify id int auto_increment;`

注：默认从1开始，也可以自定义修改`alter table table_name auto_increment=10`

**这里也可以体现delete 和truncate的区别：**

delete删除后不会重置auto_increment的值

truncate会重置

删除主键：

如果自动增长需要先去掉自动增长

`alter table  emp modify id int;`

`alter table emp drop primary key;`



### 唯一键约束

创建表时在`字段名 类型 `后面加`unique`关键字

如果出现多个`null`不算重复

### 非空约束

`字段名 字段类型 not null`

### 外键约束：

先新建另一个参照表，设置主键约束和自动增长（必须要有主键约束）create table departments(id int ,name varchar(30),location_id int);

alter table departments add primary key(id)；

 alter table departments modify id int auto_increment;

可以用以下方法查看：

![image-20260706120240133](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260706120240133.png)

在本表添加约束列`alter table emp add dept_id int;`

![image-20260706120432942](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260706120432942.png)

设置外键约束`alter table emp add constraint emp_fk foreign key(dept_id) references departments(id);`（emp_fk自定义名字）

显示添加成功：

![image-20260706120452416](C:\Users\cmy19\AppData\Roaming\Typora\typora-user-images\image-20260706120452416.png)

或者使用show create table emp;查看是否添加成功

![image-20260706121218927](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260706121218927.png)

删除外界约束：

`alter table table_name drop foreing key 约束名(emp_fk)`



### 默认值

`字段名 字段类型 default 默认值`