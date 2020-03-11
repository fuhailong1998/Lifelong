官方文档

https://dev.mysql.com/doc/refman/8.0/en/source-installation.html

https://www.cnblogs.com/Blueeeeeeee/p/12425279.html#ubuntu%E7%B3%BB

下载带有boost头的源码包

```
wget https://dev.mysql.com/get/Downloads/MySQL-8.0/mysql-boost-8.0.19.tar.gz
```

由于选择了带有boost头的包

```
cmake .. \
-DWITH_BOOST=/root/mysql/boost/boost_1_70_0 \
-DDEFAULT_CHARSET=utf8 \
-DDEFAULT_COLLATION=utf8_general_ci \
-DENABLED_LOCAL_INFILE=ON \
-DWITH_SSL=system \
-DCMAKE_INSTALL_PREFIX=/usr/local/mysql/server \
-DMYSQL_DATADIR=/usr/local/mysql/data \
-DMYSQL_TCP_PORT=3306 \
```

没选的话

```
cmake .. \
-DDOWNLOAD_BOOST=1 \
-DWITH_BOOST=. \
-DDEFAULT_CHARSET=utf8 \
-DDEFAULT_COLLATION=utf8_general_ci \
-DENABLED_LOCAL_INFILE=ON \
-DWITH_SSL=system \
-DCMAKE_INSTALL_PREFIX=/usr/local/mysql/server \
-DMYSQL_DATADIR=/usr/local/mysql/data \
-DMYSQL_TCP_PORT=3306 \
```

安装了boost的可以不需要：

```
-DDOWNLOAD_BOOST=1 
-DWITH_BOOST
```

安装位置与数据位置根据需要自定义：

```
-DCMAKE_INSTALL_PREFIX=
-DMYSQL_DATADIR=
```

报错

```
CMake Error at cmake/readline.cmake:71 (MESSAGE):
  Curses library not found.  Please install appropriate package,

      remove CMakeCache.txt and rerun cmake.On Debian/Ubuntu, package name is libncurses5-dev, on Redhat and derivates it is ncurses-devel.
Call Stack (most recent call first):
  cmake/readline.cmake:100 (FIND_CURSES)
  cmake/readline.cmake:194 (MYSQL_USE_BUNDLED_EDITLINE)
  CMakeLists.txt:1195 (MYSQL_CHECK_EDITLINE)


-- Configuring incomplete, errors occurred!
See also "/root/mysql/boost/CMakeFiles/CMakeOutput.log".
See also "/root/mysql/boost/CMakeFiles/CMakeError.log".

```

需要安装libncurses5-dev

```
apt-get install libncurses5-dev
```

移除CMakeCache.txt 

```
rm CMakeCache.txt 
```

继续报错

```
CMake Warning at cmake/pkg-config.cmake:29 (MESSAGE):
  Cannot find pkg-config.  You need to install the required package:

    Debian/Ubuntu:              apt install pkg-config
    RedHat/Fedora/Oracle Linux: yum install pkg-config
    SuSE:                       zypper install pkg-config

Call Stack (most recent call first):
  cmake/rpc.cmake:29 (MYSQL_CHECK_PKGCONFIG)
  plugin/group_replication/libmysqlgcs/configure.cmake:57 (MYSQL_CHECK_RPC)
  plugin/group_replication/libmysqlgcs/CMakeLists.txt:28 (INCLUDE)


CMake Error at /usr/share/cmake-3.10/Modules/FindPackageHandleStandardArgs.cmake:137 (message):
  Could NOT find PkgConfig (missing: PKG_CONFIG_EXECUTABLE)
Call Stack (most recent call first):
  /usr/share/cmake-3.10/Modules/FindPackageHandleStandardArgs.cmake:378 (_FPHSA_FAILURE_MESSAGE)
  /usr/share/cmake-3.10/Modules/FindPkgConfig.cmake:36 (find_package_handle_standard_args)
  cmake/pkg-config.cmake:36 (FIND_PACKAGE)
  cmake/rpc.cmake:29 (MYSQL_CHECK_PKGCONFIG)
  plugin/group_replication/libmysqlgcs/configure.cmake:57 (MYSQL_CHECK_RPC)
  plugin/group_replication/libmysqlgcs/CMakeLists.txt:28 (INCLUDE)


-- Configuring incomplete, errors occurred!
See also "/root/mysql/bld/CMakeFiles/CMakeOutput.log".
See also "/root/mysql/bld/CMakeFiles/CMakeError.log".

```

安装

```
apt install pkg-config
```

再次cmake成功

```
make
```

```
make install
```

卡住[ 52%] Building CXX object sql/CMakeFiles/sql_gis.dir/item_geofunc_setops.cc.o

g++: 内部错误：Killed (程序 cc1plus)

这个原因是内存不足， 在linux下增加临时swap空间
step 1:

```
sudo dd if=/dev/zero of=/home/swap bs=64M count=16
```

of=/home/swap,放置swap的空间; count的大小就是增加的swap空间的大小，64M就是块大小，这里是64MB，所以总共空间就是bs*count=1024MB.这里分配空间的时候需要一点时间，等待执行完毕。
step 2:

```
sudo mkswap /home/swap
```

可能会提示warning: don't erase bootbits sectorson whole disk. Use -f to force，不用理会：把刚才空间格式化成swap各式
step 3:

```
sudo swapon /home/swap
```

　　注释：使刚才创建的swap空间
step 4:执行你相关的操作，如make
如果创建了临时空间仍然提示 "g++: 内部错误：Killed (程序 cc1plus)"，可能分配的空间不够大，可继续分配更大的空间。
关闭:
step 1:

```
sudo swapoff /home/swap
```

step 2:

```
sudo rm /home/swap
```

23:24-04:06装了四个半小时。。

```
 make install
```

测试

```
make test
```

100% tests passed, 0 tests failed out of 19
Total Test time (real) =   2.14 sec

配置MySQL
安装完成后还需要进行MySQL的配置。

新建用户组与用户

```
groupadd mysql
useradd -r -g mysql -s /bin/false mysql
```

修改数据目录所有者与权限
数据目录根据需要修改。

```
chown mysql:mysql /usr/local/mysql/data
chmod 777 /usr/local/mysql/data
```

这里官网的文档写的是750权限，但是后面会出现不可写错误，755也不行，所以直接改成了777。
my.cnf
my.cnf在/etc或/etc/mysql下，笔者这里安装后默认有一个my.cnf在/etc/mysql下：
/etc/mysql/my.cnf是全局配置，~/.my.cnf是用户特定的配置，这里直接修改/etc/mysql/my.cnf：

```
[mysqld]
port=3306
basedir=/usr/local/mysql/server
datadir=/usr/local/mysql/data
character-set-server=utf8mb4
[mysql]
default-character-set=utf8
[client]
port=3306
default-character-set=utf8
```


参数根据需要可以后期添加，这里如果使用utf8：

```
[mysqld]
character-set-server=utf8
```


会有警告，因为MySQL5.5.3之后增加了utf8mb4，mb4是most bytes 4的意思，专门用来兼容四字节的unicode，utf8指的是utf8mb3，支持的utf8编码最大字符长度为3字节，警告提示改成utf8mb4:

```
[mysqld]
character-set-server=utf8mb4
```

初始化
进入到MySQL Server的安装目录下的bin：

```
./mysqld --initialize-insecure --user=mysql
```

2020-03-10T00:37:08.708780Z 0 [System] [MY-013169] [Server] /usr/local/mysql/server/bin/mysqld (mysqld 8.0.19) initializing of server in progress as process 14069
2020-03-10T00:37:12.485582Z 5 [Warning] [MY-010453] [Server] root@localhost is created with an empty password ! Please consider switching off the --initialize-insecure option.

这里使用-insecure是因为后面不用输入随机密码。当然也可以去掉insecure，这样就会有一个随机密码，要记住。

```
mysqld --initialize --user=mysql
```

支持ssl与rsa（可选）

```
./mysql_ssl_rsa_setup
```

这个一般服务器需要。

开启服务

```
./mysqld_safe --user=mysql &
```

修改root密码
先用root登录

```
./mysql -u root --skip-password
```

如果是使用initialize初始化的，输入

```
./mysql -u root -p
```

输入刚才的临时密码。
进去之后，使用alter修改root密码：

```
alter user 'root'@'localhost' identified with mysql_native_password by '123456';flush privileges
```

加入with mysql_native_password可以保证navicat连接不会出问题

测试
使用自带的mysqlshow与mysqladmin:

```
./mysqladmin -u root -p version
./mysqlshow -u root -p
```


至此MySQL Server8.0.19安装完毕。

后续处理
删除文件
可以先把安装文件给删去：

```
rm -rf mysql-8.0.19*
```

根据刚才cmake的时候的boost目录可以把boost库给删去：

```
rm -rf boost_1_70_0*
```

因为文档说只是需要boost去build，不需要使用。

别名
加个别名只是为了方便使用，这里笔者的做法其实很偷懒，默认root登录，修改~/.bashrc：

```
alias mysqld="/usr/local/mysql/server/bin/mysqld_safe --user=mysql &"
alias mysql="/usr/local/mysql/server/bin/mysql -u root -p"
```

使用MySQL之前使用mysqld启动服务挂后台，然后使用mysql登录，默认root用户。
当然更偷懒的做法是

```
alias mysql="/usr/local/mysql/server/bin/mysql -u root --password=xxxx"
```

这样密码都不用输了。

```
 source ~/.bashrc 
```

使文件生效

Navicat链接数据库报错1130解决方案

问题原因：默认情况下root用户只允许本机访问,即使用localhost访问

解决方案：将root用户对用的host改为 '%',即允许所有IP访问,然后刷新即可.

问题解决具体步骤
1.命令窗口登录mysql

```
mysql  -uroot  -padmin
```

2.连接到mysql(数据库名)

```
use mysql;
```

3.修改表user的值

```
update user set host = '%' where user = 'root';
```

4.刷新配置

```
flush   privileges;
```

