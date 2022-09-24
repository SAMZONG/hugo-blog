# Linux 笔试试题



```
一. 选择题 （1题1分）
1. 当登录Linux时，一个具有唯一进程ID号的shell将被调用，这个ID是什么(   )
A. NID　　B. PID　　C. UID　　D. CID
答案:B
2. 用vi打开一个文件，如何用字母"new"来代替字母"old" (   )
A. :s/old/new/g　　　B. :s/old/new　　C. :1,$s/old/new/g　　　D. :r/old/new
答案:A
3. 请选择对标准的变量PS2正确的描述(   )
A. 是一个主shell提示符变量　　　　B. 是一个一般的shell提示符变量
C. 是第二主shell提示符变量　　   D. 是一个连续提示符变量
答案:B
4. 哪一个命令能用来查找文件TESTFILE中只包含四个字符的行?(   )
A. grep '^????$' TESTFILE　　　　B. grep '????' TESTFILE
C. grep '^....$' TESTFILE　　　　　D. grep '....' TESTFILE
答案:C
5. 一个bash shell脚本的第一行是什么(   )
A. #!/bin/bash　　B. #/bin/bash　　C. #/bin/csh　　　D. /bin/bash
答案:A
6. 用标准的输出重定向(>)像"> file01"能使文件file01的数据（   ）
A. 被移动　　B. 被复制　　C. 被打印　　　D. 被覆盖
答案:D
7. 下面哪个命令是用来定义shell的全局变量(    )
A. exportfs　　B. alias　　C. exports　　D. export
答案:D
8. 如果想加载一个/dev/sdb1的windows95分区到/mnt/win95目录，需要运行哪个命令(   )
A. mount -t hpfs /dev/sdb1 /mnt/win95
B. mount -t hpfs /mnt/win95 /dev/sdb1
C. mount -t vfat /dev/sdb1 /mnt/win95
D. mount -t vfat /mnt/win95 /dev/sdb1
答案:C
9. 哪个文件存放用户密码信息(   )
A. /boot/passwd　　　B. /etc/shadow　　　C. /var/passwd　　D. /dev/passwd
答案:B
10. 假定kernel支持vfat分区，下面哪一个操作是将/dev/sda1，一个window98分区加载到/win目录(   )
A. mount -s win /dev'sda1 /win
B. mount -fs=msdos /dev/sda1 /win
C. mount -t vfat /dev/sda1 /win
D. mount -t windows /win /dev/sda1
答案:C
11. 默认情况下管理员创建了一个用户，就会在(   )目录下创建一个用户主目录。
A. /usr　　B. /home　　　C. /root　　D. /etc
答案:B
12. 如果要列出一个目录下的所有文件需要使用命令行(    )。
A. ls –l　　B. ls　　　C. ls –a　　　D. ls -d
答案:C
13. 利用哪个工具可以设置用户在文件系统中的空间大小(   )。
A. turboservice　　B. turbofscfg　　C. turbonetcfg　　　D. turboxcfg
答案:B
14. 哪个命令可以将普通用户转换成超级用户(   )
A. super　　B. passwd　　C. tar　　　D. su
答案:D
15. 哪个命令用来显示/home及其子目录下文件名(   )
A. ls -R /home　　B. ls -d /home　　C. ls -a /home　　　　D. ls -l /home
答案:A
16. 在vi模式下，哪个命令用来删除光标处的字符(    )
A. xd　　　B. x　　　C. dd　　　D. d
答案:B　　dd删除一行,x删除当前字符
17. 在一行内运行多个命令需要用什么字符隔开(   )
A. @　　B. $　　　C. ;　　D. *
答案:C
18. 确定myfile的文件类型的命令是(   )
A. whatis myfile
B. file myfile
C. type myfile
D. type -q myfile
答案:B
19. 哪些命令组合起来能统计多少用户登录系统(    )
A. who | wc –w　　　B. who | wc –l　　　C. who | wc –c　　　D. who | wc
答案:BD
20. 用 "rm -i",系统会提示什么来让你确认(   )
A. 命令行的每个选项　　B. 是否真的删除　　C. 是否有写的权限　　　D. 文件的位置
答案:B
21. Linux启动的第一个进程init启动的第一个脚本程序是(   )。
A. /etc/rc.d/init.d　　　B. /etc/rc.d/rc.sysinit　　C. /etc/rc.d/rc5.d　　D. /etc/rc.d/rc3.d
答案:B
22. 按下(   )键能终止当前运行的命令
A. Ctrl-C　　　B. Ctrl-F　　　C. Ctrl-B　　　D. Ctrl-D
答案:a
23. 用来分离目录名和文件名的字符是(   )
A. dash (-)　　B. slash (/)　　C. period (.)　　　D. asterisk（*）
答案:B
24. 系统的配置文件在(  )目录下
A. /home　　　B. /dev　　C. /etc　　　D. /usr
答案:C
25. 显示用户的主目录的命令是什么?(   )
A. echo $HOME　　B. echo $USERDIR　　　C. echo $ENV　　D. echo $ECHO
答案:A
26. 在vi编辑器里，哪个命令能将光标移到第200行(    )
A. g200　　B. G200　　C. :200　　　D. 200g
答案:C
:200可以，200G也可以
27. 用"useradd jerry"命令添加一个用户，这个用户的主目录是什么?(   )
A. /etc/jerry　　　B. /var/jerry　　C. /home/jerry　　　D. /bin/jerry
答案:C
28. 哪一个命令能用来删除当前目录及其子目录下名为'core'的文件(   )
A. find . -name core -exec rm {} \ ;
B. find . -name core -exec rm ;
C. find . -name core -exec rm {} ;
D. find . -name core -exec rm {} -;
答案:A
29. 以下哪条命令在创建一个xp用户的时候将用户加入到root组中(  )
A. useradd -g xp root　　B. useradd -r root xp　　C. useradd -g root xp　　　D. useradd root xp
答案:C
30. 不改变运行级别而重新读入inittab文件的命令是(    )。
A. init s　　B. init q　　C. init S　　　D. init Q
答案:B
31. 以下哪个命令可以终止一个用户的所有进程(   )
A. skillall　　　B. skill　　C. kill　　　D. killall
答案:D
32. 通过修改哪个文件可以在创建用户的时候改变用　户主目录的路径(   )
A. /etc/default/passwd　　　B. /etc/default/useradd　　C. /etc/profile　　D. /etc/fstab
答案:B
33. 以只读方式打开一个文件并进入vi编辑器的命令是(   )
A. view -r filename　　　B. view filename　　　C. vi filename　　　D. vi -r filename
答案:B
34. 以下哪个命令是将缓存中的内容粘贴到光标之前(   )
A. a　　　B. i　　　C. P　　　D. p
答案:C
35. 以下哪条vi命令能将文档5-20行间出现的abc替换成为cba (   )
A. :1,$s/abc/cba/g　　　B. :5,20/abc/cba/g　　C. :5-20s/abc/cba/g　　　D. :5,20s/abc/cba/g
答案:D
. 在vi中通过哪条命令可以将ps命令执行的结果插入到文档中(   )
A. :r!ps　　　B. :!ps　　　C. :!rps　　　　D. :w!ps
答案:A
36. 以下哪个vi命令可以在当前位置插入/etc/passwd文本文件(   )
A. :r /etc/passwd　　　B. :i /etc/passwd　　C. :w /etc/passwd　　　D. :s /etc/passwd
答案:A
37. vi中复制整行的命令是(   )
A. y1　　　B. yy　　　C. ss　　　D. dd
答案:B
38. 以下哪个vi命令可以给文档的每行加上一个编号(    )
A. :e number　　　B. :set number　　C. :r!date 　　　　D. :200g
答案:B
38. 以下哪些文件只有根用户才能读写(   )
A. /etc/bashrc　　　B. /etc/profile　　　C. /etc/shadow　　　　D. /etc/passwd
答案:BC
39. 使用groupdel删除一个组的时候，命令执行失败，原因可能是(   )
A. 该组是系统组　　　B. 该组是空的　　　C. 该组中成员非空　　　D. 该组不存在
答案:CD
40. Linux中文件名构成的规则比较灵活表现在(   )
A. 文件名长度多达256个字符　　　　　B. 可以使用除了/符号外的所有ASCII字符
C. 不区分大小写　　　　　　　　　　　　D. 无扩展名限制
答案:ABD
41. 对用户的口令进行加解锁的命令是passwd,参数选项是(   )
A. –l　　B. –L　　C. –u　　　D. -U
答案:AC
42. 如果你对文件和目录的权限不确定，则不能用(   )命令来检测权限
A. ps　　　B. ck　　　　C. ls –l　　　D. chown
答案:ABD
43. 选择对/proc文件系统不正确的描述(    )
A. 通常情况下，不提供中断、IO端口、CPU等信息　　　B. /proc文件系统可以提供系统核心的许多参数
C. /proc是一个虚拟的文件系统　　　　　　　　　　　　D. 可以得到系统中运行的进程的一些信息
答案:A
44. 以下哪些符号可以用来连接多条命令(   )
A. ||　　　　B. &&　　　C. ;　　　D. |
答案:ABCD
45. 在shell中，下面哪些字符串当作普通字符串时候需要使用"\"来转义(   )
A. 分号(;)　　　B. 双引号(")　　C. 单引号(')　　　D. 反斜杆(\)
答案:BCD
46. Linux中提供了几个重要的工具用来改变服务和进程的运行状态和运行级别以及初始化进程，它们是(   )。
A. chkconfig　　B. service　　C. turboservice　　　D. ksysv
答案:ABCD
47. 在/etc/rc.d/init.d目录下的所有脚本至少支持两个运行参数,它们是(    )。
A. start　　　B. restart　　　　C. stop　　　D. reload
答案:AC
48. Linux一般被称为是稳定的服务器系统，它的安全性表现在(   )
A. 网络防火墙　　B. 用户管理策略　C. 系统、目录、文件的权限控制　D. 封闭源码便于及时修正漏洞等
答案:ABC
49. 在vi中下列哪些命令不能用来在光标前插入文本(   )
A. p [text]　　B. i [text]　　C. o [text]　　　D. a [text]
答案:ACD
50. 在本地的文件系统中下列哪些linux路径结构是无效的(   )
A. \usr/zhang/memo　　　B. /usr/zhang/memo　　　C. //usr\zhang/memo　　　D. \usr\zhang\memo
答案:ACD

二、简答题 （1题3分）

1.常见的Linux发行版本都有什么？你最擅长哪一个？它的官网网站是什么？说明你擅长哪一块？

2.Linux开机启动流程详细步骤是什么？系统安装完，忘记密码如何破解？

4.某一天突然发现Linux系统文件只读，该怎么办呢？完整操作步骤。

5.安装一台系统使用DVD光盘安装，如何安装50台Linux系统如何安装呢？思考一下。

6.用虚拟机安装了一台Linux系统，突然想克隆一台服务器，克隆后发现无法上网，如何解决？

7.Linux网卡配置文件路径是什么？要使服务器上外网，必须满足的条件有哪些？需要配置什么？

8.一般可以使用什么软件远程linux服务器？通过什么上传文件和下载文件？

9./mnt目录主要用于什么？/root目录跟root用户有什么关系？/根目录与/boot目录有什么联系？

10.某一天误操作，执行了rm  -rf  * ，会有哪些情况发生？请举例。



三、 公有云题目 （1题5分）
1. 请解释上云的好处是什么？传统业务类型与公有云也为类型有什么区别？请举例说明。

2. 列出你用过的阿里云\AWS\Azure服务？并讲述他们的作用？

3. 请列出你觉得阿里云\AWS\Azure目前的特色和不成熟的地方是那些？你觉得应该如何改正。

4. 请用阿里云\AWS\Azure设计一个视频网站的架构图并进行解释说明。

```

