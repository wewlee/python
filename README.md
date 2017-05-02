# python
python自学笔记
1.用户及文件基本操作

1.1用户
su <user>    切换到用户user，需输入密码
su - <user>  切换用户，同时环境变量也变为目标用户的环境变量（su -l dcc）
adduser <user>  添加用户
groups <user> 查看user用户的用户组
deluser <user> 删除用户（sudo deluser lilei --remove-home）

1.2文件权限
ls　　        显示文件或目录
     -l        列出文件详细信息l(list)
     -a        列出当前目录下所有文件及目录，包括隐藏的a(all)
chown         变更文件所有者（sudo chown <user> filename）
chmod         修改文件权限（chmod 700 filename）

2.目录结构及文件基本操作
2.1目录结构
tree           树形结构显示目录（tree /）
cd             切换目录
    ..          进入上一级目录
    ~           进入home目录
pwd            获取当前路径
绝对路径：以根"/"目录为起点的完整路径，以你所要到的目录为终点，如： /usr/local/bin相对路径相对路径：以当前目录 . 为起点，以你所要到的目录为终点，如： usr/local/bin 假设你当前目录为根目录

2.2文件的基本操作
touch          创建空白文件（touch {1..5}.txt批量新建文件）
mkdir          新建目录
       -p       同时创建父目录（mkdir -p father/son）
echo           创建带有内容的文件
cp             拷贝文件或者目录
    -r          递归复制
rm             删除文件
     -r         递归删除，可删除子目录及文件
     -f         强制删除
mv             移动文件，剪切文件,或者重命名
rename         批量重命名
                 # 批量将这 5 个后缀为 .txt 的文本文件重命名为以 .c 为后缀的文件
                 $ rename 's/\.txt/\.c/' *.txt
                 # 批量将这 5 个文件，文件名改为大写
                 $ rename 'y/a-z/A-Z/' *.c
cat             正序显示
     -n            显示行号
tac             倒序显示
nl              添加行号并打印
more、less      分页显示文本文件内容
head、tail      显示文件头、尾内容
ln              创建链接文件
file            查看文件类型（file /bin/ls）

3.环境变量与文件查找
3.1环境变量
declare         创建变量
echo $temp      读取变量的值（$符号用于表示引用一个变量的值）
注：要添加一个永久生效的环境变量，只需要打开/etc/profile，在最后加上你想添加的环境变量
echo $PATH       查看path环境变量
gedit            使用文本编辑器新建文件（gedit hello.sh）
gcc              生成可执行文件（gcc -o hello.sh）
PATH=$PATH:绝对路径    添加自定义路径到“PATH”环境变量
echo "PATH=$PATH:/home/shiyanlou/mybin" >> .zshrc         修改用户目录下的配置文件，添加内容到.zshrc中，>>表示将标准输出以追加的方式重定向到一个文件中，注意前面用到的>是以覆盖的方式重定向到一个文件中
变量设置方式	                说明
${变量名#匹配字串}	        从头向后开始匹配，删除符合匹配字串的最短数据
${变量名##匹配字串}	        从头向后开始匹配，删除符合匹配字串的最长数据
${变量名%匹配字串}	        从尾向前开始匹配，删除符合匹配字串的最短数据
${变量名%%匹配字串}	        从尾向前开始匹配，删除符合匹配字串的最长数据
${变量名/旧的字串/新的字串}	将符合旧字串的第一个字串替换为新的字串
${变量名//旧的字串/新的字串}	将符合旧字串的全部字串替换为新的字串
unset             删除变量
source .zshrc     环境变量立即生效
. ./.zshrc        同上

3.2搜索文件
whereis          只能搜索二进制文件（-b,-m.-s）
locate           查找指定目录下的文件（-c统计数目，-i忽略大小写）
             locate /etc/sh             查找 /etc 下所有以 sh 开头的文件
             locate /usr/share/\*.jpg   查找 /usr/share/ 下所有 jpg 文件
which            确定是否安装了某个指定的软件，因为它只从PATH环境变量指定的路径中去搜索命令
find              在文件系统中搜索某文件 
find / -name file1 从 '/' 开始进入根文件系统搜索文件和目录
find / -user user1 搜索属于用户 'user1' 的文件和目录
find /home/user1 -name \*.bin 在目录 '/ home/user1' 中搜索带有'.bin' 结尾的文件
find /usr/bin -type f -atime +100 搜索在过去100天内未被使用过的执行文件
find /usr/bin -type f -mtime -10 搜索在10天内被创建或者修改过的文件
find / -name \*.rpm -exec chmod 755 '{}' \; 搜索以 '.rpm' 结尾的文件并定义其权限
find / -xdev -name \*.rpm 搜索以 '.rpm' 结尾的文件，忽略光驱、捷盘等可移动设备  


4.文件打包与压缩
4.1主要压缩格式
文件后缀名        说明
*.zip zip         程序打包压缩的文件 
*.rar rar         程序压缩的文件 
*.7z 7zip         程序压缩的文件 
*.tar tar         程序打包，未压缩的文件 
*.gz gzip         程序(GNU zip)压缩的文件 
*.xz xz           程序压缩的文件 
*.bz2 bzip2       程序压缩的文件 
*.tar.gz tar      打包，gzip程序压缩的文件 
*.tar.xz tar      打包，xz程序压缩的文件 
*tar.bz2 tar      打包，bzip2程序压缩的文件 
*.tar.7z tar      打包，7z程序压缩的文件 

4.2  ZIP
zip   打包压缩
$zip -r -q -o shiyanlou.zip /home/shiyanlou
     -r    参数表示递归打包包含子目录的全部内容
     -q    参数表示为安静模式，即不向屏幕输出信息
     -o    表示输出文件，需在其后紧跟打包输出文件名
#设置压缩级别为9和1（9最大,1最小），重新打包：
$ zip -r -9 -q -o shiyanlou_9.zip /home/shiyanlou -x ~/*.zip
$ zip -r -1 -q -o shiyanlou_1.zip /home/shiyanlou -x ~/*.zip
#创建加密zip包
使用-e参数可以创建加密压缩包：
$ zip -r -e -o shiyanlou_encryption.zip /home/shiyanlou
注意: 关于zip命令，因为 Windows 系统与 Linux/Unix 在文本文件格式上的一些兼容问题，比如换行符（为不可见字符），在 Windows 为 CR+LF（Carriage-Return+Line-Feed：回车加换行），而在 Linux/Unix 上为 LF（换行），所以如果在不加处理的情况下，在 Linux 上编辑的文本，在 Windows 系统上打开可能看起来是没有换行的。如果你想让你在 Linux 创建的 zip 压缩文件在 Windows 上解压后没有任何问题，那么你还需要对命令做一些修改：
$ zip -r -l -o shiyanlou.zip /home/shiyanlou
需要加上-l参数将LF转换为CR+LF来达到以上目的。
unzip      解压缩
#将shiyanlou.zip解压到当前目录：
$ unzip shiyanlou.zip
#使用安静模式，将文件解压到指定目录：
$ unzip -q shiyanlou.zip -d ziptest
#上述指定目录不存在，将会自动创建。如果你不想解压只想查看压缩包的内容你可以使用-l参数：
$ unzip -l shiyanlou.zip

4.3  RAR
rar      打包压缩
?从指定文件或目录创建压缩包或添加文件到压缩包：
$ rar a shiyanlou.rar .
上面的命令使用a参数添加一个目录～到一个归档文件中，如果该文件不存在就会自动创建。
注意：rar 的命令参数没有-，如果加上会报错。
?从指定压缩包文件中删除某个文件：
$ rar d shiyanlou.rar .zshrc
?查看不解压文件：
$ rar l shiyanlou.rar
unrar                  解压 
例：
?使用unrar解压rar文件
#全路径解压：
$ unrar x shiyanlou.rar
#去掉路径解压：
$ mkdir tmp
$ unrar e shiyanlou.rar tmp/

4.4   TAR
tar      打包工具(tar -cf shiyanlou.tar ~)
    -c    表示创建一个 tar 包文件， 
    -f    用于指定创建的文件名，注意文件名必须紧跟在-f参数之后，比如不能写成tar -fc shiyanlou.tar，可以写成tar -f shiyanlou.tar -c ~。
    -v    参数以可视的的方式输出打包的文件。上面会自动去掉表示绝对路径的/，
    -P    保留绝对路径符。
例：
?解包一个文件(-x参数)到指定路径的已存在目录(-C参数)：
$ mkdir tardir
$ tar -xf shiyanlou.tar -C tardir

?只查看不解包文件-t参数：
$ tar -tf shiyanlou.tar

?保留文件属性和跟随链接（符号链接或软链接），有时候我们使用tar备份文件当你在其他主机还原时希望保留文件的属性(-p参数)和备份链接指向的源文件而不是链接本身(-h参数)：
$ tar -cphf etc.tar /etc

对于创建不同的压缩格式的文件，对于tar来说是相当简单的，需要的只是换一个参数，这里我们就以使用gzip工具创建*.tar.gz文件为例来说明。
?我们只需要在创建 tar 文件的基础上添加-z参数，使用gzip来压缩文件：
$ tar -czf shiyanlou.tar.gz ~

?解压*.tar.gz文件：
$ tar -xzf shiyanlou.tar.gz

现在我们要使用其他的压缩工具创建或解压相应文件只需要更改一个参数即可：
压缩文件格式    参数
*.tar.gz         -z 
*.tar.xz         -J 
*tar.bz2         -j 


5.文件系统操作与磁盘管理
5.1查看磁盘和目录的容量
df         查看磁盘的容量
df -h

du         查看目录的容量
   -h      #同--human-readable 以K，M，G为单位，提高信息的可读性。
   -a      #同--all 显示目录中所有文件的大小。
   -s      #同--summarize 仅显示总计，只列出最后加总的值。
例：
#只查看1级目录的信息
$ du -h -d 0 ~
# 查看2级
$ du -h -d 1 ~


6.帮助命令
help ls         内部
ls --help       外部
man ls
info ls


7.任务计划crontab
7.1使用
crontab -e       添加一个计划任务
man crontab      命令查看
#每分钟我们会在/home/shiyanlou目录下创建一个以当前的年月日时分秒为名字的空白文件
$*/1 * * * * touch /home/shiyanlou/$(date +\%Y\%m\%d\%H\%M\%S)
注意:“ % ” 在 crontab 文件中，有结束命令行、换行、重定向的作用，前面加 ” \ ” 符号转意，否则，“ % ” 符号将执行其结束命令行或者换行的作用，并且其后的内容会被做为标准输入发送给前面的命令。
crontab -l      查看添加了那些任务
sudo tail -f /var/log/syslog       查看到执行任务命令之后在日志中的信息反馈
crontab -r       删除任务

f1 f2 f3 f4 f5 program 
其中 f1 是表示分钟，f2 表示小时，f3 表示一个月份中的第几日，f4 表示月份，f5 表示一个星期中的第几天。program 表示要执 
行的程序。 
当 f1 为 * 时表示每分钟都要执行 program，f2 为 * 时表示每小时都要执行程序，其馀类推 
当 f1 为 a-b 时表示从第 a 分钟到第 b 分钟这段时间内要执行，f2 为 a-b 时表示从第 a 到第 b 小时都要执行，其馀类推 
当 f1 为 */n 时表示每 n 分钟个时间间隔执行一次，f2 为 */n 表示每 n 小时个时间间隔执行一次，其馀类推 
当 f1 为 a, b, c,... 时表示第 a, b, c,... 分钟要执行，f2 为 a, b, c,... 时表示第 a, b, c...个小时要执行，其馀类推 
使用者也可以将所有的设定先存放在档案 file 中，用 crontab file 的方式来设定时程表。 
例：
#每天早上7点执行一次 /bin/ls : 
0 7 * * * /bin/ls 
在 12 月内, 每天的早上 6 点到 12 点中，每隔3个小时执行一次 /usr/bin/backup : 
0 6-12/3 * 12 * /usr/bin/backup 
周一到周五每天下午 5:00 寄一封信给 alex@domain.name : 
0 17 * * 1-5 mail -s "hi" alex@domain.name < /tmp/maildata 
每月每天的午夜 0 点 20 分, 2 点 20 分, 4 点 20 分....执行 echo "haha" 
20 0-23/2 * * * echo "haha" 
30 21 * * * /usr/local/etc/rc.d/lighttpd restart 
上面的例子表示每晚的21:30重启apache。 
45 4 1,10,22 * * /usr/local/etc/rc.d/lighttpd restart 
上面的例子表示每月1、10、22日的4 : 45重启apache。 
10 1 * * 6,0 /usr/local/etc/rc.d/lighttpd restart 
上面的例子表示每周六、周日的1 : 10重启apache。 
0,30 18-23 * * * /usr/local/etc/rc.d/lighttpd restart 
上面的例子表示在每天18 : 00至23 : 00之间每隔30分钟重启apache。 
0 23 * * 6 /usr/local/etc/rc.d/lighttpd restart 
上面的例子表示每星期六的11 : 00 pm重启apache。 
0 */1 * * * /usr/local/etc/rc.d/lighttpd restart 
每一小时重启apache 
0 23-7/1 * * * /usr/local/etc/rc.d/lighttpd restart 
晚上11点到早上7点之间，每隔一小时重启apache 
0 11 4 * mon-wed /usr/local/etc/rc.d/lighttpd restart 
每月的4号与每周一到周三的11点重启apache 
0 4 1 jan * /usr/local/etc/rc.d/lighttpd restart 
一月一号的4点重启apache 


8.命令执行顺序控制与管道
cut                选取
-b ：以字节为单位进行分割。这些字节位置将忽略多字节字符边界，除非也指定了 -n 标志。
-c ：以字符为单位进行分割。
-d ：自定义分隔符，默认为制表符，分割区域。
-f  ：与-d一起使用，指定显示哪个区域。
-n ：取消分割多字节字符。仅和 -b 标志一起使用。如果字符的最后一个字节落在由 -b 标志的 List 参数指示的范围之内，该字符将被写出；否则，该字符将被排除。 
cut /etc/passwd -d ':' -f 1,6    打印/etc/passwd文件中以:为分隔符的第1个字段和第6个字段分别表示用户名和其家目录
# 前五个（包含第五个）
$ cut /etc/passwd -c -5
# 前五个之后的（包含第五个）
$ cut /etc/passwd -c 5-
# 第五个
$ cut /etc/passwd -c 5
# 2到5之间的（包含第五个）
$ cut /etc/passwd -c 2-5


grep              在文本中或 stdin 中查找匹配字符串
       -r         表示递归搜索子目录中的文件,
       -n          表示打印匹配项行号，
       -I         表示忽略二进制文件
grep -rnI "shiyanlou" ~  搜索/home/shiyanlou目录下所有包含"shiyanlou"的所有文本文件，并显示出现在文本中的行号
export | grep ".*yanlou$"   查看环境变量中以"yanlou"结尾的字符串，$就表示一行的末尾

wc              用于统计并输出一个文件中行、单词和字节的数目
      -l        只输出行数
      -w        只输出单词数
      -c        只输出字节数
      -m        只输出字符数
      -L        只输出最长行字节数
ls -dl /etc/*/ | wc -l    统计 /etc 下面所有目录数

sort             排序命令
sort [-bcfMnrtk][源文件][-o 输出文件] 
      -b       忽略每行前面开始出的空格字符。
      -c       检查文件是否已经按照顺序排序。
      -f       排序时，忽略大小写字母。
      -M       将前面3个字母依照月份的缩写进行排序。
      -n       依照数值的大小排序。
      -o<输出文件>   将排序后的结果存入指定的文件。
      -r       以相反的顺序来排序。
      -t<分隔字符>   指定排序时所用的栏位分隔字符。
      -k      选择以哪个区间进行排序。
cat /etc/passwd | sort -t':' -k 3 -n

uniq             去重命令
history          命令查看最近执行过的命令（实际为读取${SHELL}_history文件,如我们环境中的/.zsh_history文件）
history | cut -c 8- | cut -d ' ' -f 1 | sort | uniq 输出之前使用过的命令去重 
# 输出重复过的行（重复的只输出一个）及重复次数
$ history | cut -c 8- | cut -d ' ' -f 1 | sort | uniq -dc
# 输出所有重复的行
$ history | cut -c 8- | cut -d ' ' -f 1 | sort | uniq -D


9.简单的文本处理
9.1文本处理命令
tr            删除一段文本信息中的某些文字。或者将其进行转换

使用方式：
tr [option]...SET1 [SET2]
常用的选项有：
选项   说明
-d      删除和set1匹配的字符，注意不是全词匹配也不是按字符顺序匹配 
-s      去除set1指定的在输入文本中连续并重复的字符 
操作举例：
# 删除 "hello shiyanlou" 中所有的'o','l','h'
$ echo 'hello shiyanlou' | tr -d 'olh'
# 将"hello" 中的ll,去重为一个l
$ echo 'hello' | tr -s 'l'
# 将输入文本，全部转换为大写或小写输出
$ cat /etc/passwd | tr '[:lower:]' '[:upper:]'
# 上面的'[:lower:]' '[:upper:]'你也可以简单的写作'[a-z]' '[A-Z]',当然反过来将大写变小写也是可以的

col            可以将Tab换成对等数量的空格键，或反转这个操作
使用方式：
col [option]
常用的选项有：
选项      说明
  -x      将Tab转换为空格 
  -h      将空格转换为Tab（默认选项 
操作举例：
# 查看 /etc/protocols 中的不可见字符，可以看到很多 ^I ，这其实就是 Tab 转义成可见字符的符号
$ cat -A /etc/protocols
# 使用 col -x 将 /etc/protocols 中的 Tab 转换为空格,然后再使用 cat 查看，你发现 ^I 不见了
$ cat /etc/protocols | col -x | cat -A

join          用于将两个文件中包含相同内容的那一行合并在一起。
使用方式：
join [option]... file1 file2
常用的选项有：
选项     说明
  -t       指定分隔符，默认为空格 
  -i       忽略大小写的差异 
  -1       指明第一个文件要用哪个字段来对比，，默认对比第一个字段 
  -2       指明第二个文件要用哪个字段来对比，，默认对比第一个字段 
操作举例：
# 创建两个文件
$ echo '1 hello' > file1
$ echo '1 shiyanlou' > file2
$ join file1 file2
# 将/etc/passwd与/etc/shadow两个文件合并，指定以':'作为分隔符
$ sudo join -t':' /etc/passwd /etc/shadow
# 将/etc/passwd与/etc/group两个文件合并，指定以':'作为分隔符, 分别比对第4和第3个字段
$ sudo join -t':' -1 4 /etc/passwd -2 3 /etc/group

paste          在不对比数据的情况下，简单地将多个文件合并一起，以Tab隔开。
使用方式：
paste [option] file...
常用的选项有：
选项   说明
  -d    指定合并的分隔符，默认为Tab 
  -s    不合并到一行，每个文件为一行 
操作举例：
$ echo hello > file1
$ echo shiyanlou > file2
$ echo www.shiyanlou.com > file3
$ paste -d ':' file1 file2 file3
$ paste -s file1 file2 file3


10.数据流重定向
>     将标准输出导向一个文件
>>    将标准输出追加到一个文件

11.正则表达式基础
11.1基本语法：
一个正则表达式通常被称为一个模式（pattern），为用来描述或者匹配一系列符合某个句法规则的字符串。

选择：
|竖直分隔符表示选择，例如"boy|girl"可以匹配"boy"或者"girl"

数量限定：
数量限定除了我们举例用的*,还有+加号,?问号,如果在一个模式中不加数量限定符则表示出现一次且仅出现一次：
+   表示前面的字符必须出现至少一次(1次或多次)，例如，"goo+gle",可以匹配"gooogle","goooogle"
?   表示前面的字符最多出现一次(0次或1次)，例如，"colou?r",可以匹配"color"或者"colour";
*   星号代表前面的字符可以不出现，也可以出现一次或者多次（0次、或1次、或多次），例如，“0*42”可以匹配42、042、0042、00042等。

语法：
符   描述
\    将下一个字符标记为一个特殊字符、或一个原义字符。例如，“n”匹配字符“n”。“\n”匹配一个换行符。序列“\\”匹配“\”而“\(”则匹配“(”。 
^    匹配输入字符串的开始位置。 
$    匹配输入字符串的结束位置。 
{n}   n是一个非负整数。匹配确定的n次。例如，“o{2}”不能匹配“Bob”中的“o”，但是能匹配“food”中的两个o。 
{n,}   n是一个非负整数。至少匹配n次。例如，“o{2,}”不能匹配“Bob”中的“o”，但能匹配“foooood”中的所有o。“o{1,}”等价于“o+”。“o{0,}”则等价于“o*”。 
{n,m}  m和n均为非负整数，其中n<=m。最少匹配n次且最多匹配m次。例如，“o{1,3}”将匹配“fooooood”中的前三个o。“o{0,1}”等价于“o?”。请注意在逗号和两个数之间不能有空格。 
*     匹配前面的子表达式零次或多次。例如，zo*能匹配“z”、“zo”以及“zoo”。*等价于{0,}。 
+     匹配前面的子表达式一次或多次。例如，“zo+”能匹配“zo”以及“zoo”，但不能匹配“z”。+等价于{1,}。 
?     匹配前面的子表达式零次或一次。例如，“do(es)?”可以匹配“do”或“does”中的“do”。?等价于{0,1}。 
.      匹配除“\n”之外的任何单个字符。要匹配包括“\n”在内的任何字符，请使用像“(.｜\n)”的模式。 
(pattern)  匹配pattern并获取这一匹配的子字符串。该子字符串用于向后引用。要匹配圆括号字符，请使用“\(”或“\)”。 
x｜y      匹配x或y。例如，“z｜food”能匹配“z”或“food”。“(z｜f)ood”则匹配“zood”或“food”。 
[xyz]     字符集合（character class）。匹配所包含的任意一个字符。例如，“[abc]”可以匹配“plain”中的“a”。其中特殊字符仅有反斜线\保持特殊含义，用于转义字符。其它特殊字符如星号、加号、各种括号等均作为普通字符。脱字符^如果出现在首位则表示负值字符集合；如果出现在字符串中间就仅作为普通字符。连字符 - 如果出现在字符串中间表示字符范围描述；如果如果出现在首位则仅作为普通字符。 
[^xyz]    排除型（negate）字符集合。匹配未列出的任意字符。例如，“[^abc]”可以匹配“plain”中的“plin”。 
[a-z]      字符范围。匹配指定范围内的任意字符。例如，“[a-z]”可以匹配“a”到“z”范围内的任意小写字母字符。 
[^a-z]     排除型的字符范围。匹配任何不在指定范围内的任意字符。例如，“[^a-z]”可以匹配任何不在“a”到“z”范围内的任意字符。 

grep         模式匹配命令
      -b 将二进制文件作为文本来进行匹配 
      -c 统计以模式匹配的数目 
      -i 忽略大小写 
      -n 显示匹配文本所在行的行号 
      -v 反选，输出不匹配行的内容 
      -r 递归匹配查找 
      -A n n为正整数，表示after的意思，除了列出匹配行之外，还列出后面的n行 
      -B n n为正整数，表示before的意思，除了列出匹配行之外，还列出前面的n行 
      --color=auto 将输出中的匹配项设置为自动颜色显示 
使用基本正则表达式，BRE：
?位置
查找/etc/group文件中以"shiyanlou"为开头的行
$ grep 'shiyanlou' /etc/group
$ grep '^shiyanlou' /etc/group
?数量
# 将匹配以'z'开头以'o'结尾的所有字符串
$ echo 'zero\nzo\nzoo' | grep 'z.*o'
# 将匹配以'z'开头以'o'结尾，中间包含一个任意字符的字符串
$ echo 'zero\nzo\nzoo' | grep 'z.o'
# 将匹配以'z'开头,以任意多个'o'结尾的字符串
$ echo 'zero\nzo\nzoo' | grep 'zo*'
注意：其中\n为换行符
?选择
# grep默认是区分大小写的，这里将匹配所有的小写字母
$ echo '1234\nabcd' | grep '[a-z]'
# 将匹配所有的数字
$ echo '1234\nabcd' | grep '[0-9]'
# 将匹配所有的数字
$ echo '1234\nabcd' | grep '[[:digit:]]'
# 将匹配所有的小写字母
$ echo '1234\nabcd' | grep '[[:lower:]]'
# 将匹配所有的大写字母
$ echo '1234\nabcd' | grep '[[:upper:]]'
# 将匹配所有的字母和数字，包括0-9,a-z,A-Z
$ echo '1234\nabcd' | grep '[[:alnum:]]'
# 将匹配所有的字母
$ echo '1234\nabcd' | grep '[[:alpha:]]'

特殊符号  说明
[:alnum:] 代表英文大小写字节及数字，亦即 0-9, A-Z, a-z 
[:alpha:] 代表任何英文大小写字节，亦即 A-Z, a-z 
[:blank:] 代表空白键与 [Tab] 按键两者 
[:cntrl:] 代表键盘上面的控制按键，亦即包括 CR, LF, Tab, Del.. 等等 
[:digit:] 代表数字而已，亦即 0-9 
[:graph:] 除了空白字节 (空白键与 [Tab] 按键) 外的其他所有按键 
[:lower:] 代表小写字节，亦即 a-z 
[:print:] 代表任何可以被列印出来的字节 
[:punct:] 代表标点符号 (punctuation symbol)，亦即：" ' ? ! ; : # $... 
[:upper:] 代表大写字节，亦即 A-Z 
[:space:] 任何会产生空白的字节，包括空白键, [Tab], CR 等等 
[:xdigit:] 代表 16 进位的数字类型，因此包括： 0-9, A-F, a-f 的数字与字节 
# 排除字符
$ echo 'geek|good' | grep '[^o]'
注意:当^放到中括号内为排除字符，否则表示行首。

使用扩展正则表达式，ERE
要通过grep使用扩展正则表达式需要加上-E参数，或使用egrep。
?数量
# 只匹配"zo"
$ echo 'zero\nzo\nzoo' | grep -E 'zo{1}'
# 匹配以"zo"开头的所有单词
$ echo 'zero\nzo\nzoo' | grep -E 'zo{1,}'

注意：推荐掌握{n,m}即可，+,?,*，这几个不太直观，且容易弄混淆。
?选择
# 匹配"www.shiyanlou.com"和"www.google.com"
$ echo 'www.shiyanlou.com\nwww.baidu.com\nwww.google.com' | grep -E 'www\.(shiyanlou|google)\.com'
# 或者匹配不包含"baidu"的内容
$ echo 'www.shiyanlou.com\nwww.baidu.com\nwww.google.com' | grep -Ev 'www\.baidu\.com'
注意：因为.号有特殊含义，所以需要转义。

sed        
命令基本格式：
sed [参数]... [执行命令] [输入文件]...
# 形如：
$ sed -i '1s/sad/happy/' test # 表示将test文件中第一行的"sad"替换为"happy"
      -n 安静模式，只打印受影响的行，默认打印输入数据的全部内容 
      -e 用于在脚本中添加多个执行命令一次执行，在命令行中执行多个命令通常不需要加该参数 
      -f filename 指定执行filename文件中的命令 
      -r 使用扩展正则表达式，默认为标准正则表达式 
      -i 将直接修改输入文件内容，而不是打印到标准输出设备 
sed执行命令格式：
[n1][,n2]command
[n1][~step]command
# 其中一些命令可以在后面加上作用范围，形如：
$ sed -i 's/sad/happy/g' test # g表示全局范围
$ sed -i 's/sad/happy/4' test # 4表示指定行中的第四个匹配字符串
其中n1,n2表示输入内容的行号，它们之间为,逗号则表示从n1到n2行，如果为～波浪号则表示从n1开始以step为步进的所有行；command为执行动作，下面为一些常用动作指令：
命令    说明
s     行内替换 
c     整行替换 
a     插入到指定行的后面 
i     插入到指定行的前面 
p     打印指定行，通常与-n参数配合使用 
d     删除指定行 
打印指定行：
# 打印2-5行
$ nl passwd | sed -n '2,5p'
# 打印奇数行
$ nl passwd | sed -n '1~2p'
行内替换：
# 将输入文本中"shiyanlou" 全局替换为"hehe",并只打印替换的那一行，注意这里不能省略最后的"p"命令
$ sed -n 's/shiyanlou/hehe/gp' passwd
注意： 行内替换可以结合正则表达式使用。
行间替换：
$ nl passwd | grep "shiyanlou"
# 删除第21行
$ sed -n '21c\www.shiyanlou.com' passwd
（这里我们只把要删的行打印出来了，并没有真正的删除，如果要删除的话，请使用-i参数）

awk
待学习


12.软件安装
12.1apt包管理
apt-get
        install 其后加上软件包名，用于安装一个软件包 
        update 从软件源镜像服务器上下载/更新用于更新本地软件源的软件包列表 
        upgrade 升级本地可更新的全部软件包，但存在依赖问题时将不会升级，通常会在更新之前执行一次update 
        dist-upgrade 解决依赖关系并升级(存在一定危险性) 
        remove 移除已安装的软件包，包括与被移除软件包有依赖关系的软件包，但不包含软件包的配置文件 
        autoremove 移除之前被其他软件包依赖，但现在不再被使用的软件包 
        purge 与remove相同，但会完全移除软件包，包含其配置文件 
        clean 移除下载到本地的已经安装的软件包，默认保存在/var/cache/apt/archives/ 
        autoclean 移除已安装的软件的旧版本软件包 
     -y 自动回应是否安装软件包的选项，在一些自动化安装脚本中使用这个参数将十分有用 
     -s 模拟安装 
     -q 静默安装方式，指定多个q或者-q=#,#表示数字，用于设定静默级别，这在你不想要在安装软件包时屏幕输出过多时很有用 
     -f 修复损坏的依赖关系 
     -d 只下载不安装 
     --reinstall 重新安装已经安装但可能存在问题的软件包 
     --install-suggests 同时安装APT给出的建议安装的软件包 
安装软件包：
apt-get install <软件包名>
$ sudo apt-get --reinstall install w3m    重新安装：
软件升级
# 更新软件源
$ sudo apt-get update
# 升级没有依赖问题的软件包
$ sudo apt-get upgrade
# 升级并解决依赖关系
$ sudo apt-get dist-upgrade
卸载软件
sudo apt-get remove w3m 
# 不保留配置文件的移除
$ sudo apt-get purge w3m
# 或者 sudo apt-get --purge remove
# 移除不再需要的被依赖的软件包
$ sudo apt-get autoremove
 软件搜索
sudo apt-cache search softname1 softname2 softname3……

12.2dpkg         
dpkg                以deb形式打包的软件包，就需要使用dpkg命令来安装
       -i 安装指定deb包 
       -R 后面加上目录名，用于安装该目录下的所有deb安装包 
       -r remove，移除某个已安装的软件包 
       -I 显示deb包文件的信息 
       -s 显示已安装软件的信息  
       -S 搜索已安装的软件包 
       -L 显示已安装软件包的目录信息 
然后我们将第一个deb拷贝到home目录下，并使用dpkg安装
$ cp /var/cache/apt/archives/emacs24_24.3+1-4ubuntu1_amd64.deb ~
# 安装之前参看deb包的信息
$ sudo dpkg -I emacs24_24.3+1-4ubuntu1_amd64.deb


如你所见，这个包还额外依赖了一些软件包，这意味着，如果主机目前没有这些被依赖的软件包，直接使用dpkg安装可能会存在一些问题，因为dpkg并不能为你解决依赖关系。
# 使用dpkg安装
$ sudo dpkg -i emacs24_24.3+1-4ubuntu1_amd64.deb

我们将如何解决这个错误了，这就要用到apt-get了，使用它的-f参数了，修复依赖关系的安装
$ sudo apt-get -f install

使用dpkg -L查看deb包目录信息
$ sudo dpkg -L emacs








我的问题呢，要是知道呢，那么是萨达哈琳
