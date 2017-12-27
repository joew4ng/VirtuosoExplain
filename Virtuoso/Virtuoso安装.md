# Virtuoso 数据库安装

## Virtuoso 数据库 在 Windows上安装
1. 下载virtuoso pre-built版本
2. 运行6.1.4或者版本之上，需要[Microsoft Visual C++ 2010 Redistributable Package (x64)](http://www.microsoft.com/en-us/download/details.aspx?id=30679#)（如果没有安装，请必须首先安装）
3. 环境配置
- 将下载后的压缩包解压，放在C盘目录下，地址可按照 C:/Program Files/OpenLink Software/VOS7/
- 添加环境变量（计算机=》属性=》高级设置=》环境变量(系统环境变量)）新建变量 VIRTUOSO_HOME 值为：C:/Program Files/OpenLink Software/VOS7/virtuoso-opensource/   (注意目录名称根据自己的命名变化)
- 在系统环境变量PATH中将该变量添加进去(命令行能调用)  
> ;%VIRTUOSO_HOME%/bin;%VIRTUOSO_HOME%/lib
- 在virtuoso-opensource目录下的 database子目录下新建 php.ini配置文件 内容为:
> http://ftp://download.openlinksw.com/support/vos/php.ini
- 创建virtuoso的windows服务:
  1. 使用**管理员模式**打开cmd/dos窗口,输入测试命令为下，如果成功为显示该命令的帮助。
  > virtuoso-t -? 
  2. 运行命令,进入Virtuoso数据库数据库文件夹下，所有的操作都在这进行
  > cd %VIRTUOSO_HOME%/database
  3. 创建windows服务，创建一个Virtuoso数据库服务，可以在计算机=》管理=》服务中查看默认是 **Openlink Virtuoso(自定义名称)**
  > virtuoso-t +service create +instance "New Instance Name" +configfile virtuoso.ini
  4. virtuoso常用操作指令：
  ```
  显示所有服务                   virtuoso-t +service list
  启动virtuoso服务               virtuoso-t +instance "服务名称" +service start
  停止服务                       virtuoso-t +instance "服务名称" +service stop
  删除服务                       virtuoso-t +instance "服务名称" +service delete
  ```
  
  ## Virtuoso 数据库 在 Linux上安装
  安装Virtuoso，按照Github上面的提示，需要确保安装下面的程序的最低版本

    Package  Version                         From
    ——-  ——-                         —-
    autoconf 2.57               http://www.gnu.org/software/autoconf/
    automake 1.9                http://www.gnu.org/software/automake/
    libtool  1.5.16             http://www.gnu.org/software/libtool/
    flex     2.5.33 (was 2.5.4) http://www.gnu.org/software/non-gnu/flex/
    bison    2.3 (was 1.35)     http://www.gnu.org/software/bison/
    gperf    2.7.2              http://www.gnu.org/software/gperf/
    gawk     3.1.1              http://www.gnu.org/software/gawk/
    m4       1.4.1              http://www.gnu.org/software/m4/
    make     3.79.1             http://www.gnu.org/software/make/
    OpenSSL  0.9.7i             http://www.openssl.org/

    通过下面的指令，在命令行里运行，来检查是否满足基本条件：
    autoconf –version
    automake –version
    libtoolize –version
    flex –version
    bison –version
    gperf –version
    gawk –version
    m4 –version
    make –version
    openssl version

    安装的过程不复杂，进入克隆下来的目录，逐次运行下面命令，要保证有至少800MB的硬盘空间：
    ./autogen.sh
    ./configure –with-layout=debian
    make
    sudo make install
    安装完毕

    运行：
    进入/var/lib/virtuoso/db
    执行virtuoso-t -f &
    之后可以进入下面链接进行操作
    http://localhost:8890/
