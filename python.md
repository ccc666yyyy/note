## python

### 1. 定义：

python是一种面向**对象**的**解释型**计算机程序语言；

强类型的**动态脚本**语言（不需要定义变量类型）

>**编译型**：提前把源码一次性翻译成机器码 / 二进制可执行文件，运行时直接跑二进制，**不依赖源码、速度快**，此类语言被称为静态语言

> **解释型**：运行时逐行翻译执行，自带解释器，**跨平台、开发快、部署简单，运行速度慢**，此类语言被称为脚本语言

### 2. 注意事项：

   print(value,sep' ',end'\n',file=None)

print顶格写，两个print不在一行，字符串必需要加上单引号或双引号，数字不用

ctrl+/添加或取消注释（#）  ctrl+d复制到下一行

中文声明注释：\# coding=utf-8，必须放文本顶部

sep用来间隔多个值

end用来设定以什么符号结尾，默认为换行符\n,print("字符串"，end="...")

### 3. 字面量和变量

   字面量：特定的值

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-02 184549.png)

### 4. 标识符（命名规则与c语言一样）

   只能包含字母数字和下划线；

   不能以数字开头；

   不能使用关键字(保留字）（True，False，None，and，or，if，else，elife,for,while);

   严格区分大小写



> 查保留字
>
> ```python
> import keyword
> print(keyword.kwlist)
> ```
>
> 

### 5. 值交换

   c=a a=b b=c   /a,b=b,a

### 6. 数据类型

   type(要查看的数据类型) eg:print(type("hello"))

   isinstance()检查数据是否是指定类型，返回bool值 eg:isinstance(num,int)

   ![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-02 192954.png)

### 7. 字符串

   ![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-02 193906.png)

引号内有引号，用转义符/或者内外用不同的引号

原字符：r或R，是转义字符失效的字符，在字符串前写上r

字符串的截取：

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-06-29 100427.png)

分正向索引和反向索引

```python
s='aasdfghhhhhhhhhhhhhh'
print(s[2,7]) # 从2的位置开始到7结束，不包括7

```



### 8.字符串拼接

* 直接拼接

  ![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-02 222259.png)

* 用+进行拼接

  ![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-02 222308.png)

注意+不能用来拼接字符串与非字符串，可以用**str(变量名)**将非字符串型变量**转化**为字符型变量

也可以使用join进行拼接分`隔符字符串.join(可迭代对象)`

==join 只插在**元素中间**，首尾不加分隔符==

列表里是数字不能直接 join，必须先用推导式转字符串：

```python
拼接列表：
# 1. 空分隔符，直接连起来
lst1 = ["a", "b", "c"]
res1 = "".join(lst1)
print(res1)  # abc

# 2. 逗号分隔
lst2 = ["张三", "李四", "王五"]
res2 = ",".join(lst2)
print(res2)  # 张三,李四,王五

# 3. 横线分隔
res3 = "-".join(lst2)
print(res3)  # 张三-李四-王五

num_lst = [1001, 1002, 1003]
# 错误写法：",".join(num_lst) 直接报错

# 正确：先全部转为str
res = ",".join([str(i) for i in num_lst])
print(res)  # 1001,1002,1003

元组，字符串，集合，都可以使用此方法进行拼接
```





![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-02 223526.png)

字符串格式化：

使用%s进行占位

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-02 224455.png)



f"..{变量名/表达式}.."

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-02 224723.png)

使用f"{变量名/表达式}.."的方式最为推荐

格式化用法：

{ [变量名] : [填充字符] [对齐方式] [宽度] [.精度] [类型码] }

```python
对齐与填充
num = 66
# 占8字符，右对齐，空格填充
print(f"{num:>8}")
# 占8字符，左对齐，#填充
print(f"{num:#<8}")
# 占8字符，居中，*填充
print(f"{num:*^8}")
保留小数
pi = 3.1415926
print(f"{pi:.2f}")  # 保留2位小数 → 3.14
print(f"{pi:.4f}")  # 保留4位小数 → 3.1416
千位分隔符
money = 1234567
print(f"{money:,}")  # 1,234,567
print(f"{money:,.2f}") # 1,234,567.00

进制转换
num = 25
print(f"{num:d}")    # 十进制 25
print(f"{num:x}")    # 十六进制 19
print(f"{num:%}")    # 2500.000000%
print(f"{0.123:.1%}")# 12.3%
```



format方法：

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-06-30 180119.png)

索引0，1...指定顺序





判断是否是一个字串的子串x in y：

`print('ccc' in s)`



### 9. 输入输出

输入input()  输出print（）

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-02 230215.png)

输出到文本文件：打开文件；输出；关闭文件

```python
fp=open('text.txt','w')
print('ccc',file=fp)
fp.close()
```



### 10.运算符

1. 算术运算符

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-02 230800.png)

优先级：** --> * / // % --> + -

在设计浮点数的运算中可能会出现精度损失，因为二进制无法准确地转化为浮点数

可以使用`print(round(    运算式  ,2))`对输出结果保留两位小数





2. 赋值运算符

   ![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-02 232835.png)

**有浮点数参与运算结果为浮点数**

3. 比较运算符

3. 逻辑运算符

   ![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-06-29 103456.png)

5. 优先级

   ![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-06-29 104742.png)

### 11.if语句

if 要判断的条件：

​    条件成立时，要执行的操作（前面4个空格）

```python
score=int(input("enter your score"))
if score>700:
    print("欢迎来清华")
```

if...elif...else:

```python
if 条件：
    操作1
elif 条件：
    操作2
else 条件：
    操作3
```

if...else:

```python
min=x if x<y else y
```

注：三目运算符在py中不适用

### 12.模式匹配match...case

```python
day=input()
match day:
    case "1":
        print("周一")
        
    case "6"|"7":
        print("周末")
        
    case _:
        print("错误")
```



注意与C语言的区别：匹配到一个后就会跳出，如果都匹配不到就会执行—_



### 13. while

```
while 条件：
    循环语句
else：
    循环正常结束后的语句
若循环异常结束，则不会执行else,这个else可有可无

举个例子：
i=0
while i<10:
    print("人生苦短，我用python")
    i+=1
else:
    print("end")
```



### 14. for循环

```
for 元素名 in 元素集：
    循环体代码（对元素进行处理）
else：
    语句（循环正常结束才会执行）
    
msg=input("输入要遍历的字符串：")
for s in msg:
    print(f"{s}”)
    
```



### range语句

* range(start,end,step)

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-04 190315.png)

注意：break和continue只能应用于循环体系中

pass 空语句起占位作用



### 随机数生成

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-14 213241.png)



### 统计字子串出现次数s.count()

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-14 214911.png)



### 15. 数据容器

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-14 215206.png)

### 16. 列表类型

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-14 215551.png)

数据容器定义：列表名=[1,2,3,4...]元素可以为任意类型

元素获取：列表名[索引]

元素修改：列表名[索引]=新元素

元素删除：del 列表名[索引]

遍历：

```python
for item in s:
    print(item)
    
for i in range(0,len(list)):
    print(list[i])
    
for index,item in enumerate(list):
    print(index,item)#输出序号和元素，序号默认从0开始，可以手动修改，for index,item in enumerate(list,1),此时序号从1开始
    

```



**列表切片**

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-14 220851.png)

语法：s=[start:end:step]

从0开始步长为-1，逆序输出

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-14 221902.png)

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-02-14 223522.png)

![image-20260630212427525](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260630212427525.png)



补充方法：

注意lst.reverse()无返回值，print(lst.reverse())输出None

new_list=list.copy(),列表的拷贝



对列表进行排序：

1. `lst.sort()`默认升序

​       `lst.sort(reverse=True)`降序

​       此方法在原列表上进行修改，不产生新列表对象

2. 使用内置函数sorted,产生新列表

   `new_lst=sorted(lst)`默认升序

   `new_lst=sorted(lst,reverse=Ture)`降序

   

   



如何快速合并两个列表？

```python
1.遍历列表后用s.append(num)逐个添加

for  num in num_lst2:

​    num_lst1.append(num)

2.使用+直接和并num_lst=num_lst1+num_lst2

3.使用*进行解包操作num_lst=[\*num_lst1,\*num_lst2]


```

如何判断元素是否在列表中？

语法：元素 in 列表

注意：返回为布尔值



c在s中第一次出现的索引位置？

s.index('c')

c在s中出现的个数？

s.count('c')



**列表生成式**

```python
lst = [i for i in range(1,11)]
# [1,2,3,4,5,6,7,8,9,10]

lst = [i**2 for i in range(1,6)]
# [1, 4, 9, 16, 25]

lst = [i for i in range(1,11) if i % 2 == 0]
# [2,4,6,8,10]

lst = [i if i%2==0 else 0 for i in range(1,6)]
# [0, 2, 0, 4, 0]

res = [(x,y) for x in [1,2] for y in [3,4]]
# [(1,3),(1,4),(2,3),(2,4)]
```

二维列表

```python
# 最简单的二维列表
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
#遍历
for row in matrix:
    for num in row:
        print(num, end=" ")
    print()  # 换行分隔行

    
#列表推导式
# 3行4列全0
matrix = [[0 for _ in range(4)] for _ in range(3)]
print(matrix)

# 生成有规律数字：1~9的3*3矩阵
matrix = [[i*3 + j + 1 for j in range(3)] for i in range(3)]
print(matrix)
```

### 17.元组类型

1. 定义

> 元组：**有序、不可修改**的序列容器

> 符号：小括号 `()`，元素用逗号隔开

> 和列表区别：列表 `[]` 可增删改；元组 `()` 创建后不能修改元素
>
> ==元组不能增，删，改元素==

2. 创建元组

   **t4 = (5)    # 只是数字5，int类型**

```python
# 1. 普通元组
t1 = (10, 20, 30, "hello")
print(t1)
print(type(t1))  # <class 'tuple'>

# 2. 不加括号也能创建（逗号是关键）
t2 = 1, 2, 3
print(t2)

# 3. 只有一个元素！必须加逗号，否则不是元组
t3 = (5,)   # 元组
t4 = (5)    # 只是数字5，int类型

# 4. 空元组
empty = ()
# 5. 二维元组（嵌套）
t5 = ((1,2), (3,4), (5,6))
```

3. 元组的取值和切片

   ```python
   t = (2, 4, 6, 8, 10)
   
   # 下标取值
   print(t[0])   # 2
   print(t[-1])  # 10
   
   # 切片 [起始:结束:步长]
   print(t[1:4]) # (4,6,8)
   print(t[::2]) # (2,6,10)
   ```

4. 元组遍历（与列表一样）

   ```python
   for num in t:
       print(num)
   
   for index,num in enumerate(t):
       print(f"index{index}:{num}")
       
   t=((1,2),(3,4))
   for row in t:
       for num in row:
           print(num,end=" ")
   ```

5. 列表 ↔ 元组互相转换

   ```python
   # 列表转元组 list → tuple
   lst = [1,2,3]
   t = tuple(lst)
   print(t)
   
   # 元组转列表 tuple → list（想修改时用）
   t = (10,20,30)
   lst = list(t)
   lst[0] = 99
   print(lst)
   ```

6. 元组的生成式，其结果是一个生成器对象，需要转换成元组或列表

   ```python
   t=(i for i in range(1,4))
   print(t)#输出结果是一个生成器对象
   t=tuple(t)#转换成元组
   for item in t:
       print(item)
       
   还可以使用next
   t=(i for i in range(1,4))
   print(t.__next__())#每次去一个元素依次往后
   ```

   

### 18.字典类型

1. 字典基础概念

   存储结构：**键值对（key: value）**，`{键: 值, 键: 值}`

   特点

   - 无序存储
   - **键必须不可变**：数字、字符串、元组；==列表 / 字典/集合不能当 key==
   - 键唯一，重复键会覆盖旧值
   - 值可以是任意类型（列表、元组、字典都可以）

2. 字典创建方法

   直接写 `{key:value}`，适合少量已知数据

   ```python
   d1 = {"name":"张三", "age":18, "gender":"男"}
   # 空字典
   empty1 = {}
   ```

   

   dict () 关键字参数创建,`dict(键1=值1,键2=值2)`，==键只能是字符串==，不能数字

   ```python
   d2 = dict(name="李四", age=20)
   print(d2) # {'name': '李四', 'age': 20}
   ```

   dict () 接收可迭代键值对列表 / 元组,传入 `[(k1,v1),(k2,v2)]` 配对序列

```python
d3 = dict([("id",1001), ("score",95)])
print(d3)
```

zip 映射配对创建

```python
keys = ["a","b","c"]
vals = [10,20,30]
d4 = dict(zip(keys, vals))
print(d4)
```

3. 字典取值

   `[key]` 取值（键不存在会报错）

   `.get()` 不存在返回默认值

   ```python
   d = {"name":"老王", "age":25}
   print(d["name"])  # 老王
   # print(d["height"])  # KeyError 报错
   
   print(d.get("age"))
   print(d.get("height", 170)) # 无height键，返回170
   print(d.get("height"))      # 无键返回None
   
   ```

   

4. 字典遍历

   ```python
   d = {"name":"小李", "age":19, "gender":"男"}
   
   # 1. dict.keys() 获取所有键
   print(d.keys())
   # 2. dict.values() 获取所有值
   print(d.values())
   # 3. dict.items() 获取(键,值)元组对
   print(d.items())
   
   
   d = {"name":"小李", "age":19, "gender":"男"}
   
   # 1. 直接for循环：遍历所有键
   for k in d:
       print(k, d[k])
   
   # 2. 单独遍历键
   for k in d.keys():
       print(k)
   
   # 3. 单独遍历值
   for v in d.values():
       print(v)
   
   # 4. 同时遍历键和值（最常用）
   for k, v in d.items():
       print(f"键：{k}，值：{v}")
   ```

   

6. 方法：

   ![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-06-30 150021.png)

* 添加 / 修改元素

键存在 = 修改；键不存在 = 新增

```python
d = {"a":1, "b":2}
d["c"] = 3   # 新增
d["a"] = 99  # 修改原有值
print(d) # {'a': 99, 'b': 2, 'c': 3}
```

* 删除操作

```python
d = {"a":1, "b":2, "c":3}

# del 删除指定键值对
del d["a"]
print(d)

# pop(key) 删除并返回对应值
res = d.pop("b")
print(res)

# popitem() 删除最后插入的一对，并返回对应的键值对
d.popitem()

# clear() 清空所有元素
d.clear()
```

空字典，列表，元组bool值为False

7. 字典推导式

```python
d={i:i**2 for i in range(1,5)}
#遍历循环中的1234做键，i的2次方做值

#映射、
lst1=[1,2,3]
lst2=['a','b','c']
d={key:value for key,value in zip(lst1,lst2)}

```

### 19.集合类型

##### 集合特点-可变数据类型

1. 符号：`{}`，**无序、元素唯一、可变**
2. 核心特性：自动去重，不能用下标取值（无顺序）
3. 元素限制：只能存**不可变类型**（数字、字符串、元组），==列表 / 字典 / 集合不能放进集合==

##### 创建集合

```python
#字面量创建

s1 = {1, 2, 3, 3, 2}
print(s1)  # {1,2,3} 自动去重

#set()转换创建

# 列表转集合，快速去重
lst = [1,1,2,2,3]
s2 = set(lst)
print(s2)

# 字符串转集合：拆分单个字符、去重
s3 = set("aabbcc")
print(s3) # {'a','b','c'}

# 元组转集合
t = (5,5,6)
s4 = set(t)
```

##### 集合的数学运算

```python
a = {1,2,3,4}
b = {3,4,5,6}

# 并集 | 两个集合所有元素（去重）
print(a | b)  # {1,2,3,4,5,6}
print(a.union(b))

# 交集 & 两者都有的元素
print(a & b)  # {3,4}
print(a.intersection(b))

# 差集 - a有b没有的
print(a - b)  # {1,2}
print(a.difference(b))

# 补集 ^ 只在其中一个里存在
print(a ^ b)  # {1,2,5,6}
```

##### 集合的相关操作

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-06-30 160426.png)

##### 集合的遍历

因为集合无序，不能用下标，只能用for循环遍历

```python
s = {1,3,5}
for num in s:
    print(num)
#或
for index,item in neumerate(s)
    print(index,'-->',item)
```

##### 集合的生成式（推导式）

```python
s={i for i in range(1,10)}
s={i for i in range(1,10) if i%2==0}
```



![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-06-30 161913.png)

字典合并运算符|：

`merged_dict=d1|d2`

同步迭代：同时遍历**两个 / 多个等长**的列表、元组、集合，按位置一一配对取出，叫同步迭代，核心工具：`zip()`

```python
# 两组对应数据
names = ["小明", "小红", "小刚"]
scores = [90, 88, 95]

# zip 将元素按位置配对：("小明",90) ("小红",88) ("小刚",95)
for name, score in zip(names, scores):
    print(name, score)
    
    
小明 90
小红 88
小刚 95
```



## 20.字符串与正则表达式

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-06-30 174634.png)

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-06-30 174951.png)

strip去除时与chars顺序无关，没参数就去掉空格

replace可以指定替换次数，直接加上count就行



![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-06-30 181542.png)

```python
# 原始字符串（str类型）
s = "你好Python"

# utf-8编码
b = s.encode(encoding="utf-8")
print(b)  # b'\xe4\xbd\xa0\xe5\xa5\xbdPython'  结果为bytes类型

# gbk编码
b_gbk = s.encode("gbk")
print(b_gbk) # b'\xc4\xe3\xba\xc3Python'

s = b.decode(encoding="utf-8")
```

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-07-01 084831.png)

注意：如或是占字节数，在utf_8中中文占3字节



![image-20260630182901906](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260630182901906.png)



##### 字符串去重

```python
for item in s:
    if item not in new_s:
        new_s+=item
        
for i in range(len(s)):
    if s[i] not in new_s:
        new_s+=s[i]

#通过集合去重+列表排序
new_s=set(s)#转集合
lst=list(new_s)#转列表
lst.sort(key=s.index)#还原打乱顺序
print(''.join(lst))#空字串拼接列表

```

##### 正则表达式相关符号

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-06-30 203925.png)



![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-06-30 204043.png)

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-06-30 204235.png)

##### re模块

使用前必须导入：`import re`

![image-20260630205912827](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260630205912827.png)

```python
import re  # 导入正则模块
# 正则规则：1位数字.多位数字（未加r存在转义bug）
pattern='\d\.\d+'
# 文本1：开头是字母I
s='I study Python 3.11 every day'
# match从开头匹配，开头无数字，返回None
match=re.match(pattern,s,re.I)
print(match) # None

# 文本2：开头就是小数3.11
s2='3.11Python I study every day'
# 开头匹配成功，返回匹配对象
match2=re.match(pattern,s2)
print(match2) # <re.Match object; span=(0, 4), match='3.11'>

match.group()#返回正则匹配到的完整字符串
```

![image-20260701092643495](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260701092643495.png)



统计字串出现次数：

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/屏幕截图 2026-07-01 090729.png)

### 21.python中的异常处理

```python
try:
    # 可能报错、容易出异常的代码
    执行逻辑
except 异常类型1 as e:
    # 捕获对应异常后的处理代码
   # as e = 将捕获到的异常实例存到变量e，方便打印、读取错误详情，用于调试排错
    异常处理
except 异常类型2 as e:
    # 捕获第二种异常
else:
    # try 代码无任何异常时才执行（可选）
finally:
    # 无论是否报错，最后一定会执行（可选，常用于关闭文件/释放资源）
    
```

**异常类型**：`IndexError/ValueError/ZeroDivisionError...`

![image-20260701095416439](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260701095416439.png)

![image-20260701095530234](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260701095530234.png)

纯字符 `'a'` 无法直接转整数，会抛 `ValueError`比如：`num = int("a")`会报错，可以用`ord('a')` 获取字符对应的 ASCII 码值



##### raise关键字

`raise` 用于**手动主动抛出异常**，主动触发报错，中断程序流程，配合 `try-except` 使用

```python
lst = [1,2,3]
try:
    if len(lst) < 4:
        # 主动模拟下标3越界的错误
        raise IndexError("列表长度不足，无法访问下标3")
    print(lst[3])
except IndexError as e:
    print("捕获异常：", e)
```

![image-20260701100937921](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260701100937921.png)

![image-20260701101114257](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260701101114257.png)





### 22. 函数

def 函数名（形参）：

​    函数体

函数调用：函数名（实参）

注：

* 传参是遵循位置参数在前，关键字参数在后

* 默认参数应从右至左赋值

* 返回值可以有多个，函数的返回结果赋值给一个变量是元组类型

* 没有返回值的函数`type(fun())`类型是None
* type(fun)类型是function

* 使用global在函数内部声明全局变量时，声明和赋值必须分开不能一行完成

##### 可变参数

![image-20260701104320351](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260701104320351.png)

可变位置参数：（打包成元组）

```python
def test(*para):
    print(para, type(para))

test(10,20,30)
test("苹果", "香蕉")

(10, 20, 30) <class 'tuple'>
('苹果', '香蕉') <class 'tuple'>
```

解包

```python
nums = (1,2,3)
func(*nums)  # 等价于 func(1,2,3)
```



可变关键字参数：（打包成字典)

```python
def test(**para):
    print(para, type(para))

test(name="小明", score=90)
test(id=1001, money=99.9)
```

```python
info = {"name":"小李", "age":19}
func(**info) # 等价于 func(name="小李", age=19)
```



##### 匿名函数

lambda 参数列表 : 返回表达式

`lambda`：关键字，代表匿名函数

`参数列表`：多个参数用逗号分隔，无参数直接空着

`:` 后面**只能写 1 条表达式**，表达式结果自动作为返回值，不能写 `if/for/print` 等多行代码

应用：

```python
# 求和
f = lambda a,b : a + b
print(f(2,3)) # 5
```

sort排序

```python
students = [("张三",18),("李四",16),("王五",20)]
# 按元组第二个元素（年龄）升序排序
res = sorted(students, key=lambda x: x[1])
print(res)
# [('李四', 16), ('张三', 18), ('王五', 20)]
```

##### 常用内置函数

![image-20260701113323913](C:\Users\cmy19\AppData\Roaming\Typora\typora-user-images\image-20260701113323913.png)

字符串'a'和浮点数字串'98.7'类型都不能用int()转成整形



![image-20260701114123249](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260701114123249.png)

注意：round函数会进行四舍五入，不加第二个参数默认保留整数

![image-20260701114625930](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260701114625930.png)

对于any()对象中只要有一个元素是True结果为True,全为False结果才为False

reversed()函数返回迭代器对象，要输出时需再转为原来的类型

```python
lst=[1,2,3,4,5]
new_lst=list(reversed(lst))
print(new_lst)

zip/enumerate也是同样
new_zip=list(zip(x,y))
new_enum=list(neumerate(x,start=1))
```

filter示例

![image-20260701120456654](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260701120456654.png)

map示例

![image-20260701120513972](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260701120513972.png)

filter会改变长度起筛选作用，map长度不变



![image-20260701143100311](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260701143100311.png)

format数值型value默认右对齐，字符串型默认左对齐；format_spec格式信息用引号引起来



# 面向对象编程

### 类与对象

![image-20260701154454831](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260701154454831.png)

```python
class Dog:
    # 类属性
    species = "犬类"
    #初始化方法
    def __init__(self, name, color):
        self.name = name#实例属性
        self.__color = color  # 私有

    # 实例方法
    def bark(self):
        print(f"{self.name} 汪汪叫")

    # 获取私有属性
    def get_color(self):
        return self.__color
    #静态方法
    @staticmethod
    def sm():
        print("sm")

    # 类方法
    @classmethod
    def get_species(cls):
        return cls.species
    #静态方法和类方法不能调用实例属性和实例方法

# 使用
d = Dog("旺财", "黄色")
d.bark()
print(d.get_color())
print(Dog.get_species())
```

类属性相当于c++中的静态数据成员，所有对象共有，一般使用类名调用，如果用对象名调用类似动态绑定属性，即给当前对象新建同名实例属性

**对象动态绑定属性和方法**

```python
s1 = Student("小明",18)
# 动态新增score属性，类定义里根本没有写score
s1.score = 98
print(s1.score)  # 98

s2 = Student("小红",19)
# print(s2.score) 报错，s2没有score


def say_hello():
    print("你好")

s1 = Student("小明",18)
# 给s1单独绑定一个方法
s1.hello = say_hello
s1.hello()

# s2没有hello方法，调用会报错
s2 = Student("小红",19)
# s2.hello()
```

还可以给整个类动态绑定属性和方法

### 封装继承和多态

![image-20260701162406604](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260701162406604.png)

**对于私有属性的访问：**

1.可以绕过`__age` 改写成 `_类名__age`用`print(p._Person__age) `强行绕过私有,或者用函数访问（get/set)

2.**使用property装饰器**：

替代手动写 `get_xxx`、`set_xxx`，让私有属性**像普通属性一样读写**，同时保留数据校验、封装逻辑

1. 私有属性：`self.__age`

2. @property 装饰读取方法（get），方法名 = 属性名

3. @属性名.setter 装饰修改方法（set）

```python
class Person:
    def __init__(self, age):
        self.__age = age  # 私有属性

    # 读操作
    @property
    def age(self):
        return self.__age

    # 写操作
    @age.setter
    def age(self, new_age):
        # 数据校验
        if isinstance(new_age, int) and 0 < new_age < 150:
            self.__age = new_age
        else:
            print("年龄输入非法！")
            
 p = Person(18)
# 取值，不用加括号，像普通属性
print(p.age)  # 18

# 修改值，自动触发setter里的校验
p.age = 25
print(p.age)  # 25

p.age = 200  # 年龄输入非法！
```

![image-20260701170013300](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260701170013300.png)

格式：

```python
class 子类名(父类名):
    pass
```

子类定义 `__init__` 时，**不会自动调用父类构造**，必须手动 `super()` 调用父类初始化。

`super()` 代表父类对象。

```python
class Person:
    def __init__(self, name):
        self.name = name
    def show(self):
        print(f"姓名：{self.name}")

# 学生子类，多一个age属性
class Student(Person):
    def __init__(self, name, age):
        # 调用父类构造，给父类属性赋值
        super().__init__(name)
        # 子类独有属性
        self.age = age

    def show(self):
        # 重写父类方法
        super().show()  # 复用父类原有逻辑
        print(f"年龄：{self.age}")

s = Student("小明", 18)
s.show()

多继承如果每个父类都有 __init__（构造函数），只用一次 super() 会只调用第一个父类构造，其余父类属性不会初始化。---用显式调用解决

class Son(Father, Mother):
    def __init__(self, n, a):
        Father.__init__(self, n)
        Mother.__init__(self, a)
```



![image-20260701172704915](C:\Users\cmy19\AppData\Roaming\Typora\typora-user-images\image-20260701172704915.png)

##### 鸭子类型（Python 特有，**不需要继承**）

Python 是动态语言，不检查类型，只检查**对象有没有这个方法**。

只要对象具备同名方法，就能传入同一个函数表现不同行为，效果和多态一模一样。

```python
# 无任何继承关系
class Dog:
    def cry(self):
        print("汪汪")

class Water:
    def cry(self):
        print("哗哗流水")

# 统一函数
def sound(x):
    x.cry()

sound(Dog())
sound(Water())
```

哪怕两个类毫无关联，只要都有 `cry()`，就能实现 “同一个函数，不同行为”。

##### 标准面向对象多态（需要继承）

有统一父类，子类重写方法：

```python
class Animal:
    def cry(self):pass

class Dog(Animal):
    def cry(self):print("汪")
class Cat(Animal):
    def cry(self):print("喵")

def test(obj):
    obj.cry()

test(Dog())
test(Cat())
```



`dir(对象/类)`：列出该对象 / 类**所有可用属性、方法名**，返回字符串列表。

不传入参数：`dir()`，返回当前作用域所有变量名。



### object类

`object` 是 Python 中**所有类的顶层父类**，一切对象的根源。

![image-20260701175159691](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260701175159691.png)

==`__init__` 在创建对象实例时会**自动调用**==

可以重写__str__(),默认print(p)是对象内存地址

```python
class Person:
    def __str__(self):
        return "自定义打印内容"
p = Person()
print(p)
```

`issubclass(A, B)`：判断 A 是不是 B 的子类，所有类都是 object 子类

`isinstance(obj, 类)`：判断对象是否属于该类，所有实例都是 object 的实例

任何对象 `isinstance(xxx, object)` 结果都是 True。



![image-20260701175724185](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260701175724185.png)

`res = a + b  # 等价于 a.__add__(b)`     直接写符号就很方便



![image-20260701180516793](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260701180516793.png)

```python
class Student:
    school = "一中"  # 类属性
    def __init__(self,name):
        self.name = name  # 实例属性

s = Student("小明")
print(s.__dict__)
# 输出：{'name': '小明'}
# 动态新增属性会同步存入__dict__
s.age = 18
print(s.__dict__) # {'name': '小明', 'age': 18}
```

`C.class.__base__`c如果继承了多个父类只会显示第一个，而bases会显示所有



### 类的深拷贝和浅拷贝

![image-20260701182111716](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260701182111716.png)

| 赋值               | 浅拷贝             | 深拷贝               |
| ------------------ | ------------------ | -------------------- |
| a=b                | `a.copy.copy(b)`   | `a.copy.deepcopy(b)` |
| 两对象地址相同     | 两对象内存地址不同 | 两对象内存地址不同   |
| 子对象内存地址相同 | 子对象内存地址相同 | 子对象内存地址不同   |

练习：

![image-20260702090854723](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702090854723.png)

# 模块

![image-20260702090952031](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702090952031.png)

### 导入模块

1. import 模块名（全部导入，使用时加模块名.）

```
import math
print(math.sqrt(16))  # 开平方
print(math.pi)        # 圆周率
```

2. import 模块 as 别名（简化名字）

```
import math as m
print(m.sqrt(25))
```

3. from 模块 import 功能（直接使用，不用加模块名）

```
from math import sqrt, pi
print(sqrt(9))
print(pi)
```

4. from 模块 import * 导入全部（容易重名）

```
from math import *
print(fabs(-5))
```

可以同时导入多个模块，如果有同名变量和函数，后导入的会覆盖之前导入的，此时应使用使用模块名调用

### 包（package）

多个模块放在同一个文件夹，文件夹里加 `__init__.py` 就是**包**，可以分层导入

导入包下面的模块：
1.`import 包名.模块名 as 别名`

`__init__.py`中的内容会自动调用,只执行一次

2.`from 包名 import 模块名 as a`

3.`from 包名.模块名 import 具体功能名称`

4.`from 包名.模块名 import *`

##### 主程序运行

`if __name__ == "__main__"`

模块被其他文件 import 导入`if __name__ == "__main__"`条件内代码**不会执行**

阻止全局变量中的数据被输出执行



### 系统内置模块

![image-20260702093932842](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702093932842.png)

##### random模块

![image-20260702094458753](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702094458753.png)

##### time模块

![image-20260702094642729](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702094642729.png)

![image-20260702094846290](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702094846290.png)

```python
import time
print(time.strftime('%Y-%m-%d %H:%M:%S',time.localtime(time.time())))
```

![image-20260702095833037](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702095833037.png)

```python
from datetime import datetime#导入datetime类
dt = datetime.now()
print("当前系统时间：",dt)
print("格式化输出：", now.strftime("%Y-%m-%d %H:%M:%S"))#转成字符串


# 手动创建2026年10月1日 8点30分
dt = datetime(2026, 10, 1, 8, 30)
print(dt.strftime("%Y-%m-%d %H:%M"))


示例
from datetime import datetime, timedelta
def main():
    # 1. 当前时间
    now = datetime.now()
    print("当前完整时间：", now.strftime("%Y-%m-%d %H:%M:%S"))

    # 2. 字符串转时间
    time_str = "2026-01-01 00:00:00"
    target = datetime.strptime(time_str, "%Y-%m-%d %H:%M:%S")
    print("转换后的时间：", target)

    # 3. 时间运算
    tomorrow = now + timedelta(days=1)
    print("明天：", tomorrow.strftime("%Y-%m-%d"))

    # 4. 时间差
    diff = now - target
    print("距离目标时间天数：", diff.days)

```

### 第三方模块

![image-20260702110223269](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702110223269.png)



##### 使用request进行爬虫

示例：爬取网站天气数据

拿到网址；用正则表达式过滤信息；数据打包转成列表输出

```python
import lst
import requests
import re

headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36"
}

url = 'https://www.weather.com.cn/weather/101010100.shtml'

session = requests.Session()
session.trust_env = False
r = session.get(url, headers=headers)
r.encoding="utf-8"
# print(r.text)

city=re.findall('<span class="name">([\u4e00-\u9fa5]*)</span>',r.text)#结果是一个列表类型

weather=re.findall('<span class="weather">([\u4e00-\u9fa5]*)</span>',r.text)

wd=re.findall('<span class="wd">(.*)</span>',r.text)

#将数据打包

lst=list (zip(city,weather,wd))
for i in lst:
    print(i)

```

示例：爬取图片

找到图片网址；保存本地

```python
import requests
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36"
}

url='https://www.baidu.com/img/PCfb_5bf082d29588c07f842ccde3f97243ea.png'

session = requests.Session()
session.trust_env = False

r = session.get(url, headers=headers)
r.encoding="utf-8"
#保存到本地
with open("baidu.png", "wb") as file:
    file.write(r.content)
```

保存到本地之后在你的python项目里就会出现下载的图片

![image-20260702111542944](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702111542944.png)



# 文件操作

### 文件的写入操作

![image-20260702112113212](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702112113212.png)

![image-20260702112206771](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702112206771.png)

##### 文件基本操作

| 读写方法               | 描述说明                                                     |
| ---------------------- | ------------------------------------------------------------ |
| `file.read(size)`      | 从文件中读取 size 个字符，如果没有给定参数，则读取文件中的全部内容 |
| `file.readline(size)`  | 读取文件中的一行数据，如果给定参数，则为读取这一行中的 size 个字符 |
| `file.readlines()`     | 从文件中读取所有内容，结果为列表类型，一行数据是列表的一个元素 |
| `file.write(s)`        | 将字符串 s 写入文件                                          |
| `file.writelines(lst)` | 将内容全部为字符串的列表 lst 写入文件                        |
| `file.seek(offset)`    | 改变当前文件操作指针的位置，英文占一个字节，中文 gbk 编码占两个字节，utf-8 编码占三个字节，offset为对应的字节数 |



文件的写入：

![image-20260702113235156](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702113235156.png)

 `if __name__ == '__main__':`

 这是**程序入口判断**，用来区分两种运行场景：

1.  直接运行当前这个 py 文件
   
   内置变量 `__name__` 自动等于字符串 `'__main__'`，冒号下方缩进的代码会执行；

2. 把这个文件当成模块，被别的文件 import 导入

    等于当前文件名，条件不成立，下面两行写入文件的代码

   不会自动执行


作用：把测试代码隔离，只在单独运行本文件时才执行写入操作，导入当工具时不会乱生成文件。

**完整执行流程梳理**

1. 程序运行，先加载定义 `def my_write(s):` 这个写入函数；
2. 走到 `if __name__ == '__main__':` 判断，因为是直接运行本文件，条件成立；
3. 第一句调用函数，写入第一行文字并换行；
4. 第二句调用函数，写入第二行文字并换行；
5. 函数内部每次执行都会打开、写入、关闭 `b.txt`，模式是 `'a'` 追加，多次运行不会覆盖原有内容，只会持续往下新增。



文件的读取：

```python
def my_read(filename):
    # (1) 打开文件 w+：可读可写，不存在则创建，存在则清空原有内容
    file = open(filename, 'w+', encoding='utf-8')

    # (2) 操作：写入内容，写完后文件指针停在文件末尾
    file.write('你好啊')

    # seek(0) 将文件指针移动到文件开头，否则read读不到内容
    file.seek(0)

    # 读取全部文本，赋值给变量s
    s = file.read()
    print(type(s), s)

    # (3) 关闭文件
    file.close()


if __name__ == '__main__':
    my_read('d.txt')
```



文件的复制：（复制图片）

图片、视频、压缩包这类非文本文件必须用二进制读写

```python
def copy(src, new_path):
    # (1) 二进制只读打开源图片文件 rb
    file1 = open(src, 'rb')
    # (2) 二进制只写创建目标文件 wb
    file2 = open(new_path, 'wb')

    # (3) 开始复制，边读边写
    s = file1.read()  # 源文件读取全部二进制数据
    file2.write(s)    # 向目标文件写入全部二进制数据

    # (4) 关闭文件：后打开的先关闭，先打开的后关闭
    file2.close()
    file1.close()


if __name__ == '__main__':
    # . 代表当前代码文件所在目录
    src = './google.jpg'
    # .. 代表上级文件夹（退回上一级目录）
    new_path = '../chap10/copy_google.jpg'
    # 调用复制函数
    copy(src, new_path)
    print('文件复制完毕')
```



### with语句

![image-20260702120117846](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702120117846.png)

```python
# 写入文件函数
def write_fun():
    with open('aa.txt', 'w', encoding='utf-8') as file:
        file.write('2022北京冬奥会欢迎你')

# 读取文件函数
def read_fun():
    with open('aa.txt', 'r', encoding='utf-8') as file:
        print(file.read())

# 文件复制函数（文本文件）
def copy(src_file, target_file):
    # 同时打开源文件和目标文件
    with open(src_file, 'r', encoding='utf-8') as f_read, open(target_file, 'w', encoding='utf-8') as f_write:
        content = f_read.read()
        f_write.write(content)


# 程序入口
if __name__ == '__main__':
    # 执行写入
    write_fun()
    # 执行读取
    read_fun()
    # 执行复制，把aa.txt复制到bb.txt
    copy("aa.txt", "bb.txt")
    print("文件复制完成")
```

### 数据的组织维度及存储

![image-20260702143642374](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702143642374.png)

##### 一维数据读写：

写入：一维列表 → 用 `','.join(列表)` 拼接成**一行逗号分隔字符串**，存入 txt

读取：读取 txt 整行字符串 → 用 `split(',')` 按逗号切割，还原一维列表

```python
# 一维列表（一维数据）
data = ["张三", "李四", "王五", "赵六"]

# 写入
with open("one_dim.txt", "w", encoding="utf-8") as f:
    # join：列表元素用逗号连接成字符串
    line = ",".join(data)
    f.write(line)
    
    
with open("one_dim.txt", "r", encoding="utf-8") as f:
    content = f.read()
    # split(",")：以逗号切割字符串，变回一维列表
    data = content.split(",")
print(data)
# 输出：['张三', '李四', '王五', '赵六']
```

##### 二维数据读写：

`.csv` 是专门存储表格的文本文件，Python 内置 `csv` 模块专门处理，不用手动拼接分割

```python
import csv

# 二维列表（表格：3行2列）
two_data = [
    ["姓名", "分数"],  # 表头
    ["张三", 88],
    ["李四", 95],
    ["王五", 79]
]

# 写入csv
with open("two_dim.csv", "w", encoding="utf-8", newline="") as f:
    # 创建写入对象
    writer = csv.writer(f)
    # 一次性写入所有行（二维列表）
    writer.writerows(two_data)
    

two_list = []
with open("two_dim.csv", "r", encoding="utf-8") as f:
    reader = csv.reader(f)
    # 循环每一行，每一行都是一维列表
    for row in reader:
        two_list.append(row)

print(two_list)
# 输出二维嵌套列表：
# [['姓名', '分数'], ['张三', '88'], ['李四', '95'], ['王五', '79']]
```



##### 高维数据读写

![image-20260702150746253](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702150746253.png)

示例：dumps Python → JSON 字符串； loads JSON 字符串 → Python 数据

```python
import json
# Python字典（Python原生数据）
stu = {"name":"小明", "age":18, "hobby":["打球","看书"]}
# 编码：转JSON字符串
json_str = json.dumps(stu, ensure_ascii=False, indent=2)
print(type(json_str), json_str)

# 把JSON字符串还原成字典
python_data = json.loads(json_str)
print(type(python_data), python_data["name"])
```

ensure_ascii正常显示中文保证不乱码；indent=2缩进两字符

示例：dump 写入 json 文件； load 读取 json 文件

```python
import json
stu = {"name":"小明", "age":18}
# w模式打开json文件
with open("stu.json", "w", encoding="utf-8") as f:
    # 直接写入文件，无需手动转字符串
    json.dump(stu, f, ensure_ascii=False, indent=2)
    
with open("stu.json", "r", encoding="utf-8") as f:
    # 直接读取文件内容，返回Python字典
    data = json.load(f)
print(date)
```

### 目录与文件的相关操作

首先导入`import os`

![image-20260702152300379](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702152300379.png)

![image-20260702152334126](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702152334126.png)

os.path模块

![image-20260702155051376](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702155051376.png)

![image-20260702155159820](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702155159820.png)

示例

```python
import os

# 1. 获取当前路径
current = os.getcwd()
print("当前目录：", current)

# 2. 拼接文件路径
txt_path = os.path.join(current, "demo.txt")

# 3. 判断文件是否存在
if not os.path.exists(txt_path):
    print("文件不存在")
else:
    print("文件存在")

# 4. 创建文件夹
if not os.path.exists("new_folder"):
    os.mkdir("new_folder")
    print("文件夹创建完成")

# 5. 遍历目录所有内容
all_file = os.listdir(".")
print("目录下所有文件：", all_file)
```

![image-20260702161444872](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702161444872.png)

writelines直接拼接列表字符串，**不会自动加换行**

文件关闭后不会自动打开

文本以文本方式打开时，读写按照字符的方式

对文件操作完成后不关闭文件不会报错，但是有数据丢失，资源占用的风险



# 程序与进程

##### 程序

本质：**存放在硬盘上的静态代码文件**（`.exe`/`.py`/ 二进制文件），一堆指令集合，静止不动

##### 进程

本质：**程序运行起来后，加载到内存中的动态实体**，操作系统分配资源的最小单位



### 创建进程的方式1：

![image-20260702165539042](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702165539042.png)

`os.getpid()`：自己进程 ID

`os.getppid()`：**父进程 ID**

`p.start()`：创建并**启动进程**，调用 target 函数

`p.join()`：**主线程阻塞**，等待子进程运行结束再继续往下走

```python
from multiprocessing import Process#导入process类
import os
import time

# 子进程要执行的任务
def work(num):
    print(f"子进程PID：{os.getpid()}，传入数字：{num}")
    time.sleep(2)  # 模拟任务耗时2秒
    print("子进程任务执行完毕")

if __name__ == '__main__':
    print(f"主进程PID：{os.getpid()}")

    # 1. 创建进程对象，此时只是定义，进程未创建、未运行
    p = Process(target=work, args=(10,))
    print("1. 进程对象创建完成，还未启动")

    # 2. p.start()：真正创建子进程、操作系统分配资源，执行target函数
    p.start()
    print("2. 子进程已启动，主线程继续往下执行（无join会不等子进程）")

    # 3. p.join()：主线程阻塞，停在这里等待子进程全部执行完，才会执行后续代码
    p.join()
    print("3. 子进程运行结束，主线程解除阻塞，程序收尾")
```

注意args=(10,)这里是给元组传参，`,`不能省

### process类常用方法/属性

![image-20260702172217708](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702172217708.png)



`pid` 只有调用`start()`之后才有数值，启动前为`None`；

`start()`只能调用一次，重复调用会抛异常；

`join(timeout)`超时不会杀死进程，只是主线程不再等待，子进程仍后台运行；

`terminate()`是暴力结束，生产环境尽量少用，优先正常执行完退出；

`run()`是内部回调方法，不要手动调用，由`start()`自动触发。

没有给定target参数，会调用Process类中的run()方法，run()可自定义修改（涉及创建进程方式2）

### 创建进程方式2：

![image-20260702174723913](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260702174723913.png)

```python
from multiprocessing import Process
import os, time

# 自定义进程类，继承Process父类
class SubProcess(Process):
    # 重写构造方法，接收自定义name参数
    def __init__(self, name):
        # 调用父类Process的初始化方法，传入进程名称
        super().__init__(name=name)
        # self.name = name  # 父类__init__已经处理name，这行可省略

    # 重写父类核心run方法：进程start()后自动执行run内代码
    def run(self):
        print(f'子进程的名称{self.name}，PID：{os.getpid()}, 父进程的PID：{os.getppid()}')
        time.sleep(1)

if __name__ == '__main__':
    print(f"主进程PID：{os.getpid()}")
    # 实例化自定义进程类，传入进程名
    p = SubProcess(name="自定义进程1")
    # 这里没有给target传参，启动子进程，自动触发run()方法
    p.start()
    # 主线程等待子进程执行完毕再退出
    p.join()
    print("子进程执行结束，主程序收尾")
```

**两种创建进程方式区分**

- 函数式：`Process(target=函数)`，适合简单短任务
- 继承类式：继承`Process`、重写`run()`，适合复杂、多逻辑任务



### pool进程池

可以自动开始子进程

先导入Pool类`from multiprocessing import Pool`

创建进程池

| 方法                                | 作用                                            |
| ----------------------------------- | ----------------------------------------------- |
| `Pool(n)`                           | 创建进程池，n 为最大并发进程数；默认 CPU 核心数 |
| `apply(func, args)`                 | 同步执行，阻塞，一次提交一个任务                |
| `apply_async(func, args, callback)` | 异步提交，不阻塞，返回结果对象                  |
| `map(func, iterable)`               | 同步批量处理，自动分片，阻塞等全部完成          |
| `map_async(func, iterable)`         | 异步批量，返回结果对象                          |
| `imap(func, iterable)`              | 迭代式返回，边算边取结果，省内存                |
| `close()`                           | 关闭池子，不再接收新任务                        |
| `join()`                            | 阻塞等待所有进程执行完毕（必须先 close）        |
| `terminate()`                       | 强制杀死所有进程，不等待收尾                    |

```python
from multiprocessing import Pool
import os,time

def task(name):
    print(f'子进程{os.getpid()},{name}')
    time.sleep(1)

if __name__ == '__main__':
    start=time.time()
    print("父进程执行")
    p=Pool(3)
    for i in range(10):
        #非阻塞方式
        p.apply_async(target=task,args=(i,))
        p.close()
        p.join()
        print("所有子进程结束，父进程结束")
        print(time.time()-start)


```

### 并发和并行

> **并发（Concurrency）**：**同一时间段**，多个任务交替切换执行，宏观看起来同时跑，**不一定多核**，单核 CPU 也能实现。

> **并行（Parallelism）**：**同一时刻**，多个任务真正同时运行，**必须多核 CPU**，每个核心各干一个任务。



进程之间数据不共享----引入队列



### 进程之间的通讯



![image-20260703090004954](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260703090004954.png)

先导Queue类`from multiprocessing import Queue`

创建队列`q=Queue(n)`不写n说明可接收消息数无上限

![image-20260703090047563](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260703090047563.png)

1. `put(item, block=True, timeout=None)`

- 作用：把`item`（任意可序列化对象）存入队列尾部

- ```
  block=True（默认阻塞）：队列已满时，进程卡住等待空位；设置
  ```

  ```
  timeout=3   #等待 3 秒无空位抛full异常
  ```

- `block=False`（非阻塞）：队列满直接抛`Full`异常

2. `put_nowait(item)`不等待，队列满立刻报错。

   

```python
from multiprocessing import Queue,Process
import time
a=100
def write(q):
    global a
    if not q.full():
        for i in range(6):
            a-=10
            q.put(a)
            print("a入队时：",a)

def read(q):
    time.sleep(1)
    while not q.empty():
        print("a出队时：",q.get())
if __name__ == '__main__':
    print("父进程开始")
    q=Queue()
    p1=Process(target=write,args=(q,))
    p2=Process(target=read,args=(q,))
    p1.start()
    p2.start()
    p1.join()
    p2.join()
    print("父进程结束")
    
父进程开始
a入队时： 90
a入队时： 80
a入队时： 70
a入队时： 60
a入队时： 50
a入队时： 40
a出队时： 90
a出队时： 80
a出队时： 70
a出队时： 60
a出队时： 50
a出队时： 40
父进程结束

```

写和出用的都是一个队列，这个队列是共享的



### 线程

![image-20260703093140000](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260703093140000.png)



##### 函数式创建线程

![image-20260703093447089](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260703093447089.png)

```python
from threading import Thread
import time

def work(num):
    print(f"任务{num}开始")
    time.sleep(1)
    print(f"任务{num}结束")

if __name__ == '__main__':
    thread_list = []
    # 创建5个线程
    for i in range(5):
        t = Thread(target=work, args=(i,))
        thread_list.append(t)
        t.start()
    
    # 统一等待所有线程
    for t in thread_list:
        t.join()
    print("所有子线程执行完毕")
```

其中包括一个主线程负责执行main中的代码，5个自定义创建的线程

每个线程并行执行不同的任务，多线程之间并发执行

##### 继承式创建进程

与创建进程类似，自定义继承threading模块下的Thread类，重写run()方法

```python
from threading import Thread
import time

class TaskThread(Thread):
    def __init__(self, num):
        super().__init__()
        self.num = num

    def run(self):
        print(f"任务{self.num}开始")
        time.sleep(1)
        print(f"任务{self.num}结束")

if __name__ == '__main__':
    thread_list = [TaskThread(i) for i in range(3)]
    for t in thread_list:
        t.start()
    
    # 统一等待所有线程
    for t in thread_list:
        t.join()
    print("全部任务执行结束")
```

多线程并发执行

**线程之间的数据可以共享**

> **进程**：操作系统资源分配的最小单位，**独立内存、独立资源**，进程之间完全隔离。

> **线程**：进程内调度执行的最小单位，**共享所属进程的内存、资源**，线程切换开销极小。

多个线程同时读写全局变量，会出现数据覆盖、结果错误（竞态条件）；锁保证**临界区代码串行执行**

![image-20260703102128399](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260703102128399.png)

1. **Lock 两大操作**

- `lock.acquire()`：加锁，其他线程阻塞等待
- `lock.release()`：释放锁，其他线程才能进入临界区

```python
from threading import Thread, Lock
import time

num = 0
lock = Lock()

class MyThread(Thread):
    def __init__(self):
        super().__init__()
    def run(self):
        global num
        # 上锁with lock 自动加锁、自动释放，不用手动写 release
        with lock:
            temp = num
            time.sleep(0.01)
            num = temp + 1

if __name__ == '__main__':
    thread_list = [MyThread() for _ in range(100)]
    for t in thread_list:
        t.start()
    for t in thread_list:
        t.join()
    print(num)
```

### 消费者与生产者问题

![image-20260703110910987](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260703110910987.png)

共享一个队列，便于数据写入和取出

```python
from queue import Queue
from threading import Thread
import time

#创建生产类
class Produce(Thread):
    def __init__(self,name,queue):
        Thread.__init__(self,name=name)
        self.queue=queue
    def run(self):
        for i in range(1,6):
            print(f"{self.name}将产品{i}放入队列")
            self.queue.put(i)
            time.sleep(1)
        print("存放")
#创建消费者
class Consume(Thread):
    def __init__(self,name,queue):
        Thread.__init__(self,name=name)
        self.queue=queue
    def run(self):
        for _ in range(5):
            value=self.queue.get()
            print(f"{self.name}取出{value}")
        print("取出")
if __name__ == '__main__':
    queue=Queue()
    p=Produce('Produce',queue)
    c=Consume('Consume',queue)
    p.start()
    c.start()
    p.join()
    c.join()
    print("主线程结束")
    
Produce将产品1放入队列
Consume取出1
Produce将产品2放入队列
Consume取出2
Produce将产品3放入队列
Consume取出3
Produce将产品4放入队列
Consume取出4
Produce将产品5放入队列
Consume取出5
取出
存放
主线程结束

```

