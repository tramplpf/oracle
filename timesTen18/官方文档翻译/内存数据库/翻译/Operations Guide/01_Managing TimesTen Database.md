# 管理TimesTen数据库

一个TimesTen 数据库是由表，视图，以及序列等一系列的对象组成的集合。 你可以通过SQL 语句来访问以及操控TimesTen 数据库。 如果你的数据库不存在，当实例管理员连接连接到数据库的时候，TimesTen 根据特殊的属性来创建该数据库。 你可以通过断开和TimesTen 数据库连接的所有连接来释放数据库占用的存储片段。 

这一章首先描述了如何配置TimesTen数据库的连接， 因为你对数据库的配置和管理包含在连接定义当中。

一旦你创建了数据库，你可以执行下面的操作
* 使用ttIsql工具来连接数据库从而执行sql文件或者开始一个交互式SQL会话。 查看第五章的"Batch mode vs interactive mode" 了解更多的信息。 

* 执行一个使用该数据库的应用。

这一章节的内容包括如下的内容： 
* 使用ODBC 或者JDBC 连接TimesTen数据库
* 指定数据源名称来标识TimesTen数据库
* 定义数据管理DSN 
* 定义客户端以及服务器DSNs
* 解析DNS 路径
* DNS示例
* 使用连接字符串连接数据库
* 指定内存策略
* 从存储从加载以及卸载数据
* 和数据库断开连接
* 指定数据库的大小
* 管理数据库中已存在的表
* 使用ttBulkCp工具
* TimesTen 的线程工具
* TimesTen的碎片整理
* 验证你的数据库是单实例还是分布式数据库



## 使用ODBC 或者JDBC 连接TimesTen数据库
正如《 Oracle TimesTen In-Memory Database Introduction》中"TimesTen connection options" 中所描述的，应用程序使用TimesTen ODBC驱动来访问TimesTen数据库。 应用程序使用ODBC 直接驱动，ODBC 客户端驱动， 或者是 ODBC驱动管理来连接数据库。 

Figure 1-1 展示了一个应用程序可以使用不同的驱动和接口来访问TimesTen数据库。 

飞： 从图中，可以看到TimesTen数据库包含两个驱动，一个是SQL engine 另一个是PL/SQL engine. 


* Java 应用程序通过加装JDBC 库俩和TimesTen数据句酷交互

考虑下面的场景：
* 一个应用程序通过TimesTen ODBC驱动直接和数据库连接，无论它是通过直接驱动还是客户端驱动， 它仅仅可以使用它所连接的驱动。 一个应用程序直接连接到TimesTen 的ODBC 驱动可以在同一时间连接到多个数据库。 TimesTen 直接驱动或者客户端驱动支持到多个数据库的多个连接。 
注意： 这种方式，提供了较少的灵活性，但是相比于通过驱动管理器提供了更好的性能。 

* 在一个应用程序中，可以通过多个TimesTen ODBC 驱动来连接到TimesTen 数据库。即时这些驱动连接到不同的数据库。 如果一个应用程序加载多余一个的TimesTen ODBC驱动， 那么应用程序必须使用驱动管理器.例如Windows ODBC驱动管理器。 
如果一个应用程序同时想要使用TimesTen的直接连接和TimesTen 的客户端驱动连接，那么应用程序需要连接多个驱动。 Windows 的ODBC驱动管理器在运行的时候，动态加载一个ODBC驱动。 然而，必须谨慎的评估使用ODBC驱动管理器的好处，因为他会影响应用程序的执行性能。 

注意： 
一个应用程序使用ODBC驱动管理器之后不能使用XLA. 

要了解更多的关于如何编译应用程序的信息查看《 Oracle TimesTen In-Memory Database C Developer's Guide》中的"Compiling and linking applications" 和 《 Oracle TimesTen In-Memory Database Java Developer's Guide》中的"Compiling Java applications" 以及 《Oracle TimesTen In-Memory Database TTClasses Guide》 中的 "Compiling and linking applications". 


下面的部分描述了 如何定义TimesTen 数据库
* 使用TimesTen 的ODBC驱动如何连接数据库
* 使用TimesTen 的JDBC驱动 和驱动管理器如何连接数据库

### 使用TimesTen 的ODBC驱动如何连接数据库
TimesTen 包括下面的集中TimesTen 驱动器
* TimesTen Data Manager driver: 这对直连应用的TimesTen ODBC驱动程序。 
* TimesTen Client driver ： 使用客户端/服务器端模式连接的ODBC 驱动器。 

TimesTen 包括下面两个版本的Data Manager ODBC 驱动
Production: 在生产和大部分的开发中使用production 版本的TimesTen 数据管理驱动。 
Debug:  只有在你使用TimesTen数据库的过程中遇到了问题，才会使用debug 版本的数据管理启动。 该版本执行额外的内部错误检查并且比production 版本的要慢。 在Linux和Unix 平台， TimesTen 调试库是通过-g 来展示更多的调试信息。 

对于TimesTen classic 在windows 平台的支持， 默认安装的是product 版本的驱动。 为了安装debug版本的驱动， 选择 Custom 步骤。 为了安装TimesTen 客户端驱动，也需要选择Typical 或者 Custome setup。 



Table 1-1 在windows 平台上面提供的ODBC驱动的类型

在Linux 和Unix 平台上，依赖于安装过程中的选择， TimesTen 可能安装Client driver以及 product 版本和debug 版本的TimesTen 数据管理ODBC驱动。 

Table 1-2 展示了在Linux 和Unix 平台上TimesTen ODBC的驱动类型 



### 使用TimesTen 的JDBC驱动 和驱动管理器如何连接数据库

JDBC 可以让Java 应用程序发送SQL语句到TimesTen 数据库并且处理返回的结果。 在java 程序语言中，它是主要的数据访问接口。  当TimesTen 安装之后，JDBC 将会和TimesTen 的数据管理器一起被安装。 


正如Figure 1-1中所描述的，TimesTen 的JDBC 驱动是通过ODBC 驱动来访问TimesTen 数据库的。 对于每一个JDBC 方法， 驱动执行一系列的ODBC 功能来执行恰当的操作。 因为JDBC的所有操作都依赖于ODBC驱动， 因此使用JDBC的第一步就是定义TimesTen 数据库以及ODBC 驱动来访问JDBC代码的数据库。 

The TimesTen JDBC API is implemented using native methods to bridge to the
TimesTen native API and provides a driver manager that can support multiple drivers
connecting to separate databases. 
...

位于DriverManager类中的JDBC 的驱动管理器跟踪java应用程序可以加载的所有的JDBC驱动。 java 应用程序可能加载一些驱动并且独立的访问这些驱动。 例如， TimesTen Client JDBC 驱动以及 TimesTen direct driver 可以被一个应用程序加载。 然后，java应用程序可以通过本地系统或者远程系统来访问数据库。 

可以通过查看《 Oracle TimesTen In-Memory Database Java Developer's Guide》 中的"Support for interfaces in
the java.sql package" 获得一系列的TimesTen 支持的Java 程序。 

## 指定数据源名称来标识TimesTen数据库
当你从一个应用程序连接到TimesTen数据库的时候，你使用一个数据源名称(Data Source Name, DSN) 来唯一便是一个你想要连接指定的TimesTen 数据库。 一个DSN 是一个字符串名字用来标识TimesTen 数据库，并且一系列的连接属性在你连接数据库的时候，都会生效。  在Windows 平台，DSN 同样指定了ODBC 驱动来访问数据库。 


你可以定义一个默认都的DSN,这样，当一个用户或者应用程序在没有指定DSN的情况下，或者没有在odbc.ini 文件中定义该DSN的时候，作为默认的连接。  查看第一章的 "Setting up a default DSN". 

注意： 
如果一个用户试图使用一个它们没有权限的有连接属性的DSN 连接符的时候，例如first connection attributes， 它们将会啊收到一个错误。 查看《 Oracle TimesTen In-Memory Database Reference》 中的"Connection Attributes" 了解关于 first connection attribute privileges 的信息。 



尽管一个DSN 唯一标识了TimesTen数据库，但是一个数据库却可以使用多个DSN 来定义。 这些不同的DSN 可以具有不同的连接属性。 这种便利，为一个数据库配置多个不同的连接描述符提供了便利。 

注意：
根据ODBC 标准， 当一个属性在连接字符串中出现多次的时候，使用第一次出现的取值，而不是最后一次的取值。 

一个DNS 包含如下的字符:
* 它的最大长度是32个字符
* 它是大小写不敏感的。 (不区分大小写)
* 它是由除了 () [] {} , ; ? * = ! @ \ / 的ASCII 字符组成的。 
* TimsTen 不建议使用空格作为DSN 的一部分。 如果一个DSN 包含空格，那么TimesTen 的一些工具会从空格处对DSN 进行截取。 除此之外，DSN 也不能以空格开头或者结尾。 DSN 也不能只有空格组成。 

羡慕的章节描述了如何配置和管理你的DSNs
* 用户和系统DSNs
* 定义直连或者客户端/服务器端连接的DSN 
* 对于Data Manager DSN 或者 server DSN 的连接属性

### 用户级和系统级额DSN的概览
使用两层的命名系统来对DSN 进行解析,第一层解析用户DSN ,第二次解析系统DSN. 
* 用户级别的DSN 只能被 创建该DNS的用户来使用
	在Windows 系统，用户DSNs 定义在 ODBC Data Source Administrator 中。 (On Windows, user DSNs are defined from the User DSN tab of the ODBC Data Source Administrator. )

	在Linux 和Unix 平台上， 在odbc.ini 文件中定义用户DSN. 如果定义了ODBCINI 环境变量,那么TimesTen 将该文件放置在ODBCINI 环境变量定义的位置处，如果没有定义ODBCINI环境变量，TimesTen 默认将该文件放置在 $HOME/.odbc.ini

尽管一个用户DSN 对于创建该DSN 的用户是私有的， 但是它仅仅是一个DSN, 一个由 字符串名字以及他的属性组成的字符串，仅仅是DSN 是私有的，它所执行的数据库并不是私有的。 它所指向的DSN 可以被其他用户的 user DSN 获取被系统DSNs 来指向。 

TimesTen 同时支持TimesTen Data Manager 和TimesTen client 在 .odbc.ini 文件中定义的数据源。 


* 系统级别的DSN 可以被该系统上面的所有用户所使用。 系统级别的DSN 用来连接TimesTen 数据看看。 
	在Windows 系统中，系统级别的DSN 被定义在 ODBC DataSource Administartor 的System dsn 的tab 页。( system DSNs are defined from the System DSN tab of the ODBC Data Source Administrator) 

	在Linux/Unix 平台，系统级别的DSN 定义在sys.odbc.ini 文件中， 该文件参考系统 odbc.ini 文件。 TimesTen 加载系统DSN 文件按照如下的顺序。 
	1. 如果SYSODBCINI 环境变量被设置的话，会位于该环境变量所在位置。 
	2. 在一个非root安装中， 该文件位于 timesten_home/conf/sys.odbc.ini . 在一个root安装中， 该文件位于 /var/TimesTen/InstanceName/sys.odbc.ini
	3. 如果既没有好的root，也没有找到非root 位置， TimesTen 在 /var/TimesTen/sys.odbc.ini 文件中查询系统级DSN. 
	4. 如果在上面的其他位置都没有找到 system DSN ,那么TimesTen 将会在 /etc/odbc.ini 文件中查询。 

### 定义一个DSN 来进行直接连接或者客户端和服务器端连接
DSNs 创建出来是为了唯一标识一个数据库， 而不关心该数据库是本地的还是远程的。 下面的内容解释了 DSN 进行直连或者客户端服务器端连接的内容：
 * Data Manager DSN : 该类型的DSN 指定了一个使用 TimesTen Data Manager ODBC 驱动的本地数据库。 该DSN 采用的是直连驱动。 你可以在TimesTen 的Data Manager driver 中使用product 版本或者 debug 版本的驱动。 
  一个 Data Manager DSN 指向一个使用路径名和文件名前缀组成执行的数据库。 该数据库路径名指定了数据库的位置以及数据库的前缀。 例如  C:\data\chns\AdminDS or /home/chns/AdminDS. 

注意： 
这里的路径名和前缀没有定义文件名，但是路径的名称表示了数据库的位置以及所有数据库文件的前缀。 被数据库准确使用的文件名是包含前缀的例如：  C:\data\chns\AdminDS.ds0 or /home/chns/AdminDS.log2. 

一个数据管理DSN所指向的数据库必须必须和该系统位于同一个主机上。 如果多个Data Manager DSNs 指向相同的数据库， 它们必须全部使用准确的数据库路径名。 及时一些其他的路径名也指向相同的位置(比如软连接)。 例如， 在一个DSN 定义中，你不能使用一个符号链接来执行该数据库，然后使用在另一个DSN 中，使用准确的路径名来指向相同的数据库。 在Windows系统上，你不能通过使用驱动映射符来表示数据库路径。 

 * Client DSN :  一个客户端DSN 指定了一个使用TimesTen client 驱动连接的远程的数据库. 客户端DSN 通过指定主机名(hostname) 和 NDS 来唯一标识一个数据库。 一个主机名标识TimesTen 服务器端运行的系统。 一个DSN 指向一个服务级别的DSN(server DSN)。 该server dsn 指向了服务器主机上面的一个TiemsTen 数据库。 
 

 * Server DSN : 一个server DSN 通常是被定义为一个系统级别的DSN, 并且为客户端可以访问到的位于服务器端的数据库所指向。 
 服务端DSN 的格式和属性和Data Manager DSN 的格式和属性和相似。 

 在Linxu和UNIX 系统中，所有的用户级DSNs 包括由特殊用户在odbc.ini文件中创建的Client DSNs以及Data Manager DSNs。 同样的所有的系统级别的DSNs定义在系统级别的 odbc.ini 配置文件中。 

 下面的表格展示了TimesTen所支持的DSN的类型，以及它们是属于user DSNs 还是 system DSNs。 以及这些DSNs的保存位置

 DSN type | User or System DSN ? | Location of DSN 
 - | :-: | -:
 Date Manager DSN | Can be a user or system DSN | Located on the system where the database resides 
 Client DSN | Can be a user or system DSN | Located on any local or remote system
 Server DSN | Must be a system DSN | Located on the system where the database resides 

 要了解关于Client DSNs 和server DSNs 的信息，查看第二章的 "Working with the TimesTen Client and Server"



### Data Manager DSNs 和 server DSNs 的连接属性
有四种类型的TimesTen Data Manager DSN 以及 server DSN 属性： 

注意： 
查看《Oracle TimesTen In-Memory Database Reference》 中的"Connection Attributes" 了解关于所有连接属性的更多信息。 

* Data Store attributes 是在数据库创建的时候，和数据库建立连接的，并且不能被后续连接修改。 它们只能通过删除数据库，并且重建数据库的时候改变。 

下面是主要的公共的存储属性:
	1. DataStore： 数据库的路径名以及文件名的前缀。 
	2. LogDir： 数据库事务日志文件的路径名，将事务日志文件和检查点文件放置在不同的磁盘上，可以提供系统的性能。 
	3. DatabaseCharacterSet： 定义存储编码必要的字符集。 

* First connection attributes： 当TimesTen 数据库被加载到内存中的时候，first connection attributes 属性将会被使用。 只有实例管理员可以使用first connection attributes 来加载数据库。 默认情况下， 在没有连接的情况下，TimesTen 会加载一个空的数据库，当第一个连接建立的时候，加载数据到内存中。 这些属性对于后续的所有连接全部有效直到最后一个连接和数据库断开连接。  只有当数据库处于未加载状态，数据库的First connection attributes 才可以被修改。 之后，实例管理员使用不同的连接属性进行第一次连接。  

下面是关于first connection attributes 的主要的公共属性：
	1. PermSize : 配置数据库持久化存储区域的大小。 持久化存储区域包括持久化数据库对象。 TimesTen 只有当一个检查点操作的时候，才会写入持久化区域数据到磁盘。 
	2. TempSize： 配置数据库的临时存储区域所分配的大小。 临时存储区域包括执行语句时生成的短暂的数据。 

注意： 
你的系统必须具有足够的主存储来容纳整个的数据库。 查看第一章的 "Specifying the size of a database" 了解更多的信息。 

* General connection attributes： 该属性可以被每一个连接所定义， 并且在连接期间保持持久化。 每一个连接针对该属性可以有不同的取值。 

注意: 
如果你在连接字符串中提供了一些连接属性，那么该属性的取值将会覆盖DSN 中的属性。  查看第一章的 "Connecting to a database using a connection string" 了解更多的信息。 

下面是关于General connection attributes 的一些公共属性： 
	1. UID: 该属性指定将要连接到数据库的用户名。 无论采用直连，还是客户端/服务器连接模式，作为实例管理员或者作为的外部的用户(external user), 你都不需要指定用户名。 当你指定一个用户名的时候，TimesTen 假设 UID 是系统标识用户名的标识。 
	2. PWD: 该参数为指定UID 设置相应的密码。对于内部用户，如果你没有在odbc.ini 文件中为特定的DSN指定PWD属性的取值，也没有在连接字符串中指定特定的取值。 TimesTen 会给出提示询问密码。 对于外部用户， 你不需要为UID 指定密码，因为它是通过操作系统认证的。 
	当你初始化 客户端/服务端 连接的时候，密码会被 客户端服务器协议进行加密传输。 
	3. PWDCrypt: 为UID 设置加密后的密码 。

* TimesTen Cache attributes： 允许你为TimesTen 加载数据的源数据库设置Oracle Service Identifier(oracle
服务标识符)、 

在Windows 系统中，你在ODBC Data Source Administrator 中指定这些属性。 
在Linux/UNIX 中， 你在odbc.ini 文件中指定属性。 如果在odbc.ini 文件中没有指定相关的属性，那么使用默认值。 


## 定义数据管理DSN 
下面的章节展示了如何在不同的平台上面创建 Data Manager DSN . 
* 在Windows 平台创建 Data Manager DSN 
* 在 Linux/UNIX 平台上创建 Data Manager DSN

### 在Windows 平台创建 Data Manager DSN 
（未完成）

### 在 Linux/UNIX 平台上创建 Data Manager DSN
下面的章节包含下面的内容
* 创建一个用户级别或者系统级别的 odbc.ini 文件
* 在数据库路径名中使用环境变量


#### 创建一个用户级别或者系统级别的 odbc.ini 文件
在Linux/UNIX 平台上， 用户级别的DSNs 是被定义在$HOME/.odbc.ini 文件或者 通过ODBCINI 环境变量定义的文件中。 该文件被称为用户级别的 odbc.ini 文件。  系统级别的DSNs 被定义在系统 odbc.ini 文件中， 该文件位于timesten_home/conf/sys.odbc.ini 

用户级别的DSN 和系统级别的DSN 的语法是一样的。  可以查看第一章的 "odbc.ini  file entry descriptions" 了解相关的语法。 系统级别的odbc.ini 是在TimesTen 数据库安装的时候被创建的。 用户必须创建他们自己的用户级别的 odbc.ini 文件。 

执行下面的命令来创建DSN:
1. 在odbc.ini 文件中指定DSN. DSN 定义在一个方括号里面。 The DSN appears inside square brackets at
the top of the DSN definition on a line by itself. For example:
[AdminDS]

2. 指定TimesTen的ODBC驱动
注意：
	JDBC用户需要指定TimesTen 的ODBC 驱动 以便使用JDBC 驱动。 
为了设置ODBC驱动，在odbc.ini 文件中指定驱动属性。 下面的例子提供了一个示例：
[AdminDS]
Driver=timesten_home/lib/libtten.so

3. 在odbc.ini 文件中，指定数据库路径以及前缀。 下面的示例中 /users/robin作为数据库的文件路径， FixedDs作为数据库文件的前缀。 
DataStore=/users/robin/FixedDs

这里的舒陆军路径可以使用环境变量。 查看第一章的 "Using environment variable in database path names" 了解相关的信息。 

4. 选择数据库字符集。 下面的例子在odbc.ini 文件中定义数据库字符集为AL32UTF8. 
DatabaseCharacterSet=AL32UTF8

5. 在odbc.ini 文件中设置连接属性。 如果没有在odbc.ini 文件中设置的连接属性，将会采用默认值。 


#### 在数据库路径名中使用环境变量
你可以在指定数据库路径名和事务日志名的时候，使用环境变量, 例如，你可以指定 $HOME/AdminDS 来表示数据库的位置
环境变量也可以通过 $varname 或者 $(varname) 来表示。 这里括号是可选的。  在数据库路径中一个反斜线(\) 分隔下一个字符。 



## 定义客户端以及服务器DSNs
## 解析DNS 路径
## DNS示例
## 使用连接字符串连接数据库
## 指定内存策略
## 从存储从加载以及卸载数据
## 和数据库断开连接
## 指定数据库的大小
## 管理数据库中已存在的表
## 使用ttBulkCp工具
## TimesTen 的线程工具
## TimesTen的碎片整理
## 验证你的数据库是单实例还是分布式数据库
