# Getting Started with TimesTen Classic 开始学习TimesTen Classic 

这一章节描述了安装TimesTen Classic数据库之前需要熟悉的一些主题的概览以及说明。
关于TimesTen Scaleout的相关信息，查看《Oracle TimesTen In-Memory Database Scaleout User''s Guide》中的
""Prerequistes and Installation of TimesTen Scaleout""


相关主题包括：

1. 关于安装和实例的概览
2. 在Linux/Unix 系统上安装和实例的管理
3. 在window上关于安装和实例的管理
4. 理解TimesTen的用户组
5. 操作系统相关预准备
6. 规划TimesTen classic的安装以及部署
7. 环境变量

## 安装和实例的概览
这一章节讨论下面的这些主题
1. 安装媒介以及安装包
2. 实例管理员：安装者(Installation)
3. TimesTen 的安装
4. 实例管理员： 实例(Instance)
5. 实例的的home 目录
6. 实例的配置文件(timesten.conf)

注意： TimesTen 的版本号数可以反映在映下TimesTen 工具的输出，文件名称，或者目录名称这些项目。
这些项目很小的该动，无法及时的反映在文档内容中。 这个文件尽力保持输出的主要格式，文件名，
文件夹名以及其他可能反映版本的代码中。 你可以通过查看Release Note 获取通过运行 ttVersion 工具来查看当前版本。


### 安装媒介以及安装包
TimesTen 产品被打包进你下载的安装媒介中。 针对所支持的不同的平台，TimesTen 被打包进一个发行包中。 一个发型包包含一个单一
的Zip 文件。 对于Linux 平台，发型包的文件名包含了发行版本的版本号以及对于的平台。 
例如 对于release 18.1.2.1.0，发行包的名称是 timesten181210.server.linux8664.zip  使用这个文件来用于全产品的安装或者仅仅安装客户端。 没有将客户端安装包单独分出来。 
对于Windows平台， 发行包的名字包含了版本号以及平台。 例如  tomesten181210.win64.zip

对于Linux和Unix 主机，只有一个发型包包含了全部的产品，包括客户端，服务器端，直接模式(direct mode), daemons 等。 
对于Windows 主机。 一个发型版本中包含了TimesTen的客户端。 

飞： 疑惑， windows 上面只能安装客户端，不能安装服务器端软件么？？？

### 实例管理员: Installation 
在Linux/Unix上，安装过程的第一步就是指定哪一个操作用户来解压安装包。这个操作系统用户被叫做 
实例管理员(instance administrator). 当操作系统用户解压好安装包治好，安装也就完成了。
查看"TimesTen installations" 来查看TimesTen 的安装信息。  实例管理员同样对实例有一个角色管理。
 (The instance administrator also plays a role in instance). 查看"Instance adminsstrator： Instance" 来了解更多的信息。 

在Windows 平台上，实例管理员是指 解压缩安装包并且执行安装器的操作系统用户。 查看""Instance adminstrator: Instance ""来了解实例管理员解压缩安装包后的作用。 

关于实例管理员需要注意的：
1. 不能够是root用户
2. 在安装路径下具有对所有文件的读的权限以及执行的权限。 
3. 是TimesTen 用户组的一个成员。 (查看 ""Understanding the TimesTen uses group"" 来了解更多的信息)

### TimsTen 安装
当操作系统用户在主机上解压缩TimesTen的安装包之后，安装就已经完成了。 因此一个安装就是一个发行版本文件解压缩之后主机上的一系列文件。安装路径(installation directory) 就是安装解压缩后得到的文件。

解压缩发行版本的用户是唯一一个可以删除安装的用户。 

注意：
1. 安装是只读的，因此在安装过程中不要添加，修改或者移除文件或路径。 
2. TimesTen 不包含任何的安装的安装仓库
3. 文件路径包含多字节字符时不被支持的


这一章节提供了下面的内容
1. TimesTen在Linux 和Unix 系统上面的安装
2. TimesTen在Windows 系统上面的安装

#### TimesTen 在Linux Unix 系统上面的安装
针对在Linux 和 Unix 主机系统上面的安装
1. 在Linux主机上, 支持TimesTen Classic 和TimesTen Scaleout 的全产品安装或者客户端的安装。 
2. 在Unix 主机上, 仅仅支持TimesTen classic 的全产品以及客户端的安装。 （暂时不提供对TimesTen Scaleout的支持）
3. 一个安装中可以创建多个实例
4. 如果一个安装安装在一个共享文件服务器，例如NFS, 那么一个安装可以通过多个主机来共享。
查看 ""Share an installation from a network-attached storage device"".
 

查看"Creating an installation on Linux/Unix" 来获取更多的信息 

实例管理员(instance administartor)可以运行 ttInstallationCheck 工具来检验安装是否有其它期望的内容或者权限。
查看 ""Verify an installation on Linux/Unix"" 来获取更多的信息。 


#### TimesTen 在Windows 系统上面的安装
在Windows 平台上，当你解压缩Zip 文件之后，实例管理员可以运行WIN64 子目录下的setup.exe安装器来完成软件的安装。 该过程创建了一个单一的安装以及一个单一的实例。 没有额外的实例将会被创建。 

TimesTen 客户端可连接 Linux或者Unix 系统上面的TimesTen scaleout以及TimesTen Classic 数据库。
 
查看"Creating an installation on Windows" 了解更多的信息。 


#### TimesTen实例
安装过程的第二步是创建一个实例(instance). 

一个实例是指： 
1. 一个运行的TimesTen 后台进程(timestend) 以及它的子进程以及相关联的进程。 还有相关联的配置文件以及其它必须的支持文件。(全实例安装)
2. 一系列的配置文件以及使用TimesTen 客户端需要的其他必须的支持文件(只安装客户端的实例)

其他的信息：
1. 一个实例有一个单独的实例管理员， 该管理员就是创建实例的用户。   (飞： 疑惑，是不是说一个linux上面的用户只能创建一个TimesTen实例呢？如果要在Linux上面创建多个TimesTen实例，是不是需要需要通过多个用户来创建了？？)
2. 每一个实例都有它自己的实例主目录(instance home). 该目录是目录结果的顶级目录。  
3. 全实例安装可以管理一个或者多个数据库，但是只有客户端的实例不能有他自己的数据库。 
4. 在一个安装中可以运行多个实例

TimesTen does not maintain an inventory of instances on a host and does not maintain
an inventory of all instances associated with a particular installation.
TimesTen 不包含一个主机上面的安装仓库，也不包含多个安装的所有实例的安装仓库。 

在Linux/Unix 系统
1. 实例管理员是唯一一个可以运行 ttInstanceCreate 工具的用户。 
2. 在大多数环境中，一个安装以及每个主机上面的一个实例是足够的。 但是如果需要的话，一个主机上可以通过一个安装来创建多个实例。 如果一个安装是通过例如NFS 形式的网络共享存储来实现的， 那么一个安装可以支持在多个主机上面的多个安装。 
3. ttInstanceCreate 工具确保实例管理员不能再TimesTen的安装树目录下创建实例。  查看 "The ttInstanceCreate utility"来查看关于ttInstanceCreate 的更多信息。 查看 "Instance administrator： Instance" 来了解实例管理员的更多信息。 

在Windows平台上， 在安装过程中会创建一个安装以及一个实例，该实例名称是 instance。 

#### 实例管理员: Instance 
在 Linux/Unix 平台上， 实例管理员是指可以使用ttInstanceCreate 工具来创建实例的用户，以及所有实例的管理员。
在 Windows 平台上，实例管理员是指解压缩发行版本并且执行安装管理器的用户。 (在Windows 平台上，没有 ttInstanceCreate 工具)

对于全安装的实例管理员来说。 创建和管理数据库，从数据库中加载数据到内存中，或者从内存中加载数据到数据库中， 修改以及销毁实例，执行所有的管理工作，执行备份和恢复操作。 
对于只安装客户端的实例管理员来， 修改以及销毁实例，在Windows 平台， 只支持客户端实例。 

在Linux 以及 Unix 平台上
1. 安装和实例必须拥有相同的用户(实例管理员)
2. 在实例管理员创建好实例之后，你不能修改实例管理员。 

在Windows 平台
1. 安装数据库和创建实例的用户必须是同一个用户(实例管理员)
2. 在管理员执行installer 之后，你不能羞羞鬼实例管理员

####实例home目录
在Linux/Unix平台， instance home 是指实例管理员执行 ttInstanceCreate 工具的路径。 
在Windows 平台，instance home 是指实例管理员运行安装器installer 后创建的目录。 

该目录(instance home )归实例管理员所拥有。 

在instance home目录下包含实例相关的所有配置文件。 它由TimesTen文档中的timesten_home指示。

有两种类型都的instance home：
1. full instance home: 支持对TimesTen的全部使用， 包括服务端以及直接模式(direct mode)
		它必须是宿主机上面的一个本地路径，用于实例的运行。 
2. Client-only instance home: 日工必要的文件来运行TimesTen 客户端当TimesTne 被配置称为使用仅客户端模式的时候创建。 

在Linux/Unix 平台上， 关于特定的TimesTen 实例的用户必须使用ttenv 脚本来设置他们自己的环境变量。 
在Windows 平台上，你既可以在安装的时候进行永久注册，也可以执行ttenv.bat 脚本来进行设置。 

注意： 
1. 一个单实例instance home 不能被超过一个的实例共享
2. instance home包含一个到相关安装的顶级目录的连接

#### 实例配置文件(timesten.conf)
实例配置文件定义了TiemsTen 后台进程的属性。 它驻留在 timesten_home/conf 目录下 并且命名为 timesten.conf。 该文件是一个ASCII 文本文件，是由一个一个的键值对组成的。

下面是一个示例配置文件，注释使用# 进行区分

	# TimesTen Instance Configuration File
	# Created by ttInstanceCreate 
	hostname=host1
	timesten_release=18.1
	instance_name=instance1
	daemon_port=6624
	server_port=6625
	tns_admin=
	admin_user=myadmin
	admin_uid=12345
	group_name-ttgroup
	instance_guid=458665856545685654SIS
	verbose=1

这里面的一些取值是TimesTen 提供的，另外一些是你可选的， 或者是在安装或者示例创建和修改过程中指定的。 
要了解该配置文件 timesten.conf 的更多信息 查看 《Oracle TimesTen In-Memory Database Reference》	中的 "Timesten Instance Configuration File"


## Installation and instance management on Linux/UNIX
Linux/Unix 上面的TimesTen的安装和实例管理
这些主题提供了Linux/Unix 上面安装和实例管理的概览
安装管理
1. 在Linux/Unix上面创建安装
2. 在Linux/Unix上面删除安装
3. 在Linux/Unix上面共享安装

实例管理
1. 在Linux/Unix上面创建实例
2. 在Linux/Unix上面修改实例
3. 在Linux/Unix上面为实例打补丁
4. 在Linux/Unix移除实例

### 在Linux/Unix上面创建安装
实例管理员通过解压缩发行版本来创建安装。 查看"Distribution media and the distribuion" 查看关于安装包的相关信息，
查看 ""Creating an installation on Linux/Unix"" 查看关于在Linux/Unix上面创建安装的相关信息。 
实例管理员可以通过通过运行 ttInstallationCheck命令校验安装是否具有对应的文件缺失以及相关的权限。 
通过查看"Verify an installation on Linux/Unix" 查看更多的信息。 

### 在Linux/Unix上面删除安装
只有创建该安装的实例管理员才可以删除该安装。 查看"Instance administrator:Installation" 查看关于实例管理员的更多信息。
 删除安装是通过手动删除安装树来实现的。 安装树是在安装相关的文件以及目录。  查看第二章的 "Deleting an installation on Linux/Unix" 查看更多的信息。 

### 在Linux/Unix上面共享安装
安装是只读的，并且可以很容易的进行共享以及克隆。 你可以对安装执行如下相关的操作：
1. 通过多个主机共享安装： TimesTen 可以通过在一个网络共享盘来进行安装。 这里的Network Attachedd Storage (NAS) 可以是NFS 或者是其他同等设备。 实例可以在共享同一个共享安装的前提下，在多个主机上创建实例。 查看第二章的 "Share an installation from a network-attached storage device" 了解更多的信息
2. 将一个安装克隆到多个主机上：因为安装是一成不变的，因此，你可以将安装文件打包，然后在其他主机上面解压缩。 只要所有文件都完成了复制并且权限保持不变，那么安装就是有效的。 你可以使用 ttInstallationCheck 命令来校验安装是否成功。 查看第二章的 "Copy an installation to another host "了解更多的信息。 


### 在 Linux/UNIX 上面创建实例
完成了安装的实例管理员(通过解压缩发行文件)是唯一可以创建实例的用户。 查看第一章的"Instance adminstrator: Installation" 
查看关于实例管理员的更多信息。 实例管理员通过执行安装目录的/bin目录下的ttInstanceCreate 工具来创建实例。 

实例管理员通过在执行 ttInstanceCreate 命令的时候，带上 -clientonly 参数来创建一个只有客户端的实例。
如果实例管理员在执行 ttInstanceCreate 的时候，没有带上 -clientonly 选项， 那么TimesTen 将会创建一个全实例安装。  查看第一章的"TimesTen instance" 了解管理TimesTen 实例的更多信息。 

ttInstanceCreate 命令创建一个实例，并且创建一个实例的home目录，设置实例home目录的相关权限。 并且使用相关的文件填充该目录。 查看第一章的"Instance home" 查看关于home directory 的更多信息。 查看第二章的"Creating an instance on Linux/UNIX:Basics" 查看关于ttInstanceCreate 命令以及创建一个实例的更多信息。 

### 在Linux/UNIX 上面修改实例
只有创建了TimesTen 安装的实例管理员才可以修改实例。 查看第一章的 ""Instance administrator: Installation "" 了解关于实例管理员的更多信息。 实例管理员通过运行安装/bin 路径下的 ttInstanceModify 工具来修改相关的实例。 查看第一章的"" Instance home "" 查看关于该目录的更多信息。 

实例管理员通过运行 ttInstanceModify 工具可以进行交互性或者指定一个支持选项。 通过查看第二章的 ""Modifying an instance of Linux/UNIX "" 来及关于ttInstanceModify 工具以及修改实例的更多处理过程。 
实例管理员可以通过修改实例的配置文件来改变实例的属性。 查看第一章的"Instance configuration file(timesten.conf) ""了解关于实例配置文件timestend.conf 的更多信息。  查看《Oracle TimesTen In-Memory Database Reference》 中的""TimesTen Instance Configuration File" 可以获得更多的信息。 

### 在Linux/UNIX系统上为实例打补丁
实例补丁参与对实例的更新以及降级。 一个实例可以从TimesTen的一个补丁版本到之后的一个补丁版本完成实例的更新。 例也可以从一个补丁版本到之前的一个补丁版本完成实例的降级。 升级或者降级只能在同一个主版本内进行(例如可以从 18.1.w.x 到 18.1.y.z ,但是不能从 11..2.2.x.y 到 18.1.x.y.0)。 
创建了安装以及实例的实例管理员才能对实例进行升级或者降级。  查看第一章的"Instance administrator:Insstallation" 查看关于实例管理员的更多信息。 实例管理员通过 ttInstanceModify 工具完成实例的升级或者降级。 

实例的升级或者降级涉及到不同安装的相关实例。 实例管理员可以通过在运行 ttInstanceModify 命令的时候带上 -install 选项来完成该功能。 (不懂)

查看第二章的"Modify an instance on Linux/UNIX" 离阿基关于ttInstanceModify 工具的更多信息。 查看第二章的"Associate an instance with a different installation(updrage or downgrade)" 了解不同安装关联实例的处理过程。 

##在Linux/Unix上面删除实例
只有进行了安装和实例安装的实例管理员才可以删除实例。 查看第一章的"Instance adminstrator:Installation" 了解关于实例管理员的更多信息。 实例管理员通过运行安装路径下/bin 目录下的 ttInstanceDestroy 命令完成实例的删除。 

需要通过设置的TIMESTEN_HOME环境变量来检测要删除的实例。 查看第一章的"Environment variables" 来交接环境变量以及它的设置。 


## Installation and instance management on Windows
(有空的时候在翻译)

## Understanding the TimesTen users group 
在 Linux/Unix 平台：
TimesTen 严格控制从安装路径安装和实例创建的用户必须是一个操作用户组的成员。 这个用户组的成员叫做 "TimesTen user group"。 该组具有数据库的安装以及实例的创建权限。 在安装之前，创建这个用户组(例如 timesten) 并且添加想要添加的操作系统用户到该组中。 一旦你创建了TimesTen 用户组, 你将不能修改该组的名称以及组额ID. 
任何用户想要通过TimesTen 工具访问该数据库，或者访问该数据库的直接模式，该用户必须是TimesTen 用户组的成员。 

在Windows 平台：
1. TimesTen 将被实例管理员进行安装。 该实例管理员必须是TimesTen user group 中的一员。  
2. TimesTen  的安装信息保存在Windows的注册表中。 

飞： 疑惑： 这里的意思， 应该是timesten 的用户组可以是任何的名字，那么这个组名字，应该在哪里进行定义呢。 






## Operating system prerequisites 
操作系统的先决条件
在安装TimesTen classic 之前，确保你检测并且执行了这些操作系统的先决条件。 
1. Linux prerequisites
2. AIX prerequisites

### Linux Prerequisites
在Linux上面执行如下先决条件的检查
1. 创建TimesTen 用户组
2. 配置 shmmax 以及 shmall
3. 配置 HugePages 
4. 修改 memlock 设置
5. 设置 信号量的取值

### 创建TimesTen用户组
这一部分概览了创建TimesTen 用户组的步骤：
1. 创建TimesTen 用户组并且添加期望的用户。 
2. 确定哪一个操作系统用户将会成为实例管理员。 该用户必须是用户组的成员。 该用户进行相关的安装。 
不要创建和TimesTen 预定义的用户相同名称的用户.(GRID, PUBLIC, SYS, SYSTEM 或者 TTREP)

下面的例子以 instanceadmin 作为操作系统用户， timesten 作为用户组的名称。 

1. 创建TimesTen 用户组，组名为timesten，组Id 为1000. 在配置大页面(HugePages)的时候，需要该信息。  查看第一章的"Configure HugePages"查看相关信息。 

	# sudo groupadd -g 10000 timesten

2. 创建用户名 instanceadmin ，对应的UID 是55000， 同时将该用户的主group 设置为timesten。 然后为instanceadmin用户设置密码

	# sudo useradd -u 55000 -g timesten instanceadmin 
	# sudo passwd instanceadmin 

### 配置shmmax 和shmall 
为了共享内存片段足够大来容纳数据库的所有的共享内存片段，你需要配置Linux的 共享内存。 在TimesTen classic 中，所有的数据库内容驻留在一个共享内存片段。 

在Linux中，共享内存片段是由pages 组成的, 默认的page 的大小是 4kb，你可以通过运行 getconf PAGESIZE 命令来校验默认page的大小。 
	% getconf PAGESIZE 
	4096 

配置下面的这些共享内存相关的内核参数来控制共享内存片段的大小。
1. shmmax: 单个共享内存片段的的最大大小(单位bytes)。该值必须足够的以容纳整个数据库的内存片段。 

2. shmall: 所有共享内存片段的系统边界。该变量的取值应该是 默认page size(4k)的整数倍。 并且必须大于等于shmmax的取值。 建议你将shmall的取值设置为小于等于总的物理内存的大小。 通过运行 cat /proc/meminfo 命令查看系统总的内存大。 

数据库的大小取决于 PermSize， TempSize， LogBufMB 的大小，以及Connections 连接属性(The 1 value is TimesTen system overhead)
在18.1.2.1.0 版本中，数据库大小的计算方式如下：(下面的计算公式，在将来的版本中，可能发生改变。 )
PermSize + TempSize + LogBufMB + 1 + (0.042 * Connections) 
这里PermSize, TempSize 以及LongBufMB 的单位是MB(megabytes). 
这里PermSize， TempSize， LogBufMB的大小以及Connections 连接数属性是你在 sys.odbc.ini或 odbc.ini 文件中定义的大小。 

如果你没有为这个值定义变量,TimesTen 将会使用默认值。  查看 《Oracle TimesTen In-Memory Database Reference》 中的 "PermSize," "TempSize," and "LogBufMB"  了解每个连接的属性。 

举例如下：
加上数据库中PermSize的取值是32G(32768M), TempSize 的取值是4G(4096M)， LogBufMB的取值是1G(1024M),并且Connections的取值是2048. 应用上面的计算公式，该数据库的大小是

	PermSize + TempSize + LogBufMB + 1 + (0.042 * Connections) 
	32768MB + 4096MB + 1024MB + 1  + (0.042 * 2048 ) = 37975 MB

在这个例子中， 设置shmmax和shmall 的方法如下:	
1. 登录root用户，编辑 /etc/sysctl.conf 文件，修改参数 kernel.shmmax和kernel.shmall。 假设数据库的大小是37975MB, 那么shmmax和shmall的取值必须大于这个取值。 针对这个例子，设置shmmax为48G(=511,539,607,552 字节)。 以及shmall 的大小为 56G(= 60129542144 bytes= 58,720,256KB/4 KB page size= 14,680,064 KB pages ); 
	
	# sudo vi /etc/sysctl.conf 
	...
	...
	kernel.shmmax=51539607552
	kernel.shmall=14680064

2. 重新加载 /etc/sysctl.conf 文件
	
	# sudo /sbin/sysctl -p 

3. 运行 Linux 的ipcs -lm 命令查看当前shmmax 以及shmall 参数的取值。 The max seg size (kbytes) is the shmmax value and the max total shared memory (kbytes) is the shmall value. The shmmax value expressed in kbytes is 50331658(= 51,539,607,552 bytes) and the shmall value expressed in kbytes is  58720256 (= 60129542144 bytes)

	% ipcs -lm 
	------ Shared Memory Limits --------
	max number of segments = 4096
	max seg size (kbytes) = 50331648
	max total shared memory (kbytes) = 58720256
	min seg size (bytes) = 1

注意： 
1. 该示例中设置的 shmmax 和shmall 的取值可以在其他应用程序需要的情况下，设置为更多的取值。 
2. 如果你不确定你数据库的大小,你可以设置shmmax和shmall 为物理存储对应的百分比(例如80%)

### 配置HugePages 
为了更加有效的内存管理，你可以设置HugePages参数。 
如果你的共享内存片段大于256G, 你必须配置HugePages。 
一旦配置了HugePages, 你从内存中分配给HugePages 大小的内存大小对于其他用户是不可用的。 与此同时，分配给HugePages的那一部分内存会被自动锁住，不会被交换到磁盘上。 

飞： HugePages是针对 用户进行设置的。 

关于配置HugePages 参数的取值，你需要知道下面的这些内容:
1. 对于数据库而言，共享内存最大的大小是多少
2. 在你的Linux系统上，HugePages 的取值是多少
3. 实例管理员的组Id(group id) 是多少

继续沿用第一章"Configure shmmax and shmall" 中的例子，假设数据库的大小是 37975MB, 并且shmmax 的取值是 48G, 同时上面穿件的用户组 instanceadmin的组Id的值是 10000： 
1. 共享内存片段的大小是 48G
2. HugePages page的大小是 2048kb。 (在不同的平台上，该值是可变动的， 并且不可配置)
	要查看 HugePages page 的大小， 运行 cat /proc/meminfo | grep Hugepagesize 命令

	% cat /proc/meminfo | grep Hugepagesize
	Hugepagesize: 2048 kB

3. 组ID 的取值是： 10000
	要查看实例管理员的group id 的取值，以 instanceadmin 用户登录，并且执行id 命令 

	% id 
	uid=55000(instanceadmin) gid=10000(g10000)groups=10000(g10000)


#### 配置HugePages 
1. 计算HugePages 的个数，通过使用总的共享存储的大小(单位MB) 除以 HugePagesize的大小(单位MB). 在这个示例中，总的共享存储的大小是 48G(=49152MB)，并且Hugepagesize的取值是 2048KB(=2MB): 
	
	49152MB / 2MB = 24576

2.  作为root用户，编辑 /etc/sysctl.conf 文件， 并且将参数 vm.nr_hugepages 的取值设置为之前设置的 HugePages 的取值24576。 并且设置 vm.hugetlb_shm_group 的取值为 实例管理员的group id(示例中是 10000)。 接下来的设置严格控制对用户组中成员对HugePages 的访问。 

	# sudo vi /etc/sysctl.conf
	...
	...
	vm.nr_hugepages=24576
	vm.hugetlb_shm_group=10000

3. 重新加载 /etc/sysctl.conf 文件 
 	#sudo /sbin/sysctl -p 

4. 为了校验你设置的HugePages是否正确，， 运行  cat /proc/meminfo | grep HugePages 命令，查看 HugePages_Total 和 HugePages_Free 的取值是多少 
	
	% cat /proc/meminfo|grep HugePages
	HugePages_Total: 24576
	HugePages_Free: 24576

注意： 
1. 因为HugePages 必须分配连续的可用的存储空间，因此，在下次重启之前,请求分配可能无效，或者仅仅部分生效。 如果主机上有足够的存储空间，那么重启系统来分配全部的HugePages空间。 
2. 如果数据库的大小小于等于256G, 那么不适合设置HugePages 空间。 常规的pages 已经足够使用。 如果数据库大小大于256G， 并且没有设置HugePages，那么数据库无法被加载到内存中。 
3. The TimesTen PL/SQL shared memory segment consumes some of the configured HugePages allocation, determined by the value of the PLSQL_MEMORY_SIZE connection attribute. See "PLSQL_MEMORY_SIZE" in the Oracle TimesTen In-Memory Database Reference for more information
4. HugePages 片段自动被锁，放置内存片段被交换到磁盘中。因此，如果你设置了HugePages ，那么你不需要设置MemoryLock连接属性。 


### 修改memlock设置
位于 /etc/security/limits.conf 文件中的memlock 实体控制着用户可以锁定的存储的大小。 这些实体是基于系统级别设置的，不同于MemoryLock 连接属性的设置。 

If HugePages are configured, the memlock values must be large enough to
accommodate the size of the shared memory segment or the database will not be
loaded into memory. 
如果设置了HugePages,那么memlock 的取值必须足够的来容纳共享存储片段或者未被加载到存储中的数据库。 


举个例子，对于instanceadmin 用户，假设总的共享存储片段的大小是48G(=49152MB), 设置memlock 实体为50331648KB(49152 * 1024)

1. 作为root用户, 编辑 /etc/security/limits.conf 文件，并且设置instanceadmin用户的memlock实体为50331648KB。 该取值意味着instanceadmin用户总的可被锁的存储。 

	# sudo vi /etc/security/limits.conf
	...
	...
	instanceadmin soft memlock 50331648
	instanceadmin hard memlock 50331648

2. 作为instanceadmin 用户, 退出登录，然后重新登录来使修改生效。 

### 修改信号量
TimesTen 对于连接到数据库的连接有一个上限,数据库连接包括如下内容：
1. 用户连接： 通过用户应用程序建立的连接
2. 系统连接： 在TimesTen内部建立的连接(设置为48个连接)	
3. 其他必须的连接: 设置为107个连接

这些连接中的每一个连接都赋予了一个信号量，因此对于数据库连接而言，总的信号量是：
Total semaphores = user connections (N) + system connections (48) +
 other required connections (107)
Total semaphores = N + 155

信号量的设置是在 /etc/sysctl.conf 文件中的 kernel.sem 参数来进行设置的。 
kernel.sem = SEMMSL SEMMNS SEMOPM SEMMNT

其中：
SEMMSL : 表示每个信号量组的最大数量。 该值和数据库的最大连接数相关联，并且是这次讨论中最具有讨论价值的内容。 该值的取值应该是大于155 的一个取值。
SEMMNS is the maximum number of semaphores system wide. Use the formula
SEMMNS = (SEMMNI * SEMMSL) as a guideline. However, in practice, SEMMNS can be
much less than SEMMNI * SEMMSL.
■ SEMOPM is the maximum number of operations for each semop call.
■ SEMMNI is the maximum number of arrays.

按照下面的步骤配置 SEMMSL 和 SEMMNS (确保当前用户是root用户)
查看已存在的内存参数设置
	
	# /sbin/sysctl -a | grop kernel.sem
	kernel.sem = 2500 320000 1000 1280

编辑 /etc/sysctl.conf 文件来修改 semmsl 参数为一个大于155 的连接数. （该值是 kernel.sem 的第一个取值 ）
在这里例子中，为了支持3845个连接(同时打开的连接数), 设置 semmsl 的取值为4000 (155 + 3845)
在这里例子中，剩余的参数将随之增长。 查看你的内核文件了解更多的细节。 
	
	# sudo vi /etc/sysctl.conf 
	...
	...
	kernel.sem = 4000 400000 2000 2560 

重新加载 /etc/sysctl.conf 文件 
	
	# sudo /sbin/sysctl -p 

注意：
如果你使用了副本集，	那么所有机器上面的参数设置都必须相同。 
If you are using replication, the Linux platform for each host on which the master databases reside must have the same kernel settings for shared memory and semaphores. Specifically, SEMMSL must be identical on all hosts that participate in an active standby replication scheme before the duplication is performed.



### AIX prerequisites
在Unix 系统上面，只需要考虑 large pages(大页面)。 信号量(Semaphores) 是由内核动态进行配置的。 
有在具有所需修补程序级别的UNIX主机上， TimesTen classic 可以使用large pages(大页面)。 使用大页面(large pages)将共享片段锁进内存当中。因此它不再需要换页。 用户必须具有CAP_BYPASS_RAC_VMM 以及 CAP_PROPAGATE 功能。 这个功能是通过root用户编辑/etc/security/user 文件进行完成的。 

	# chuser capabilities=CAP_BYPASS_RAC_VMM, CAP_PROPAGATE user_id 

系统默认没有将任何的物理存储锁定到内存中。 使用vmo 命令来配置物理内存池的大小。 下面的例子设置4GB d的内存到大页面物理存储。 

	# vmo -r -o lgpg_regions=256 -o lgpg_size=19777216 


## Planning the installation and its deployment 
计划TimesTen 的安装以及部署
关于计划的目录，这一部分调理这些内容
1. 数据库文件以及用户文件的路径
2. 数据库以及应用的路径

### 数据库文件以及用户文件的路径
意识到这些TimesTen的先决条件之后，考虑一下数据库以及其他用户文件的位置。 
1. 在TimesTen 的安装路径下是不允许存储任何额数据库文件(包括检查点以及日志文件)以及用户文件的。 TimesTen的安装路径下的内容是一成不变的--不会增加，改变或者删除。 
2. 强烈建议不要在实例的home目录下存在数据库文件获取其他的用户文件。 当实例删除的时候，实例home目录下的文件都会被删除。 
3. 处于性能考虑, 建议将TimesTen的检查点文件和事务的日志文件保存到不同的路径下。 检查点文件保存在数据库定义的DataStore 位置。 事务的日志文件保存在数据库定义的 LogDir 路径下。 

一旦你完成了数据库的安装，你就可以估算你的数据库以及必要磁盘的大小了。 参考《Oracle TimesTen
In-Memory Database Operations Guide》中的"Ensuring sufficient disk space"了解相关的细节。 

###数据库以及应用的位置
思考： 
1. 除非你考虑你的应用程序和TimesTen Classic 之间对资源的争夺，否则的话，最好将你的应用程序和TimesTen 数据库放置在同一个主机上。 这样可以允许程序采用直接连接。 由于没有了网络往返时间，直接连接具有更好的响应时间以及相比客户方/服务端 更好的吞吐量。 
2. 为了使用TimsTen Cache, 最好将Oracle 和TimesTen Classic 安装在不同的主机上。 避免二者资源的连接。 



## Environment variale 
这一章节讨论环境变量
* 为TimesTen 设置环境变量
* 环境变量的描述

### 为TimesTen 设置环境变量
在某个终端窗口设置环境变量，可以确保在该窗口中为某些特定的实例执行命令。 下面有一系列你需要设置的环境变量。 
* 在你创建实例之后需要创建的环境变量
* 使用TimesTen 工具之前需要创建的环境变量
* 在你主机运行实例的时候，以direct mode 运行模式的时候需要设置的环境变量
* 在主机上运行客户端服务器端应用的时候，需要设置的环境变量

在Linux和UNIX系统上， 你可以通过执行ttenv 脚本(ttenv.sh 或者 ttenv.csh) 来设置环境变量。 在Windows 系统上，你可以通过运行 ttenv.bat 批处理文件来设置环境变量。  TimesTen 在你创建好实例之后，就会创建该脚本。 

在TimesTen classic 环境下， 这些脚本位于timesTen 实例的home目录下的 /bin 目录下。 
通过执行这些脚本, 相关实例所需的环境变量将会被设置。 
这些环境变量包括： TIMESTEN_HOME, PATH, LD_LIBRARY_PATH（或者等量的环境变量）以及 TNS_ADMIN. 

例如： 
针对 Bourne 类型的shell。 例如 sh，bash， zsh 或者ksh 

	% cd timesten_home/bin 
	% ./ttenv.sh 

针对 csh 或 tcsh 脚本

	% cd timesten_home/bin 
	% source ttenv.csh 

一旦设置了TIMESTEN_HOME 环境变量之后,实例的home目录就已知了。 TimesTen 将会根据配置文件 timesten_home/conf/timesten.conf 进行其他的设置，例如 daemon 端口。 

注意： 
执行ttenv 脚本输出的环境变量中有些参数可能不会立即生效。 


还有其他方式来设置环境变量：
在 命令行模式下执行 ttenv 命令来重启一个新的shell，然后设置环境变量， 并且执行特定的命令。 例如执行 ttIsql 来连接database1 

	% cd timesten_home/bin 
	% ./ ttenv ttIsql database1 

环境变量将仅仅在你的 ttIsql会话中有效，并且，你将在 ttIsql 提示符下工作。 一旦你退出来ttIsql， 你的shell 将会恢复它原来的环境变量设置。 

对于windows平台而言, 在DOS 窗口执行 ttenv.bat 批处理文件， 将会在DOS 会话中改变相关的环境变量。 例如

	C:\TimesTen\tt181_64\instance\bin>ttenv

注意： 
1. 在windows 平台，实例的home目录，path  ，classpath，library paht， 以及path是在安装的过程中被设置的。 
These settings are reflected in the System control panel and persist between sessions. It is not necessary to run ttenv.bat in this case.

2. ttenv 命令行模式不适用于windows平台。 


### 环境变量的描述
这一章节提供了关于环境变量更多的细节
* TIMESTEN_HOME 环境变量
* NSL_LANG 环境变量
* Shared library path 环境变量
* PATH 环境变量
* Temporaty directory 环境变量
* TNS_ADMIN 环境变量
* Java 环境变量
* SYSODBCINI 环境变量
* ODBCINI 环境变量
* SYSTTCONNECTINIT环境变量





