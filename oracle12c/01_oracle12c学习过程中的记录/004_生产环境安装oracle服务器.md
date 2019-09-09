生产环境安装oracle服务器

生产上一般包括系统服务器，光纤存储交换器，存储器 
	
生产上的服务器最低配置是16G内存，8颗CPU,一个服务器至少应该有两个硬盘，做RAD1 磁盘冗余。 存储一般使用IBM,惠普的存储(这里的存储是独立于系统服务器的存储，是通过和光纤存储交换机和服务器相互连接的独立存储)，比较好的存储是EMC存储。 

在实际生产上的硬件配置一般是： IBM的光纤存储交换机，ESC的独立存储，服务器上的硬盘必须是ISIC 硬盘。 
作为DBA必须要提前将自己对服务器的要求告诉相关的采购人员。 

检查系统要求 
* 足够的临时空间
* 64位和32位问题
* 检查操作系统(OS)是否正确
* OS补丁程序级别
* 系统程序包
* 系统和内核参数
* X Server 权限 
* 足够的交换空间
* ORACLE_HOME 非空

 操作系统必须选择 64位的Linux。(硬件架构CPU 64位，linux操作系统64位，oracle版本64位)


 灵活体系结构(OFA)
 OFA设计用于：
 * 组织大量软件
 * 简化常规管理任务
 * 在多个ORACLE 数据库之间实现轻松切换
 * 相应地管理数据库扩展
 * 帮助消除空闲空间碎片

 ORACLE软件安装在哪个目录下面都是有标准的(为了便于管理和交流，使用这些标准目录对软件进行相关的安装)


 灵活体系结构(OFA)
 	OFA 是一种用于配置Oracle数据库和其它数据库的方法。 OFA利用OS和磁盘子系统的功能创建易于管理的配置，这样在数据库得到扩且性能要求更高时，可以提供最大程度的灵活性。 
 OFA设计用于：
 	对磁盘上的大量复杂软件和数据进行组织，以避免出现设备瓶颈和性能较差的情况。 

## 使用灵活体系结构
* 命名装载点 
	- /u01
	- /disk01
* 命名目录：
	- /u01/app/oracle
	- /u01/app/applmgr 
* 命名文件
 	- 控制文件： controln.ctl
 	- 重做日志文件： redon.log 
 	- 数据文件： tn.dbf

使用灵活体系结构
OFA 的核心位置有一个命名方案，它提供的标准可应用于装载点(通常为物理磁盘)，这些装载点上的目录和子目录，最后可应用到文件本身。 
装载点语法：
主目录语法：
软件目录语法：


##设置oracle的环境变量
ORACLE_BASE: OFA的Oracle 目录结构基础 
ORACLE_HOME: 包含Oracle软件的目录
ORACLE_SID: 初始化实例名称(默认值为orcl)
NLS_LANG:语言，地区和客户机字符集设置

设置环境变量：
Oracle环境变量有很多，此处提到的环境比那里是成功安装，使用oracle数据库的关键变量。虽然这些环境变量不需要进行设置，但是如果能在安装之前对其进行设置，则可避免将来发生的很多问题。 
ORACLE_BASE: 指定OFA的oracle 目录结构基础。该变量为可选项，如果选择使用它，则课简化日后的安装和升级操作。 他是一个目录路径. 

## 高级安装选项 
1. 数据库存储选项
	- 文件系统
	- Automatic Storage Management 
	- 裸设备
2. 数据库管理选项 
	- Enterprise Manager Grid Control 
	- Enterprise Manager Database Control 
3. 数据库备份和恢复选项
4. 电子邮件通知选项
5. 集群就绪服务
6. 克隆 

(在生产上，数据库存储一般是裸设备或者ASM,且ASM 现在正在逐步超越裸设备)


当物理内存小于4G的时候，Swap 空间的大小应该是物理内存的2倍，当物理内存大于等于4G的时候，Swap 空间的大小应该和物理内存一样大。 





在学习环境中，oracle安装的根目录一般设置为20G-30G，物理内存至少一个G，Swap空间至少二个G，且交换空间，不必要单独一个磁盘。 


生产上安装oracle数据库需要执行的命令：
1. 查看交换空间多大 
$ grep SwapTotal /proc/meminfo 
2. 查看内存有多大 
$ grep MemTotal /proc/meminfo 
3. 查看系统上空闲磁盘的大小
$ df -k 
4. 查看软件可以运行的体系结构 
$ grep "model name" /proc/cpuinfo 


 网络相关的修改：
 1. 修改网络地址   # vi /etc/sysconfig/network-script/ifcfg-eth0 
 2. 修改地址映射关系 	# vi  /etc/hosts    ip地址 	主机名 
 通过 hostname 命令查看主机名 


 创建相关的用户和组：
 先创建用户组：
 # groupadd oinstall
 # groupadd dba 
 在创建用户
 # useradd -g oinstall -G dba oracle 
 这里useradd 命令的-g 命令指定用户的主组，-G 表示用户还属于其它哪些组 



 修改linux系统的内核参数：
 修改 /etc/sysctl.conf 文件
 其中，kernel.shmmax的取值一般是物理内存的一般，在生产上的要求是大于等于物理内存的一半。 

 内核参数配置好之后，不需要重启，只要通过 sysctl -p 进行检查，并让其生效。 


 设置linux系统对oracle用户资源访问的限制：
 修改 /etc/security/limits.conf 

 	oracle		soft	nproc	2047
 	oracle		hard 	nproc	16384
 	oracle 		soft	nofile	1024
 	oracle 		hard 	nofile  65536 
 其中前两个是控制oracle用户可以打开的进程数，后面两个是oracle用户可以打开的文件个数。 


 修改 /etc/pam.d/login 文件  
 session 	required 	pam_limits.so 


 创建相关的目录
 #mkdir /u01/app/oracle -p 
 #chown -R oracle:oinstall /u01
 #chmod -R 755 /u01

设置oracle用户的环境变量
 su -oracle   切换到oracle用户
修改.bash_profile
export ORACLE_BASE=/u01/app/oracle
export ORACLE_HOME=/u01/app/oracle/product/10.2.0/db_1
export ORACLE_SID=jiagulun
export NLS_LANG=american_america.zhs16gbk




