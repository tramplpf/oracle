# What's New 
这一部分总结了Oralce 内存数据库TimesTen (Release 18.1) 的新的特性。 同时它也提供了关于更多信息的连接。 

## New features in Release 18.1.2.1.0
1. 这本书仅仅针对 TimesTen Classic 数据库。 要获取关于TimesTen Scaleout 数据库的信息，请查看 
《Oracle TimesTen In-Memrory Database Scaleout User's Guide》 一书中的 
"Prerequstes and Installation of TimesTen Scaleout" 章节。 
2. 从数据库安装到实例创建Teimesten 18.1 相对之前版本都有所改变。 
查看 "Overview of installations and instances" 获取更多信息
3. 查看"Installation and instance management on Linux/UNIX" 来获取在 
"Linux/Unix 安装以及实例管理的概括信息"。 同时可以查看 "Charter 2, Installation and TimesTen Classic on Linux/UNIX" 
来获取 "在安装和实例中获取程序调用"的信息。 
4. 查看 "Installation and instance management on Windows" 以及 "Overview of the installation precess on Windows" 
来检索在window上面安装的过程
5. 下面的表格概括了 在linux/Unix 上面安装 18.1.2.1.0 版本和之前版本 TimesTen Classic 之间的区别

安装项和进程			18.1.2.1.0 Release 		    						Previous release
安装包				 单一安装包											Client-only 以及 Data-Manager 
安装  				 安装包文件解压缩得到的文件							通过允许安装器(installer) 一次性完成安装以及实例进程的创建。 
实例					运行 ttInstanceCreate 工具创建的后台进程的集合      	通过运行安装器(installer) 一次性完成安装和实例的创建。 
创建一个安装			 解压缩安装包											解压缩安装包并且运行安装器
创建一个实例			 运行 ttInstanceCreate工具 							作为安装进程的一部分 
修改实例				 运行 ttInstanceModify工具							运行 ttmodinstall 工具
删除实例				 运行 ttInstanceDelete工具   						运行安装程序的时候，添加 -uninstall 选项 来删除实例以及安装。 
删除安装			     手动删除安装即可										运行安装程序的时候，添加 -uninstall 选项 来删除实例以及安装。 
/info 目录			 /info 目录被分为 /conf, /diag, /info 三个目录 		只有/info 目录	 					
TimesTen 后台配置文件 /conf/timesten.conf                                /info/ttdaemon.options 
PL/SQL 				 包含在安装包中，解压之后作为安装进程的一部分			可以在安装的时候忽略
											

18.1.2.1.0.Release 版本中/info 目录介绍
在18.1.2.1.0.Release 版本中 /info 目录包括/conf, /diag, /info 三个目录
/conf 实例管理员可以修改的配置文件
/diag 包含对话框输出的文件
/info 实例管理员不能修改或者测试的文件



在window上面的安装进程没有改变。 每次安装只有一个实例并且实例会在安装过程中自动创建。 该实例是仅客户端的。 