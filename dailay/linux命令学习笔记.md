个人认为linux操作并不是特别擅长，所以重新系统的学习了linux命令

man 目标命令

ls命令：
ls -F   可区分是文件还是目录
ls -a 	把隐藏文件普通文件和目录都显示出来
ls -F -R 递归输出文件和目录列表
ls -d 	只输出目录的信息
ls -i	查看文件或目录的inode编号
ls -l 	输出长列表格式的输出，包含目录中每个文件的更多相关信息
ls -l my_scrept	过滤输出，会将名称为my_scrept的文件或目录输出
？代表1个字符
*代表多个字符
ls -l my_scr?pt
ls -l my*
ls -l my_s*t
ls -l my_scr[ai]pt  将my_scrapt和my_script的文件输出
ls -l f[a-i]ll  包含a-i的字符
ls -l f[!a]ll 	不包含a的字符



touch test_one 创建一个空文件

再次使用touch test_one会修改test_one文件的创建时间

touch -a test_one 会改变test_one文件的最后访问时间



cp命令
cp source destination


使用cp命名如果目标文件已经存在那么并不会提醒
cp -i test_one test_one 会提示是否覆盖
cp -R 会递归的赋值整个目录的内容
cp *script /home	将所有以script结尾的文件复制



链接文件
符号链接
$ ls -l data_file
-rw-rw-r-- 1 christine christine 1092 May 21 17:27 data_file
$
$ ln -s data_file sl_data_file
$
$ ls -l *data_file
-rw-rw-r-- 1 christine christine 1092 May 21 17:27 data_file
lrwxrwxrwx 1 christine christine 9 May 21 17:29 sl_data_file -> data_file

硬链接:
硬链接会创建独立的虚拟文件，其中包含了原始文件的信息及位置。但是它们从根本上而言
是同一个文件。引用硬链接文件等同于引用了源文件。要创建硬链接，原始文件也必须事先存在，
只不过这次使用 ln 命令时不再需要加入额外的参数了。

$ ls -l code_file
-rw-rw-r-- 1 christine christine 189 May 21 17:56 code_file
$
$ ln code_file hl_code_file
$
$ ls -li *code_file
296892 -rw-rw-r-- 2 christine christine 189 May 21 17:56
code_file
296892 -rw-rw-r-- 2 christine christine 189 May 21 17:56
hl_code_file


移动或重命名文件：
mv source destination
$ mv fall fzll	重命名文件

$ mv fzll Pictures/	移动文件

$ mv Mod_Scripts Old_Scripts	将整个文件夹移动
mv -i		覆盖时会有提示

删除文件
rm -i source 删除会有提示
rm -i f?ll
rm -i f*l         
rm -f 忽略不存在的文件，不给出提示
rm -rf 删除文件(文件夹)，递归删除子目录

创建目录：mkdir
mkdir -p new_dir/sub_dir/under_dir

查看文件类型
file my_file
my_file: ASCII text


查看整个文件
cat test1
hello

This is a test file.


That we'll use to 	test the cat command.

cat -n test1	会给文件加上行号，空行也会加上

1 hello
2
3 This is a test file.
4
5
6 That we'll use to test the cat command.
cat -b test1	给文件加上行号，空行不会加上
1 hello

2 This is a test file.


3 That we'll use to test the cat command.

cat -T test1	不让制表符出现

more命令：more命令会显示文本文件的内容，但会在显示每页数据之后停下来

less命令：不仅和more命令一样可以一次显示一屏的文件文本，还可以识别上下键一下上下翻页键

tail命令：tail命令会显示文件最后几行的内容，默认10行
tail -n 20 log_file 	可以显示20行
tail -f 动态查看尾部
head命令
head -5 log_file显示文件的前5行

ps命令
Unix风格   各个命令可以组合起来
-A	显示所有进程
-N	显示与指定参数不符的所有进程
-a	显示除控制进程（session leader ① ）和无终端进程外的所有进程
-d	显示除控制进程外的所有进程
-e	显示所有进程
-C cmdlist	显示包含在 cmdlist 列表中的进程
-G grplist	显示组ID在 grplist 列表中的进程
-U userlist	显示属主的用户ID在 userlist 列表中的进程
-g grplist	显示会话或组ID在 grplist 列表中的进程 ②
-p pidlist	显示PID在 pidlist 列表中的进程
-s sesslist	显示会话ID在 sesslist 列表中的进程
-t ttylist	显示终端ID在 ttylist 列表中的进程
-u userlist	显示有效用户ID在 userlist 列表中的进程
-F	显示更多额外输出（相对 -f 参数而言）
-O format	显示默认的输出列以及 format 列表指定的特定列
-M	显示进程的安全信息
-c	显示进程的额外调度器信息
-f	显示完整格式的输出
-j	显示任务信息
-l	显示长列表
-o format	仅显示由 format 指定的列
-y	不要显示进程标记（process flag，表明进程状态的标记）
-Z	显示安全标签（security context） ① 信息
-H	用层级格式来显示进程（树状，用来显示父进程）
-n namelist	定义了 WCHAN 列显示的值
-w	采用宽输出模式，不限宽度显示
-L	显示进程中的线程
-V	显示 ps 命令的版本号


top命令，实时显示系统进程的情况


结束进程
linux 进程信号
信号		名称		描述
1  		HUP		挂起
2  		INT		中断
3  		QUIT		结束运行
9  		KILL		无条件终止
11 		SEGV		段错误
15  		TERM		尽可能终止
17  		STOP		无条件停止运行，但不终止
18 		TSTP		停止或暂停，但继续在后台运行
19  		CONT		在 STOP 或 TSTP 之后恢复执行

kill PID
killall http*

挂载存储媒体
mount命令会输出当前系统上挂载的设备列表

手动挂载媒体设备：
mount -t type device directory

type参数指定了磁盘被格式化的文件系统类型
vfat：windows长文件系统
ntfs：windows NT XP Vista以及Windows7中广泛使用的高级文件系统
iso9660：标准CD-ROM文件系统

比如说，手动将U盘/dev/sdb1挂载到/media/disk，可用下面的命令：
mount -t vfat /dev/sdb1 /media/disk


umount命令卸载可移动shebei
umount [directory | device]
如果有任何程序正在使用设备上的文件，系统就不会允许你卸载它


df命令
df命令可以很方便的查看所有已挂载磁盘的使用情况

$ df
Filesystem 1K-blocks Used Available Use% Mounted on
/dev/sda2 18251068 7703964 9605024 45% /
/dev/sda1 101086 18680 77187 20% /boot
tmpfs 119536 0 119536 0% /dev/shm
/dev/sdb1 127462 113892 13570 90% /media/disk
$


df -h 用M代替兆字节 G代替吉字节

du -c 显示所有一列出的文件总的大小







