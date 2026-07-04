# Linux shell基本指令

shell：系统的用户界面，提供了用户与内核进行交互的界面

## 命令 -选项 参数
（目录即文件名）
* /代表根目录         ~代表home目录
* 文件夹没有后缀，文件有后缀
* 切换root用户# su - root
* #mkdir创建文件夹
#touch创建文件
## 列出当前工作目录下的内容
ls
(ls -a列出包括隐藏文件的所有文件名）
ls -l       #显示详细信息，包括权限·大小·修改时间（竖向列表）
选项可混合使用（ls -al,ls -la,ls -a -l)
ls -lh       #以更人性化的方式是展示包含单位
## 创建文件夹
mkdir 文件名
mkdir -p文件名/下设文件名{可一次性创建多层}
eg. mkdir -p ~/test/test1{创建home目录下的test文件下的test1文件}
## 切换工作目录change directory
cd          #在home目录
cd 文件名（相对路径以当前目录为起点不需要以/为起点）
cd ~/文件名（绝对路径以/为起点）
## 展示文件路径/输出当前工作目录
pwd
## 特殊路径符
cd .(当前文件)
cd ..(上一文件)cd../..(跳两级)
cd ~(返回主目录)
## 删除文件
rm 文件             #删除文件
rm -r 文件名 ... ...          # 递归删除文件夹，及子目录也一并删除
~~rm -f 文件        # 强制删除~~
rm --h                       #查找rm下所有用法
通配符的运用*
## 创建文件，包括源代码（c++为.cpp python为.py)
touch 文件名（.---) eg. touch ~/test.txt

## 确定文件类型

file <文件名>

![image-20260703151428471](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260703151428471.png)

![image-20260703151520045](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260703151520045.png)

## 查看文件内容

cat 文件名（称为Linux路径）

cat -n 路径   列出行号（包括空白行）

more Linux路径（可翻页，空格翻页，q退出）

less 路径

![image-20260703155509916](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260703155509916.png)

## 复制文件
cp ./file1 ./file2           #文件1复制到2
cp -r ./directory1 ./directory2           #递归复制/复制文件夹+-r

保留原文件权限时间：`cp -a test.txt /tmp/`

![image-20260703152106861](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260703152106861.png)

## 重命名或移动文件到其他目录
mv old文件名 new文件名
mv 源文件 目标文件（/）（若路径不同 移动+命名）
若移动到的文件不存在就相当于改名
## 查找程序文件在哪
which Linux命令
## 搜索文件
find 起始路径 -name "文件名"   通配符运用（* .txt)
find 起始路径 -size +X（大于x大小+单位（K M G）
find 起始路径 -size -x (小于下大小)
ctrl C结束全盘搜索

## 通过关键字过滤文件行
grep ＂关键字＂ 文件名
grep -n  ＂关键字＂ 文件名(文件行前面显示行数n)

![image-20260703160022251](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260703160022251.png)

## 统计文件行数，单词数，字符数，字节数
wc -l 文件名
wc -w 文件名
wc -m 文件名
wc -c 文件名

## 对文件进行排序

sort file



## 管道符

| (将|前的内容传给后面)

## 编辑文件vim
vim 文件名
通过键盘上的上下左 右移动光标或kjhl
命令模式下进入输入模式i/a/o（光标前/光标后/光标下一行）
返回命令模式esc键
底线命令模式：：wq保存并退出
详情见手机图片

## 命令行内输出指定内容
echo "输出内容"
## `
\`飘号包围内容作为命令执行，而非普通字符
## 重定向符
\>     将左侧命令结果覆盖写入右侧指定文件
\>>   将左侧命令结果追加写入右侧指定文件
## 查看文件尾部内容
tail -n Linux路径  （查看尾部n行）
tail -f -n Linux路径  （持续跟踪）

## 切换同户名
su - root（用户名）
exit退出
-加载环境变量
sudo 命令(是普通命令带有root权限)

## 用户和用户组
groupadd
groupdel
useradd -g 用户组/-d /home/路径（指定用户Home路径)
userdel(删除用户名，home目录保留)
userdel -r(删除用户home目录)
usermod -aG 组 用户名（将该用户加到该组）
id 查看用户信息
getent passwd 查看用户
getent group 查看用户组
## 编辑文本
gedit 文件名
## 软件相关命令
apt install
...用apt --help查找更多
dpkg            #包管理工具

## 杀死进程
kill id号
## 查看进程
ps -A
## 将文件变为特定模式
chmod -x 文件名 或  chmod -777  文件名         #变file为可执行文件

u 所有者 g 用户组 o 其他用户

r读权限（5） w写权限（2） x 执行权限（1）

ctrl+L清屏

![image-20260703145154924](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260703145154924.png)

![](https://raw.githubusercontent.com/ccc666yyyy/tuchuang/main/image-20260703145209091.png)