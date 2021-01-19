# 在Linux或者UNIX 系统上安装TimesTen classic

## 在Linux/UNIX 系统上创建一个安装


### Create an installation accessible by the instance administrator''s primary group 
创建一个安装，可被实例管理员所在组的用户可以访问

1. 将相关的发行版本放在预期的可访问的路径下
2. 为安装创建必要(期望)的路径
3. 切换到安装期望的路径
4. 解压缩发行版本到期望的路径

在下面实例中， 用户ttuser1 的主group 是timesten,在 fullinstall 路径下创建的一个全安装路径， 这个安装可以被timesten组的所有成员访问。 

	% mkdir fullinstall
	% cd fullinstall 
	% unzip /swdir/TimesTen/ttinstallers/timesten181210.server.linux8664.zip

安装路径的顶级目录是 tt18.1.2.1.0
例如，在fullinstall 路径下创建路径
dr-xr-x--- 19 ttuser1 timesten 4096 Mar 2 22:07 tt18.1.2.1.0

tt18.1.2.1.0 路径包含如下的文件：

dr-xr-x--- 5 ttuser1 timesten 4096 Mar 2 22:07 3rdparty
dr-xr-x--- 2 ttuser1 timesten 4096 Mar 2 22:07 bin
dr-xr-x--- 3 ttuser1 timesten 4096 Mar 2 22:07 include
dr-xr-x--- 2 ttuser1 timesten 4096 Mar 2 22:07 info
dr-xr-x--- 2 ttuser1 timesten 4096 Mar 2 22:07 lib
dr-xr-x--- 8 ttuser1 timesten 4096 Mar 2 22:07 plsql
dr-xr-x--- 3 ttuser1 timesten 4096 Mar 2 22:07 ttoracle_home

timesten 的成员可以访问该实例，非timesten 组的用户不能访问该安装。 也就不能通过该安装来创建实例。 



### Creating an instance on Linux/UNIX : Basics 
在Linux/UNIX 上面创建一个实例

#### 创建一个全实例安装 (Create a TimesTen full instance)
这个例子使用 ttInstanceCreate 工具来创建一个全实例。在命令行中没有指定其他的参数。 

	% installation_dir/tt18.1.2.1.0/bin/ttInstanceCreate


