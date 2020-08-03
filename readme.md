

[TOC]

`#`表示root用户

`$`表示普通用户

centOS安装文件用的是`yum`命令

`ctrl+c`是强制中断程序的运行，进程已终止

`ctrl+z`将任务中止（暂停）

`ctrl+d`表示EOF

# 文件系统

Linux操作系统具有一定层次结构，由若干目录和子目录组成，不同于windows操作系统，Linux只有一个根目录，用“/”表示，它采用的是**级层式的树形结构**。
----*在Linux世界里，一切皆文件。*
![在这里插入图片描述](https://tva1.sinaimg.cn/large/007S8ZIlly1ghahadx3sjj30ml0bcq4k.jpg)

## 具体的目录结构

- /lib [library]

> 系统默认库路径文件

- /etc [etcetera]

> 所有程序所需要的配置文件

- /bin[**重点**] (/usr/bin、/usr/local/bin）[binary]

> 是Binary的缩写，这个目录存放着**最经常使用的命令**

- /sbin （/usr/sbin、/usr/local/sbin）[superuser binary]

> s就是Super User的意思，这里存放的是系统管理员使用的系统管理程序。

- /home[**重点**]

> 存放普通用户的主目录，在Linux中每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的。

- /root[**重点**]

> 该目录为系统管理员，也称作超级权限者的用户主目录。

- boot[**重点**」

> 存放的是启动Linux时使用的一些核心文件，包括一些连接文件以及镜像文件T

- 下列目录和linux内核相关，慎用！

> - /proc [process]
>     这个目录是一个虚拟的目录，它是系统内存的映射，访问这个目录来获取系统信息。
> - /srv [service]
>     service缩写，该目录存放一些服务启动之后需要提取的数据。
> - /sys
>     这是linux2.6内核的一个很大的变化。该目录下安装了2.6内核中新出现的一个文件系统

- /tmp [temporary]

> 这个目录是用来存放一些临时文件的。

- /dev [device]

> 类似于winlows的设备管理器，把所有的硬件用文件的形式存储。

- /media[**重点**]

> linux系统会自动识别一些设备，例如U盘、光驱等等，当识别后，linux会把识别的设备挂载到这个目录下。

- /mnt [**重点**] [mount]

> 系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将外部的存储挂载在/mnt/上，然后进入该目录就可以查看里的内容了。

- /opt [option]

> 这是给主机额外安装软件所摆放的目录。如安装ORACLE数据库就可放到该目录下。默认为空。

- /usr/local[**重点**]

> 这是别一个给主机额外安装软件所安装的目录。一般是通过编译源码方式安装的程序。

- /var[**重点**] [variable]

> 这个目录中存放着在不断扩充着的东西，习惯将经常被修改的目录放在这个目录下。包括各种日志文件。

- /selinux[security-enhanced linux] (类似于360)

> SELinux是一种安全子系统，它能控制程序只能访问特定文件。

## 小结

1. Linux的目录**有且只有**一个根目录
2. Linux的**各个目录存放的内容是规划好**的，**不能**随便乱放文件。
3. Linux以文件的形式管理我们的设备，因此Linux系统，一切皆文件。
4. Linux的文件系统是一个**树形结构**，每个分叉（子目录）有特定的功能。





# LINUX

## Vim

```
***vim***

yy 拷贝当前行
5yy 拷贝当前行及向下的共5行

p 粘贴到光标后
P[paste] 粘贴到光标前

u[undo] 撤销命令

dd 删除当前行
5dd 删除当前行及向下的共5行

/find 查找单词`find`,按n寻找下一个,N寻找上一个
:noh，可以取消搜索

`:set nu` `:set nonu` 显示/取消行号

G 定位到最末行
gg 定位到最首行
4G 定位到第4行


i 在光标处插入
a 在光标后一格插入
o 在下一行插入新行并进入插入模式
O 在上一行插入新行并进入插入模式
I 在行首进入插入模式
A 在行末进入插入模式

v 开始标记
y 复制标记内容

ctrl+b[backward] 上一页
ctrl+f[forward] 下一页
ctrl+u[up] 上移半屏
ctrl+d[down] 下移半屏
```

## 关机

```
***关机***

shutdown -h[halt] now   立刻关机
shutdown -h[halt] 1     1min后关机
shutdown -r[reboot] now 立即重启

halt 关机
reboot 重启

sync 把内存的数据同步到磁盘[建议在关机或重启前执行sync指令，防止数据丢失]
```

## 用户管理

``` 
***用户***

`su[select|switch user] root` `su - root` 切换成Root管理员账户，加`-`显示上次登陆地点时间

logout 需要在Royal TSX内使用，可以注销账户，关闭连接（我测试也返回上一个账户）
exit[ctrl+d] 退出账户，返回上一个账户

添加用户 useradd xm, 用户创建成功后，会自动在`/home`创建`/home/xm`同名家目录
也可以指定目录（必须为创建）useradd -d[directory] /home/dog xq ,dog就是xq的家目录

# passwd xm 给xm指定密码

删除用户必须用root
# userdel xm 删除用户但保留家目录
# userdel -r[recursion|recursively] xm 删除用户及其家目录
通常删除用户，保留家目录

id root 查询用户的uid,gid,组，不存在，返回无此用户

whoami 查看当前登录的用户

用户组(root用户来操作)
# groupadd test 增加组
# groupdel test 删除组
增加用户时直接加上组 # useradd -g[group] 用户组 用户名
# usermod[modify] -g[group] 用户组 用户名


用户和组的相关文件
/etc/passwd,用户配置文件（用户信息）,利用vim查看，最后几行包含内容为：
`better:x:1000:1000:better:/home/better:/bin/zsh`
用户名:密码:用户id:组id:用户家目录:用户的shell

/etc/group，组配置文件（组信息）,最后几行内容：
`better:x:1000:`
组名:口令:组标志号:组内用户列表(隐藏)

/etc/shadow，口令配置文件（密码和登录信息，是加密的），最后几行显示内容：
`better:$6$Ktuy0JkE$Kf./v2yLnrCjTI.jsRvWHlBEIhSbWVygIBmNljG6BfC5KVeG1oukY7fkNQ4unmW0Db.PKMVT6/hFDDUHjpcKP.:18474:0:99999:7:::`
登录名:加密口令:最后一次修改时间:最小时间间隔:最大时间间隔:警告时间:不活动时间:失效时间:标志
```

## 运行级别

```
***运行级别***
指令运行级别7个，在`/etc/inittab`里配置系统的运行级别
0.关机
1.单用户(找回丢失密码)
2.多用户无网络服务
3.多用户有网络服务
4.保留
5.图形界面 <-----所在级别
6.重启

切换运行级别指令:# init [012356]
这样可以用来找回root密码：
我们先进入单用户模式，然后修改root密码，因为进入单用户模式，root不需要密码就可以进入。

步骤：
1.开机在引导时输入 e
2.看到一个界面输入e，再看到一个界面选中第二行(加载内核)，再输入e
3.在出现一行末输入空格+1，和enter，再按b，表示进入了单用户模式。
4.可以使用`passwd root` 修改root密码

```
## 帮助指令

```
***帮助指令***
当我们对某个指令不熟悉时，可以用命令查看这个指令的使用放方法。

man[manual] [命令或配置文件](功能描述，获得帮助信息)
$ man ls

help 命令 (获得shell内置命令的帮助信息)
$ help cd (zsh这个shell没有help命令，bash有)

```
## 文件目录类指令


文件目录类  
```
pwd[Print Working Directory],显示当前工作目录的绝对路径

ls[list] [选项] [目录或文件]
选项 -a[all],-A[almost all],-l[long]长格式,-h[human-readable]，文件大小带单位。
$ ls /

cd [change directory],有绝对路径和相对路径
cd ~ 或者 cd,返回家目录
cd .. 返回上一级

mkdir[Make Directory] [选项] 要创建的目录
-p[parents],创建多级目录,指多个文件夹
$ mkdir -p /home/better/桌面/1/2/ ,创建了 1/2/

rmdir[remove directory] 删除的空目录
只能删除空的目录

如何删除非空目录
$ rm -rf[recursion|recursively,forcefully] 目录

touch 创建空文件,可同时创建多个
$ touch hello1.txt hello2.txt

cp拷贝指令[copy]
cp [选项] source destination
选项: -r[recursion|recursively],递归复制整个文件夹
$ cp /1.txt /home ,拷贝在/home/1.txt,文件名未变
$ cp /1.txt /2.txt ,拷贝后的文件为2.txt,拷贝文件的目标的父文件夹必须是存在的文件夹
$ cp -r dir1/ dir2/(dir2不存在) ,将dir1/目录的内容，复制到dir2/内。
$ cp -r dir1/ dir2/(dir2存在) ,将dir1目录的内容，复制到dir2/dir1/内。
	   如果最后一个命令参数为一个已经存在的目录名，cp会将每一个源文件
       复制到那个目录下(维持原文件名).
$ cp ./* /home,也可以拷贝多个文件,home是已经存在的目录，且不会拷贝`./`里的目录，只拷贝文件,加个-r选项,可以拷贝目录。

强制覆盖
$ \cp -r dir1/ dir2/
```

删除指令  
```
# rm -rf /* ，这个指令禁止执行！
rm[remove] [选项] 要删除的文件或目录
选项：-r[recursively]递归删除整个文件夹，-f[forcefully]强制删除不提示
$ \rm 也是强制删除(相当于 -f )

$ rm或cp或mv -i[interactive]，表示可以提示是否删除或覆盖文件，我在zsh配置文件里配置了[-i]选项
```

移动指令  
```
mv 移动文件与目录或重命名
$ mv oldnameFile newnameFile 重命名
$ mv /1.c /home , 表示移动到/home/1.c
$ mv /1.c /home/2.c ，表示移动到/home/2.c 
```

cat指令查看文件内容  
```
cat[concatenate] [选项] 文件
选项：-n[number],显示行号,只能浏览浏览文件，不能修改文件，为了浏览方便,带上管道命令 |more|less
$ cat -n 1.c|more 或者 |less, 可以分页显示
```

more指令  

more指令是一个基于VI编辑器的文本过滤器，它以全屏幕的方式按页显示文本文件的内容、more指令中内置了若干快捷键。  

```
$ more /etc/profile
以下为快捷键
--------------------------------------
空格       向下滚一屏
ctrl+f    向下滚一屏
ENTER     向下翻一行
3+enter   向下翻3行
q         立刻立刻more。不再显示该文件内容
b/ctrl+b  返回上一屏
=         输出当前行号
:f        输出文件名和当前行号
--------------------------------------
更多快捷键：
-------------------------------------------------------------------------------
<space>                 Display next k lines of text [current screen size]
z                       Display next k lines of text [current screen size]*
<return>                Display next k lines of text [1]*
d or ctrl-D             Scroll k lines [current scroll size, initially 11]*
q or Q or <interrupt>   Exit from more
s                       Skip forward k lines of text [1]
f                       Skip forward k screenfuls of text [1]
b or ctrl-B             Skip backwards k screenfuls of text [1]
'                       Go to place where previous search started
=                       Display current line number
/<regular expression>   Search for kth occurrence of regular expression [1]
n                       Search for kth occurrence of last r.e [1]
!<cmd> or :!<cmd>       Execute <cmd> in a subshell
v                       Start up /usr/bin/vi at current line
ctrl-L                  Redraw screen
:n                      Go to kth next file [1]
:p                      Go to kth previous file [1]
:f                      Display current file name and line number
.                       Repeat previous command
-------------------------------------------------------------------------------
```

less指令  
less指令用来分屏查看文件内容，less指令在显示文件内容时，并不是一次将整个文件加载之后才显示，而是根据显示需要加载内容，对于显示较大型文件具有较高效率。  

```
$ less -N(显示行号) -m(显示百分比) /etc/profile
快捷键
------------------------------------------------
空格       向下滚动一屏
b         向上滚动一屏
回车       向下滚动一行
y         向上滚动一行
d         向下滚动半屏
u         向上滚动半屏
h         less的帮助
g         跳到第一行
G         跳到最后一行
/字串      向下搜寻[字串]的功能，n:向下查找，N:向上查找
?字串      向上搜寻[字串]的功能，n:向上查找，N:向下查找
q         退出less
------------------------------------------------
更全的：
 ---------------------------------------------------------------------------

                           MOVING

  e  ^E  j  ^N  CR  *  Forward  one line   (or N lines).
  y  ^Y  k  ^K  ^P  *  Backward one line   (or N lines).
  f  ^F  ^V  SPACE  *  Forward  one window (or N lines).
  b  ^B  ESC-v      *  Backward one window (or N lines).
  z                 *  Forward  one window (and set window to N).
  w                 *  Backward one window (and set window to N).
  ESC-SPACE         *  Forward  one window, but don't stop at end-of-file.
  d  ^D             *  Forward  one half-window (and set half-window to N).
  u  ^U             *  Backward one half-window (and set half-window to N).
  ESC-)  RightArrow *  Left  one half screen width (or N positions).
  ESC-(  LeftArrow  *  Right one half screen width (or N positions).
  F                    Forward forever; like "tail -f".
  r  ^R  ^L            Repaint screen.
  R                    Repaint screen, discarding buffered input.
---------------------------------------------------------------------------
```

```
>指令和>>指令,他们可以创建文件（如果文件不存在）
>为输出重定向，>>为追加
1) ls -l > 文件         列表的内容覆盖到文件
2) ls -la >> 文件		  列表的内容追加到文件
3) cat 文件1 > 文件2     文件1内容覆盖文件2
4) echo "内容" >> 文件

cal[calendar]，显示日历


echo 指令
echo [选项] [输出内容]
应用，使用echo指令输出环境变量，输出当前的环境路径
$ echo $PATH 
/usr/local/bin:/usr/bin:/home/better/bin:/usr/local/sbin:/usr/sbin

head 命令
$ head [-n 5][-5] 文件，显示文件的开头5行，默认为10行
tail 命令
$ tail [-n 5][-5] 文件，显示文件的结尾5行，默认为10行
$ tail -f[follow] 文件，实时追踪该文档的所有更新,ctrl+c退出


ln指令
软链接🔗，也叫符号链接，类似于windows里的快捷方式，主要存放了链接其他文件的路径
$ ln -s[symbolic] [原文件或目录] [软链接名] （功能：给原文件创建一个软链接）
其中，如果软链接一个目录，进入这个目录，pwd后，仍在软链接所在位置,`我的电脑`是一个软链接
如下：`/home/better/桌面/我的电脑/home/better`
`/home/better/桌面/我的电脑/home/better/桌面/我的电脑/home/……`

删除软链接注意！
$ rm -rf 我的电脑, 不要加`/`，如果加`/`，会吧该目录下面的内容删除。

history指令
查看已经执行过历史命令，也可以执行历史命令
$ history     查看所有历史命令
$ history 10  查看最近使用过的10个命令
$ !5          执行历史编号为5的指令
```

## 日期时间类指令

```
***时间日期类***

date指令，显示当前日期
1)date             			显示当前时间
2)date +%Y                  显示当前年份
3)date +%m                  显示当前月份
4)date +%d                  显示当前是哪一天
5)date "+%Y-%m-%d %H:%M:%S" 显示年月日时分秒（`+`不要丢）

设置日期
$ date -s[set] "2020-10-10 11:22:22"

cal[calendar]查看日历
$ cal 31 3 2018
-------------------------------------
用法：
 cal [选项] [[[日] 月] 年]
选项：
 -1, --one        只显示当前月份(默认)
 -3, --three      显示上个月、当月和下个月
 -s, --sunday     周日作为一周第一天
 -m, --monday     周一用为一周第一天
 -j, --julian     输出儒略日
 -y, --year       输出整年
-------------------------------------

```

## 搜索查找类

```
***搜索查找类***

find指令
find指令将从指定目录向下递归地遍历其各个子目录，将满足条件的文件或者目录显示在终端
find [搜索范围] [选项]
选项:
-name<查询文件名>  按照指定的文件名查找模式查找文件
$ find /home -name 1.txt 或 *.txt
-user<用户名>    查找属于指定用户名所有文件
$ find /opt -user root
-size<文件大小>  按照指定的文件大小查找文件
$ find / -size +20M/+20k         大于20M
               -20M              小于20M
                20M              等于20M
按ctrl+c退出检索
```
locate指令  
locate指令可以快速定位文件路径。locate指令利用事先建立的系统中所有文件名称及路径的locate数据库实现快速定位给定的文件，locate指令无需遍历整个文件系统，查询速度较快。为了保证查询结果的准确度，管理员必须定期更新locate时刻。  

```
$ locate 搜索文件
第一次运行前，必须使用updatedb[data-base]指令创建locate数据库。
# updatedb / $ sudo[Superuser do] updatedb

grep指令和管道符号|
grep过滤查找，管道符,"|",表示将前一个命令的处理结果输出传递给后面的命令处理
grep [选项] 查找内容 源文件
-n[list-number] 显示匹配行及行号
-i[ignore-case] 忽略字母大小写
$ grep -ni hello 1.c 或者 $ cat 1.c | grep -ni hello

```

## 压缩和解压命令

```
***压缩和解压命令***

gzip和gunzip指令
gzip[GNU zip]用于压缩文件，只能压缩为*.gz文件,gunzip[GNU unzip]用于解开被gzip压缩的文件。
但是压缩后，原文件就没有了。
$ gzip 1.c        ==>   生成`1.c.gz`, `1.c`就没有了
$ gunzip 1.c.gz   ==>   r生成`1.c`  , `1.c.gz`就没有了
在 Linux 中，打包和压缩是分开处理的。而 gzip 命令只会压缩，不能打包，所以才会出现没有打包目录，而只把目录下的文件进行压缩的情况。


zip/unzip命令
zip用于压缩文件，unzip用于解压的，这个在项目打包发布中很有用的
zip [选项] dest.zip 要压缩的目录或文件  
$ zip -r dest.zip /home/
-r[recursively] 递归压缩，即压缩目录~

unzip [选项] source.zip
unzip选项：-d<directory>,指定解压后文件的存放目录
$ unzip -d dest/ source.zip，dest目录可以不存在

tar[tape archive]指令
tar指令是打包指令，最后打包的文件是`.tar.gz`的文件。
tar [选项] dest.tar.gz 打包内容 （打包目录或文件）
-c   产生.tar打包文件[create]
-v   显示详细信息[verbose]
-f   指定压缩后的文件名[file]
-z   打包同时压缩[gzip]
-x   解包.tar文件[extract]
$ tar -zcvf a.tar.gz 1.c 2.c (f在最后一个)
$ tar -zcvf a.tar.gz /home/  注意和/home/*的区别
解压
$ tar -zxvf a.tar.gz
$ tar -zxvf a.tar.gz -C[directory指定解压目录] /home/ 注意，指定解压目录必须存在
```

## 组管理和权限管理

```
Linux中的每个用户必须属于一个组，不能独立于组外。
Liunx每个文件具有1.所有者2.所在组3.其他组的概念

1)所有者
2)所在组
3)其它组
4)改变用户所在的组

文件/目录的所有者
一般来说，文件的创建者，便成为该文件的所有者
查看文件的所有者:
$ ls -ahl[all,human-readable,long],
`-rw-rw-r--.  1 better better    0 8月   1 20:51 1.c`
中间两个分别为所有者和所在组。而所在的组，一般是所有者所在的组，但是也可以改变。

修改文件所有者
chown[change owner] 用户名 文件名, 但是文件的所在组没有变化。

修改文件所在组
chgrp[change group] 组名 文件名 ，但是文件的所有者没有变。

其它组：除文件的所有者和所在组的用户外，系统的其他用户都是文件的其它组。

改变用户所在组
1)# usermod -g[group] 组名 用户
2)# usermod -d 目录名 用户名，改变该用户登录的初始目录


*权限的基本介绍*
ls -l显示:
`-rw-r--r--.  1 better better    0 8月   1 20:51 1.c`

第一个字符`-`表示文件类型,`-`是普通文件，`d`是目录，`l`是软链接，`c`是字符设备(鼠标，键盘),`b`是块文件，硬盘

第二到第四个字符`rw-`表示文件所有者拥有的权限，r是读，w是写，-是没有权限

第5到第7个字符`r--`表示文件所在组的用户的权限，`r--`只读

第8到第10个字符`r--`表示文件其它组的用户的权限，`r--`只读

`1` ，如果是文件，表示硬链接的数，一般是1，如果是目录，表示该目录的子目录的个数。

better是文件所有者，后面的better是文件所在组

`0`   表示文件的大小，不加单位指单位是字节,Byte
如果是目录的话，该值为4096(字节)

`8月  1 20:51`是文件的最后修改时间

```

rwx权限  
1. rwx作用到文件  
    1) [r]代表可读，可以读取查看  
    2) [w]代表可写,可以修改，但是不代表可以删除该文件，删除一个文件的前提条件是对该文件所在的目录有写权限，才能删除文件  
    3) [x]代表可执行[execute]:可以被执行  
2. rwx作用到目录  
    1) [r]代表可读，可以读取，ls查看目录内容  
    r权限：拥有此权限表示可以读取目录结构列表，也就是说可以查看目录下的文件名和子目录名，注意：仅仅指的是名字。  
    2) [w]代表可写，可以修改，在该目录内 创建+删除+重命名 文件或目录  
    w权限：拥有此权限表示具有更改该目录结构列表的权限，总之，目录的w权限与该目录下的文件名或子目录名的变动有关，注意：指的是名字。具体如下：  
           1.在该目录下新建新的文件或子目录。   
           2.删除该目录下已经存在的文件或子目录（不论该文件或子目录的权限如何），注意：这点很重要，用户能否删除一个文件或目录，看的是该用户是否具有该文件或目录所在的目录的w权限。  
           3.将该目录下已经存在的文件或子目录进行重命名。  
           4.转移该目录内的文件或子目录的位置。  
    3) [x]代表可执行，可以进入该目录  
           x权限：拥有目录的x权限表示用户可以进入该目录成为工作目录，能不能进入一个目录，只与该目录的x权限有关，如果用户对于某个目录不具有x权限，则无法切换到该目录下，也就无法执行该目录下的任何命令，即使具有该目录的r权限。且如果用户对于某目录不具有x权限，则该用户不能查询该目录下的文件的内容，注意：指的是内容，如果有r 权限是可以查看该目录下的文件名列表或子目录列表的。所以要开放目录给任何人浏览时，应该至少要给与r及x权限。  

```
**权限管理**
chmod[change mode] 修改文件或目录权限
1)u:所有者 g:所在组 o:其他人 a:所有人(u、g、o的总和)
 $ chmod u=rwx,g=rx,o=x 文件，给该文件的所有者读写执行的权限，所在组读和执行的权限，其他组执行的权限,当文件某个权限有x时，就会在终端显示成绿色。
 
 $ chmod o+w 文件，其它组用户增加写权限
 $ chmod a-x 文件，给所有用户减去执行权限
 $ chmod u-x,g+w 1.c，这样写。
如果使其它组没有权限，chmod 'o=' 或者 'o=-' 或者 'o=--' 或者 'o=---'

2)数字方式
r=4, w=2, x=1
rwx   = 4+2+1 = 7
rx    = 4+1   =5
x     = 1 
无权限 = 0
chmod 751 1.c ,表示chmod u=7,g=5,o=1 1.c，即chmod u=rwx,g=rx,o=x 1.c
改变目录及其子文件子目录可以 chmod -R 777 1.c

*修改文件所有者chown*
1)# chown newowner file 改变文件的所有者
2)# chown newowner:newgroup file 改变文件的所有者和所在组
3)-R[--recursive] 如果是目录，则使得其下所有文件或目录递归生效

修改文件所在组
# chgrp newgroup 文件或目录
# chgrp -R newgroup 目录
/home 该目录下，除root外，其他用户没有w权限

只有root用户可以修改文件所在组和所有者
对于文件目录的权限，只有所有者和root用户可以修改
```

## 任务调度

```
crond任务调度,系统在某个时间执行的特定的命令或程序
分类：
1.系统工作：有些重要的工作必须周而复始地执行。如病毒扫描等
2.个别用户工作：个别用户可能希望执行某些程序，比如备份
语法
crontab [选项]
-e[edit] 编辑crontab定时任务
-l[Displays the current crontab on standard output.]     查询crontab任务
-r[Removes the current crontab]     删除当前用户所有的crontab任务 
service crond restart 重启任务调度
 
1.如果只是简单的任务，可以不用写脚本，直接在crontab中加入任务即可
2.对于比较复杂的任务，需要些脚本（shell编程）

1)在crontab中输入 `*/1 * * * * ls -l /home >> /home/better/桌面/1.txt` 
 表示每小时的每分钟执行ls -l /home >> /home/better/桌面/1.txt 命令

5个占位符的说明
第一个`*`表示一小时当中的第几分钟 0-59
第二个`*`表示一天中的第几小时    0-23
第三个`*`表示一个月中的第几天    1-31
第四个`*`表示一年中的第几月      1-12
第五个`*`表示一周当中的星期几     0-7（0和7表示星期日）

参数说明
*     代表任何时间
,     代表不连续的时间，`8,9,10`表示这三个时间都执行任务
-     代表连续的时间范围。比如`1-6`表示连续六个时间
*/n   代表每隔多久执行一次， */1和*效果一样
```

![image-20200803162445685](https://tva1.sinaimg.cn/large/007S8ZIlly1ghdp9lyw0qj313e0i0amw.jpg)

```
任务调度的应用
1）我们编写脚本文件实现每隔1分钟将日期追加到文件
①编写文件 /home/better/桌面/task.sh
  添加内容 date >> /home/better/桌面/1.txt
②给task.sh一个可执行权限（根据谁要执行这个脚本来确定权限）
③crontab -e 
④添加`* * * * * /home/better/桌面/task.sh`
```

## Linux磁盘分区、挂载

```
分区方式
1)MBR分区：[Master Boot Record]
  1.最多支持四个主分区
  2.系统只能安装在主分区
  3.扩展分区要占一个主分区
  4.MBR最大只支持2TB，但拥有最好的兼容性
2)GPT分区[GUID Partition Table]
  1.支持无限多个主分区（但操作系统可能限制，windows最多128个分区）
  2.最大支持18EB的大容量
  3.windows7 64位以后支持gpt
```

windows分区

![image-20200804001015963](https://tva1.sinaimg.cn/large/007S8ZIlly1ghe2px9m1mj31560hedsk.jpg)

Linux分区  

Linux来说无论有几个分区，分给哪一目录使用，它归根结底就只有一个根目录，一个独立且唯一的文件结构, Linux中每个分区都是用来组成整个文件系统的一部分。  
Linux采用了一种叫“载入”的处理方法，它的整个文件系统中包含了一整套的文件和目录，且将一个分区和一个目录联系起来。这时要载入的一个分区将使它的存储空间在一个目录获得。  


![image-20200803191629543](https://tva1.sinaimg.cn/large/007S8ZIlly1ghdu89gtlbj31c20r47hl.jpg)

硬盘说明
1)   Linux硬盘分IDE硬盘和SCSI硬盘，目前基本上是SCSI硬盘  
2)  对于IDE硬盘， 驱动器标识符为“hdx\~",其中“hd”表明分区所在设备的类型，这里是指IDE硬盘了。“x"为盘号(a为基本盘，b为基本从属盘，c为辅助主盘，d为辅助从属盘),“~”代表分区，前四个分区用数字1到4表示，它们是主分区或扩展分区，从5开始就是逻辑分区。例，hda3表示为第一个IDE硬盘上的第三个主分区或扩展分区,hdb2表示为第二个IDE硬盘上的第二个主分区或扩展分区.  
3)  对于SCSI硬盘则标识为'sdx~", SCSI硬盘是用“sd"来表示分区所在设备的类型的，其余则和IDE硬盘的表示方法一样。  

```
$ lsblk[list block device] -f ， 查看自己的系统分区情况
Swap分区在系统的运行内存不够用的时候，把物理内存中的一部分空间释放出来，以供当前运行的程序使用。
----------------------------------------------------------------------------------
NAME            FSTYPE  LABEL   UUID                                   MOUNTPOINT
sda
├─sda1          xfs             71020384-c026-493d-9b87-138b700b8022   /boot
└─sda2          LVM2_me         KmJqpC-MiUP-aGvk-0UWh-ycM9-yn83-cJo6dp
  ├─centos-root xfs             15a68c53-18ab-4960-a185-f382e1c3070e   /
  └─centos-swap swap            f0a429f4-5d07-4488-bb09-a541ba69590c   [SWAP]
sr0             iso9660 CentOS 7 x86_64
                                2020-04-22-00-54-00-00                 /run/media
-----------------------------------------------------------------------------
$ lsblk 查看具体大小
--------------------------------------------------------------------------
NAME            MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda               8:0    0   20G  0 disk
├─sda1            8:1    0    1G  0 part /boot
└─sda2            8:2    0   19G  0 part
  ├─centos-root 253:0    0   17G  0 lvm  /
  └─centos-swap 253:1    0    2G  0 lvm  [SWAP]
sr0              11:0    1  4.5G  0 rom  /run/media/better/CentOS 7 x86
--------------------------------------------------------------------------
```

![image-20200803193315870](https://tva1.sinaimg.cn/large/007S8ZIlly1ghdupojmhqj31ee0kekab.jpg)

```
挂载案例
增加一块2G硬盘，标识为sdb1，挂载到/home/newdisk
1)虚拟机添加硬盘 ，在设置里添加
2)分区    fdisk /dev/sdb（下图）
3)格式化   mkfs -t ext4 /dev/sdb1
4)挂载    先创建文件/home/newdisk  挂载 mount /dev/sdb1 /home/newdisk
5)设置可以自动挂载(永久挂载) 
  vim /etc/fstab
  增加内容，`/dev/sdb1（分区）    /home/newdisk(挂载点)   ext4(类型)    defaults  0 0`
  mount -a 自动挂载即刻生效
  
卸载 umount /dev/sdb1 或者 umount /home/newdisk

```

![image-20200803201327105](https://tva1.sinaimg.cn/large/007S8ZIlly1ghdvvierbgj30pm0bc451.jpg)



## 磁盘情况查询

```
查询系统整体磁盘使用情况
$ df[disk find] [-h]/[-lh]
--------------------------------------------------------------
文件系统                 容量  已用  可用 已用% 挂载点
devtmpfs                 894M     0  894M    0% /dev
tmpfs                    910M     0  910M    0% /dev/shm
tmpfs                    910M   11M  900M    2% /run
tmpfs                    910M     0  910M    0% /sys/fs/cgroup
/dev/mapper/centos-root   17G  4.8G   13G   29% /
/dev/sda1               1014M  187M  828M   19% /boot
tmpfs                    182M   28K  182M    1% /run/user/1000
--------------------------------------------------------------

查询指定目录的磁盘占用情况
du -h [目录]
默认为当前目录，-s指定目录占用大小汇总，-h带计量单位，-a含文件
--max-depth=1 子目录深度，-c列出明细的同时，增加汇总值
-s仅仅显示该目录的占用大小，c是列出明细也显示总的占用大小，a包含文件。
--------------------------------------------------------------------
$ du -ach --max-depth=1 /home/better
58M	/home/better/.mozilla
4.0K	/home/better/.bash_logout
4.0K	/home/better/.bash_profile
4.0K	/home/better/.bashrc
du: 无法读取目录"/home/better/.cache/gnome-control-center": 权限不够
91M	/home/better/.cache
4.0K	/home/better/.dbus
du: 无法读取目录"/home/better/.config/gnome-control-center": 权限不够
124K	/home/better/.config
8.0K	/home/better/.ICEauthority
19M	/home/better/.local
4.0K	/home/better/.esd_auth
0	/home/better/桌面
0	/home/better/下载
0	/home/better/模板
0	/home/better/公共
0	/home/better/文档
0	/home/better/音乐
876K	/home/better/图片
0	/home/better/视频
4.0K	/home/better/.bash_history
13M	/home/better/.oh-my-zsh
0	/home/better/.pki
40K	/home/better/.zcompdump-localhost-5.0.2
20K	/home/better/.zsh_history
4.0K	/home/better/.lesshst
4.0K	/home/better/.zshrc
4.0K	/home/better/.viminfo
181M	/home/better
181M	总用量
--------------------------------------------------------------------------

另外的工作使用指令
1）统计/home文件下文件的个数
  $ ls -l /home |grep "^-" |wc -l[lines]   ,(ls -la可以查询包括隐藏文件在内的文件)
  wc -l是统计前面的行数
  "^-"是正则表达式
  
  
```

