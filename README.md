# ubuntu



Win7与Ubuntu 16.04双系统安装教程
2017-12-26

在Win7的基础上使用U盘安装Ubuntu系统总结。


1. 安装前准备工作
1.1 制作启动U盘
我是使用U盘的方式来安装Ubuntu系统的，因此主要介绍这种方式。

首先需要准备好一个2G以上的空U盘（因为之后的操作需要格式化，所以空U盘最好）。

在Ubuntu官网下载<a href="https://www.ubuntu.com/download">Ubuntu 16.04LTS</a>
的ISO安装文件。如果上面的链接有问题，可以从<a href="https://www.ubuntu.com/download/alternative-downloads">这里</a>使用BT方式下载，
或者在其他mirror站点下载。

按照官网步骤下载<a href="https://rufus.akeo.ie/">Rufus</a>并使用上一步中下载好的ISO文件制作启动U盘：<a href="https://www.ubuntu.com/download/desktop/create-a-usb-stick-on-windows">How to create a bootable USB stick on Windows</a>

1.2 电脑磁盘分区
在安装系统之前，需要事先给它分配一定的磁盘空间。其实也可以直接在非Windows系统盘（C盘）上直接安装，但是这样的话如果以后想对Ubuntu系统有单独的操作（比如删除或者别的）就会比较麻烦，所以建议给Ubuntu系统单独分配一定的空间。

在Win7系统中，我们可以通过控制面板/系统和安全/管理工具/创建并格式化硬盘分区，进入磁盘管理工具。 磁盘管理工具
选择一个剩余容量多的分区，右键 > 压缩卷 > 选择合适大小 ，我选择的是100G(一般50G就够用了）

现在准备工作就绪，可以准备安装了。

2. 安装Ubuntu系统
2.1 设置BIOS为U盘启动
将制作好的启动U盘插在电脑上，重启电脑，开机时进入BIOS选择从U盘启动。

不同品牌的电脑BIOS设置不同，请自行百度。

2.2 安装过程
等待片刻，进入Ubuntu系统欢迎界面，选择中文，点击右侧“安装Ubuntu”开始安装。 欢迎界面 也可以选左边先使用Ubuntu系统体验一下（此时没有安装），然后从桌面左上角双击“安装Ubuntu 16.04LTS”图标开始安装。

准备安装界面，勾选“为图形或无线硬件…”，然后点击“继续”（还需要等待一小会儿）。 准备安装界面注意：如果这步花费时间很长说明是网络问题，请关闭无线网络，拔掉网线之后再重试。

安装类型界面，选择“其他选项”（也有教程说可以直接选择第一个“共存”，但是大部分教程认为这样会和Windows安装在一起，导致双系统间相互影响。我没有验证真假，请大家自行判断，我以后换新电脑时再具体实验），然后“继续”。 安装类型界面注意：此时若弹出“已有挂载的分区，是否卸载”窗口一定不要确定，选择“否”，然后退出安装，返回Windows系统检测自己的分区情况，见1.2

接下来是关键的分配分区环节。 分配分区界面 我最大的疑问也在这里，大部分资料认为应该划分四个分区，分别为挂载为“/”，“/home”，“交换空间”和“/boot”。

此处有争议，我在这里给出我安装时的分配方案：

分区	类型	位置	文件系统	挂载点	大小（100G为例）
“/”分区	逻辑分区	空间起始位置	Ext4日志文件系统	“/”	约1/3，34G
“home”分区	逻辑分区	空间起始位置	Ext2文件系统	“/home”	剩余所有，60G
“交换空间”分区	逻辑分区	空间起始位置	交换空间	无	2G-5G，5G
“/boot”分区	逻辑分区	空间起始位置	Ext4日志文件系统	“/boot”	200Mb
注意：安装启动引导器的设备选择“/boot分区”

下面的说明引用自Windows下安装Ubuntu 16.04双系统：

<1>、“/”分区大致相当于windows下的系统盘（C盘），存放系统文件，当在Ubuntu下安装一些软件时，有可以选择路径的，就可以选择“/home”里面,即自定义软件安装路径，但还有一些不能选择安装路径的，就会安装到“/”分区，大部分软件是默认安装到“/”分区下的。还有一点就是这个分区下是不能像平时一样选择”删除”、”复制”、”粘贴”的，选择一个文件或文件夹，右键，是没有这些”删除”…选项的（我不确定是不是所有的文件和文件夹都是这样，毕竟我没有都试一遍）。（当然可以通过一些命令来实现”删除”、”复制”、”粘贴”、”新建”这些功能的，）

<2>、“/home”分区，这个就相当于windows下的非系统盘，像D盘、E盘、F盘…，除了一些特殊的文件，可以像在windows下一样，任意”删除”、”复制”、”粘贴”、”新建”，平时下载的东西都会保存在这个分区，这个分区主要就是用来存放文件。

<3>、”交换空间”，虚拟内存。我总共为这个Ubuntu系统分配了70G的空间，根据我的需要”/” –30G, ”/home“–35G，“交换空间”–5G,由于想把Ubuntu作为我的主系统，需要多安装一些自己编程，学习，平时使用的一些琐碎的软件，所以我把”/”分区分的大了一些。（之前用Ubuntu14.04也是这么分的，当我安装了我需要的软件之　后，满足编程，平时办公之后，”/”分区大概还剩下17-18G，”/home”还剩下20多G，当然是因为，我把能选则安装路径的大都安装在了”/home”下，还下载了7-8G 的视频放在了”/home“下，我把我之前的磁盘使用情况说一下，希望会在你们分配空间大小时能够有所帮助）

具体四个分区的分配：

（1）“/”分区： “逻辑分区”、“空间起始位置”、“Ext4日志文件系统”、挂载点“/”；

（关于这个”/“的分区类型到底是选择”主分区“还是选择”逻辑分区“，我是选择了”逻辑分区“，大多数教程是选择了”主分区“，而且还建议选择”主分区“。我之前选择”主分区“安装成功过，期间没有出现过任何问题，但是还有在选择了”主分区“后，在后面分配”/home“和”交换空间“时出现问题的，你要知道，我已经安装过Ubuntu 很多次，也曾遇到过不少问题，虽然不是16.04。之前用的14.04就是选择了”主分区“，在后面出现了问题，当我选择了”逻辑分区“后就没有出现任何问题，系统也能正常启动、使用，所以这次我就直接选择了”逻辑分区“）。

（2）“/home”分区：“逻辑分区”、“空间起始位置”、“Ext2文件系统”、挂载点“/home”；

（3）“交换空间”：“逻辑分区”、“空间起始位置”、“交换空间”；

（4）“/boot”分区：“逻辑分区”、“空间起始位置”、“Ext4日志文件系统”、挂载点“/boot”。

关于“/boot”分区的评论@小段阿誉：最下面有一个[安装启动引导器的设备]，这个是可以选择的，但是博主没有选择，用了默认的设置，默认的是将Ubuntu启动引导文件安装在了整个硬盘上，这样的话，就是Ubuntu来引导Win系统了，这样有个坏处，就是你将Ubuntu删除的时候，会导致无法引导Win系统；还有一个我认为的不好的地方就是启动页面选择操作系统的时候，列出的选项太多，并不仅仅只列出Win系统和Ubuntu系统两个启动项。

我的做法是：在分区的时候，多分一个200MB的/boot分区，然后安装启动引导器的设备选择/boot分区，安装好后重启，发现直接进入Win系统，并没有两个系统供选择，这时候进入Win系统，用EasyBCD软件添加一个Ubuntu系统启动项。然后重启就会发现出现了两个系统启动项，（我的是Windows 7 和Ubuntu 16.04 LTS）,黑底白字，煞是简洁，就像和当初安装Win7和Win xp双系统时显示的启动项菜单一样。当然，这样做还有个好处就是当你不需要Ubuntu系统时，可以直接格式化Ubuntu系统分区，然后用EasyBCD删除Ubuntu的引导项就可以了，而不会影响Win系统的启动哦。

具体分析请看下列博客：

http://blog.chinaunix.net/uid-7547035-id-60111.html

http://blog.csdn.net/arcsinsin/article/details/17143163

http://blog.csdn.net/frank_good/article/details/49177753

当上面的分区分好之后，点击”现在安装“,再次确认分区，然后一路简单的“选择位置”、“键盘布局”、“创建用户”之后继续，开始安装，请耐心等待。 正在安装界面

安装成功后重启电脑，如果你在之前的步骤中在安装启动引导器的设备选择“/boot分区”的话，此时会自动进入Windows系统，此时需要添加系统启动项才能进入新系统。



3 双系统兼容问题
经过上面的步骤，Win7和Ubuntu双系统已经安装成功了。但是经常在两个系统间切换的朋友可能会发现它们之间有一些兼容的问题，下面介绍其中一些我遇到的问题。

3.1 同步系统时间
下面解决方案引用自：解决ubuntu和windows双系统时间差异8小时的方法及Win7+Ubuntu双系统安装完成后时间不一致相差大概8小时

Windows/Ubuntu 双系统用户会发现在 Ubuntu 里面的时间正常的情况下Windows的系统时间被改到8小时前。原来 Linux 操作系统是以 CMOS 时间做为格林威治标准时间，再根据系统设置的时区来确定目前系统时间。但是Windows 会直接修改CMOS 时间。而中国的时区是+8区，所以才会造成时间被调整了-8个小时。

所以您可以让 Windows 去使用时区或者让 Ubuntu 使用本地时间。

解决方案如下：

Windows：(此方法没有测试）

修改 Windows 使用时区的方法是在注册表：

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation\

下面增加一个名为RealTimeIsUniversal的REG_DWORD键，并赋值为1。

Ubuntu(16.04之前)：

而让Ubuntu 使用本地时间的方法是：

sudo gedit /etc/default/rcS

把里面的UTC=yes改为UTC=no

Ubuntu(16.04及以后)：

打开终端输入

#先在Ubuntu下更新一下时间
sudo apt-get install ntpdate
#使用window的
sudo ntpdate time.windows.com

#将时间更新到硬件上
sudo hwclock --localtime --systohc

回车重启！OK了


故障现象：
先安装Windows7 SP1 64位版，后使用U盘安装Ubuntu 14.04.1。Ubuntu安装成功后，可正常启动，而GRUB上选择Windows 7菜单项，无法启动到Win7界面，直接返回GRUB菜单界面。

解决办法 <a href="http://blog.csdn.net/caimagic/article/details/39532911">这里</a>

<h1 >mysql </h1>
安装：

参考网址：
http://www.cnblogs.com/EasonJim/p/7147787.html



而在16.04版本上，由于使用了Systemd进行接管，以上脚本无法使用，那么需要使用以下脚本来禁止才能通过：

#禁止开机启动
sudo systemctl disable mysql
#开机启动
sudo systemctl enable mysql


<h3>mysql的简单操作</h3>
参考网址 ：https://www.jianshu.com/p/694d7d0a170b

<h4>登陆mysql数据库</h4>

可以通过如下命令：

$ mysql -u root -p
$ mysql -h localhost -u root -p
-u 表示选择登陆的用户名
-p 表示登陆的用户密码
-h 登录主机名
<hr />

<h4>常用命令</h4>

create database new_dbname;--新建数据库<br />
drop database old_dbnane; --删除数据库<br />
show databases;--显示数据库<br />
use databasename;--使用数据库<br />
select database();--查看已选择的数据库<br />

show tables;--显示当前库的所有表<br />
create table tablename(fieldname1 fieldtype1,fieldname2 fieldtype2,..)[ENGINE=engine_name];--创建表<br />
drop table tablename; --删除表<br />
create table tablename select statement;--通过子查询创建表<br />
desc tablename;--查看表结构<br />
show create table tablename;--查看建表语句<br />

alter table tablename add new_fielname new_fieldtype;--新增列<br />
alter table tablename add new_fielname new_fieldtype after 列名1;--在列名1后新增列<br />
alter table tablename modify fieldname new_fieldtype;--修改列<br />
alter table tablename drop fieldname;--删除列<br />
alter table tablename_old rename tablename_new;--表重命名<br />

insert into tablename(fieldname1,fieldname2,fieldnamen) valuse(value1,value2,valuen);--增<br />
delete from tablename [where fieldname=value];--删<br />
update tablename set fieldname1=new_value where filename2=value;--改<br />
select * from tablename [where filename=value];--查<br />

truncate table tablename;--清空表中所有数据，DDL语句<br />

show engines;--查看mysql现在已提供的存储引擎:<br />
show variables like '%storage_engine%';--查看mysql当前默认的存储引擎<br />
show create table tablename;--查看某张表用的存储引擎（结果的"ENGINE="部分）<br />
alter table tablename ENGINE=InnoDB--修改引擎<br />
create table tablename(fieldname1 fieldtype1,fieldname2 fieldtype2,..) ENGINE=engine_name;--创建表时设置存储引擎<br />

