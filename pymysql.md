![image-20260706223304709](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260706223304709.png)

### 1. 第一步：建立连接 (Connect)

就像打电话要先拨号，操作数据库的第一步是建立连接。你需要提供数据库的地址、账号、密码等信息。

python

```
import pymysql

# 建立与MySQL数据库的连接
connection = pymysql.connect(
    host='localhost',      # 数据库地址，本机就是 'localhost' 或 '127.0.0.1'
    user='root',           # 你的数据库用户名
    password='你的密码',    # 你的数据库密码
    database='你的数据库名', # 你要操作的数据库名称
    port=3306,             # 端口号，MySQL默认是3306
    charset='utf8mb4'      # 字符编码，为了正确显示中文
)
print("数据库连接成功！")
```



### 2. 第二步：创建游标 (Cursor)

连接成功后，需要创建一个“游标”对象。它就像一个“操作手”，后续所有的SQL语句都要通过它来执行。

python

```
# 创建一个游标对象
cursor = connection.cursor()
```



### 3. 第三步：执行SQL语句 (Execute)

这是最核心的一步，通过游标来执行各种SQL命令。

#### 查询数据 (Read)

python

```
# 编写SQL查询语句
sql = "SELECT * FROM 你的表名"

# 执行SQL语句
cursor.execute(sql)

# 获取所有查询结果
results = cursor.fetchall()
for row in results:
    print(row)  # 每一行数据会以元组形式返回
```



- `fetchall()`: 获取所有结果。
- `fetchone()`: 获取结果集中的下一条记录。
- `fetchmany(n)`: 获取结果集中的下 n 条记录。

#### 增、删、改数据 (Create, Update, Delete)

对于会修改数据的操作（插入、更新、删除），除了执行SQL，还必须 **`commit`（提交）**，才能真正把修改保存到数据库里。

python

```
# 1. 插入数据
insert_sql = "INSERT INTO 你的表名 (列1, 列2) VALUES (%s, %s)"
# 注意：数据用元组传递给execute，可以防止SQL注入[citation:2]
data = ('值1', '值2')

try:
    cursor.execute(insert_sql, data)
    # 提交事务，非常重要！
    connection.commit()
    print("数据插入成功！")
except Exception as e:
    # 如果出错，可以回滚撤销操作
    connection.rollback()
    print(f"操作失败：{e}")

# 2. 更新和删除，逻辑完全相同，只需更换SQL语句
# update_sql = "UPDATE 你的表名 SET 列1 = %s WHERE 条件"
# delete_sql = "DELETE FROM 你的表名 WHERE 条件"
```



**关于 `%s` 占位符**：在SQL语句中用 `%s` 作为占位符，然后把真实数据作为第二个参数传给 `execute()`，这是**非常推荐的做法**，能有效防止SQL注入攻击，保证程序安全。

### 4. 第四步：收尾清理 (Close)

操作完成后，需要关闭游标和连接，释放资源。

python

```
# 先关闭游标，再关闭连接
cursor.close()
connection.close()
print("数据库连接已关闭。")
```

##### 游标（Cursor）的 `scroll()` 方法

移动光标位置

`cursor.scroll(value, mode='relative')`

`'relative'`（相对当前位置）或 `'absolute'`（绝对位置）

##### 返回数据默认是元组，可以在定义光标是修改为元组

`cursor=conn.cursor(cursor=pymysql.cursors.DictCursor)`

### 模板

```python
import pymysql

try:
    conn = pymysql.connect(
        host="localhost",
        user="root",
        passwd="root",
        db="b1",
        charset="utf8mb4"
    )
    cursor = conn.cursor()
    #sql语句
    sql=""

    cursor.execute(sql)
    conn.commit()



except pymysql.MySQLError as e:
    print(f"数据库操作出错: {e}")

finally:

    if conn:
        cursor.close()
        conn.close()
        print("资源已释放。")
```





```
import pymysql

try:
    # 1. 建立连接
    conn = pymysql.connect(
        host='localhost',
        user='root',
        password='your_password',
        database='your_database',
        charset='utf8mb4'
    )
    # 2. 创建游标
    cursor = conn.cursor()

    # 3. 执行SQL操作：创建一张测试表
    cursor.execute("CREATE TABLE IF NOT EXISTS users (id INT, name VARCHAR(20))")
    
    # 执行SQL操作：插入一条数据
    cursor.execute("INSERT INTO users (id, name) VALUES (%s, %s)", (1, 'Alice'))
    
    # 执行SQL操作：查询数据
    cursor.execute("SELECT * FROM users")
    result = cursor.fetchall()
    print("查询结果:", result) # 输出: 查询结果: ((1, 'Alice'),)

    # 提交事务，保存更改
    conn.commit()
    
except pymysql.MySQLError as e:
    print(f"数据库操作出错: {e}")
    # 如果出错，可以在这里执行 conn.rollback()
finally:
    # 4. 清理资源（无论是否出错，都尝试关闭连接）
    if conn:
        cursor.close()
        conn.close()
        print("资源已释放。")
```

### 事务

一组sql操作，要么**全部成功**，要么**全部失败**（回滚）

> 就像银行转账：A转给B 100元，A扣钱和B加钱必须同时成功，不能只做一半。

数据库开启事务：`start transaction`

回滚：`rollback`

提交事务（保留更改）：`commit`不提交保存不上

pymysql就是基于事务来完成的，默认自动开启事务，之前的`conn.commit()`就是其中一条操作

| 方法                      | 作用         | 说明                                 |
| :------------------------ | :----------- | :----------------------------------- |
| `connection.begin()`      | 开始事务     | PyMySQL默认自动开始，可省略          |
| `connection.commit()`     | 提交事务     | 保存所有更改，永久生效               |
| `connection.rollback()`   | 回滚事务     | 撤销所有未提交的更改                 |
| `connection.autocommit()` | 自动提交模式 | True=每条SQL自动提交，False=手动提交 |

### Savepoint(保留点)

**Savepoint（保存点）** 是在事务内部设置的**标记点**，允许你**回滚到事务的某个中间状态**，而不是全部回滚

数据库操作:直接在你想设的保存点语句后加`savepoint 保存点名称；`

`rollback to savepoint 保存点名称；`回滚到保存点

`release savepoint 保存点名称`删除保存点

pymysql操作：要用游标来执行；`cursor.execute("savepoint sp1")`