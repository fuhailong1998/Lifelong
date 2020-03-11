http://www.php.net/downloads.php

官网文档

https://www.php.net/manual/zh/install.unix.nginx.php

下载源码包解压

```
wget https://www.php.net/distributions/php-7.4.3.tar.gz
```

```
tar xzf php-7.4.3.tar.gz 
```

安装依赖

```
apt install -y gcc make openssl curl libbz2-dev libxml2-dev libjpeg-dev libpng-dev libfreetype6-dev libzip-dev libcurl4-gnutls-dev libssl-dev
```

编译

```
./configure --prefix=/usr/local/php --enable-fpm --with-fpm-user=root --with-fpm-group=root --with-mysqli --with-pdo-mysql --with-iconv-dir --with-freetype-dir --with-jpeg-dir --with-png-dir --with-zlib --with-libxml-dir=/usr --enable-xml --disable-rpath --enable-bcmath --enable-shmop --enable-sysvsem --enable-inline-optimization --with-curl --enable-mbregex --enable-mbstring --enable-ftp --with-gd --with-openssl --with-mhash --enable-pcntl --enable-sockets --with-xmlrpc --enable-zip --enable-soap --without-pear --with-gettext --disable-fileinfo --enable-maintainer-zts --enable-zip
```

提示

configure: error: Package requirements (sqlite3 > 3.7.4) were not met:

```
sudo apt-get install sqlite3 libsqlite3-dev
```

重新编译

提示

configure: error: Package requirements (oniguruma) were not met:

```
git clone https://github.com/kkos/oniguruma.git oniguruma
cd oniguruma
./autogen.sh
./configure
make
make install
```

重新编译

+--------------------------------------------------------------------+
| License:                                                           |
| This software is subject to the PHP License, available in this     |
| distribution in the file LICENSE. By continuing this installation  |
| process, you are bound by the terms of this license agreement.     |
| If you do not agree with the terms of this license, you must abort |
| the installation process at this point.                            |
+--------------------------------------------------------------------+

Thank you for using PHP.

```
make
```

Generating phar.php
/root/php/sapi/cli/php: error while loading shared libraries: libonig.so.5: cannot open shared object file: No such file or directory
Makefile:446: recipe for target 'ext/phar/phar.php' failed
make: *** [ext/phar/phar.php] Error 127

```
whereis libonig.so.5
```

libonig.so: /usr/local/lib/libonig.so /usr/local/lib/libonig.so.5

```
export  LD_LIBRARY_PATH=LD_LIBRARY_PATH:/usr/local/lib/
```

```
make
```

Generating phar.phar
chmod: cannot access 'ext/phar/phar.phar': No such file or directory
Makefile:450: recipe for target 'ext/phar/phar.phar' failed
make: [ext/phar/phar.phar] Error 1 (ignored)

Build complete.
Don't forget to run 'make test'.

可忽略

解决办法

```
cd ~/php/ext/phar
cp phar/phar.phar ./phar.phar
```

```
make test
```

=====================================================================
TIME END 2020-03-10 03:26:13

=====================================================================
TEST RESULT SUMMARY
---------------------------------------------------------------------
Exts skipped    :   32
Exts tested     :   41
---------------------------------------------------------------------

Number of tests : 15596             11886
Tests skipped   : 3710 ( 23.8%) --------
Tests warned    :    0 (  0.0%) (  0.0%)
Tests failed    :   45 (  0.3%) (  0.4%)
Expected fail   :   35 (  0.2%) (  0.3%)
Tests passed    : 11806 ( 75.7%) ( 99.3%)
---------------------------------------------------------------------
Time taken      : 1084 seconds
=====================================================================

=====================================================================
EXPECTED FAILED TEST SUMMARY
---------------------------------------------------------------------
Test open_basedir configuration [tests/security/open_basedir_linkinfo.phpt]  XFAIL REASON: BUG: open_basedir cannot delete symlink to prohibited file. See also
bugs 48111 and 52176.
Inconsistencies when accessing protected members [Zend/tests/access_modifiers_008.phpt]  XFAIL REASON: Discussion: http://marc.info/?l=php-internals&m=120221184420957&w=2
Inconsistencies when accessing protected members - 2 [Zend/tests/access_modifiers_009.phpt]  XFAIL REASON: Discussion: http://marc.info/?l=php-internals&m=120221184420957&w=2
Bug #48770 (call_user_func_array() fails to call parent from inheriting class) [Zend/tests/bug48770.phpt]  XFAIL REASON: See Bug #48770
Bug #48770 (call_user_func_array() fails to call parent from inheriting class) [Zend/tests/bug48770_2.phpt]  XFAIL REASON: See Bug #48770
Bug #48770 (call_user_func_array() fails to call parent from inheriting class) [Zend/tests/bug48770_3.phpt]  XFAIL REASON: See Bug #48770
Initial value of static var in method depends on the include time of the class definition [Zend/tests/method_static_var.phpt]  XFAIL REASON: Maybe not a bug
DateTime::add() -- fall type2 type3 [ext/date/tests/DateTime_add-fall-type2-type3.phpt]  XFAIL REASON: Various bugs exist
DateTime::add() -- fall type3 type2 [ext/date/tests/DateTime_add-fall-type3-type2.phpt]  XFAIL REASON: Various bugs exist
DateTime::add() -- fall type3 type3 [ext/date/tests/DateTime_add-fall-type3-type3.phpt]  XFAIL REASON: Various bugs exist
DateTime::add() -- spring type2 type3 [ext/date/tests/DateTime_add-spring-type2-type3.phpt]  XFAIL REASON: Various bugs exist
DateTime::add() -- spring type3 type2 [ext/date/tests/DateTime_add-spring-type3-type2.phpt]  XFAIL REASON: Various bugs exist
DateTime::add() -- spring type3 type3 [ext/date/tests/DateTime_add-spring-type3-type3.phpt]  XFAIL REASON: Various bugs exist
DateTime::diff() -- fall type2 type3 [ext/date/tests/DateTime_diff-fall-type2-type3.phpt]  XFAIL REASON: Various bugs exist
DateTime::diff() -- fall type3 type2 [ext/date/tests/DateTime_diff-fall-type3-type2.phpt]  XFAIL REASON: Various bugs exist
DateTime::diff() -- fall type3 type3 [ext/date/tests/DateTime_diff-fall-type3-type3.phpt]  XFAIL REASON: Various bugs exist
DateTime::diff() -- spring type2 type3 [ext/date/tests/DateTime_diff-spring-type2-type3.phpt]  XFAIL REASON: Various bugs exist
DateTime::diff() -- spring type3 type2 [ext/date/tests/DateTime_diff-spring-type3-type2.phpt]  XFAIL REASON: Various bugs exist
DateTime::diff() -- spring type3 type3 [ext/date/tests/DateTime_diff-spring-type3-type3.phpt]  XFAIL REASON: Various bugs exist
DateTime::sub() -- fall type2 type3 [ext/date/tests/DateTime_sub-fall-type2-type3.phpt]  XFAIL REASON: Various bugs exist
DateTime::sub() -- fall type3 type2 [ext/date/tests/DateTime_sub-fall-type3-type2.phpt]  XFAIL REASON: Various bugs exist
DateTime::sub() -- fall type3 type3 [ext/date/tests/DateTime_sub-fall-type3-type3.phpt]  XFAIL REASON: Various bugs exist
DateTime::sub() -- spring type2 type3 [ext/date/tests/DateTime_sub-spring-type2-type3.phpt]  XFAIL REASON: Various bugs exist
DateTime::sub() -- spring type3 type2 [ext/date/tests/DateTime_sub-spring-type3-type2.phpt]  XFAIL REASON: Various bugs exist
DateTime::sub() -- spring type3 type3 [ext/date/tests/DateTime_sub-spring-type3-type3.phpt]  XFAIL REASON: Various bugs exist
Bug #52480 (Incorrect difference using DateInterval) [ext/date/tests/bug52480.phpt]  XFAIL REASON: See https://bugs.php.net/bug.php?id=52480
RFC: DateTime and Daylight Saving Time Transitions (zone type 3, bd2) [ext/date/tests/rfc-datetime_and_daylight_saving_time-type3-bd2.phpt]  XFAIL REASON: Still not quite right
RFC: DateTime and Daylight Saving Time Transitions (zone type 3, fs) [ext/date/tests/rfc-datetime_and_daylight_saving_time-type3-fs.phpt]  XFAIL REASON: Still not quite right
Bug #42718 (unsafe_raw filter not applied when configured as default filter) [ext/filter/tests/bug42718.phpt]  XFAIL REASON: FILTER_UNSAFE_RAW not applied when configured as default filter, even with flags
Bug #67296 (filter_input doesn't validate variables) [ext/filter/tests/bug49184.phpt]  XFAIL REASON: See Bug #49184
Bug #67167: filter_var(null,FILTER_VALIDATE_BOOLEAN,FILTER_NULL_ON_FAILURE) returns null [ext/filter/tests/bug67167.02.phpt]  XFAIL REASON: Requires php_zval_filter to not use convert_to_string for all filters.
via [ext/pdo_sqlite/tests/common.phpt]
        SQLite PDO Common: PDOStatement::getColumnMeta [ext/pdo_sqlite/tests/pdo_022.phpt]  XFAIL REASON: This feature is not yet finalized, no test makes sense
Phar: bug #69958: Segfault in Phar::convertToData on invalid file [ext/phar/tests/bug69958.phpt]  XFAIL REASON: Still has memory leaks, see https://bugs.php.net/bug.php?id=70005
updateTimestamp never called when session data is empty [ext/session/tests/bug71162.phpt]  XFAIL REASON: Current session module is designed to write empty session always. In addition, current session module only supports SessionHandlerInterface only from PHP 7.0.
Bug #73529 session_decode() silently fails on wrong input [ext/session/tests/bug73529.phpt]  XFAIL REASON: session_decode() does not return proper status.
=====================================================================

=====================================================================
FAILED TEST SUMMARY
---------------------------------------------------------------------
Bug #64267 (CURLOPT_INFILE doesn't allow reset) [ext/curl/tests/bug64267.phpt]
Bug #71523 (Copied handle with new option CURLOPT_HTTPHEADER crashes while curl_multi_exec) [ext/curl/tests/bug71523.phpt]
Bug #78775: TLS issues from HTTP request affecting other encrypted connections [ext/curl/tests/bug78775.phpt]
Bug #78014 (Preloaded classes may depend on non-preloaded classes due to unresolved consts) [ext/opcache/tests/bug78014.phpt]
Bug #78175 (Preloading segfaults at preload time and at runtime) [ext/opcache/tests/bug78175.phpt]
Bug #78175.2 (Preloading segfaults at preload time and at runtime) [ext/opcache/tests/bug78175_2.phpt]
Bug #78376 (Incorrect preloading of constant static properties) [ext/opcache/tests/bug78376.phpt]
Bug #78937.1 (Preloading unlinkable anonymous class can segfault) [ext/opcache/tests/bug78937_1.phpt]
Bug #78937.2 (Preloading unlinkable anonymous class can segfault) [ext/opcache/tests/bug78937_2.phpt]
Bug #78937.3 (Preloading unlinkable anonymous class can segfault) [ext/opcache/tests/bug78937_3.phpt]
Bug #78937.4 (Preloading unlinkable anonymous class can segfault) [ext/opcache/tests/bug78937_4.phpt]
Bug #78937.5 (Preloading unlinkable anonymous class can segfault) [ext/opcache/tests/bug78937_5.phpt]
Bug #78937.6 (Preloading unlinkable anonymous class can segfault) [ext/opcache/tests/bug78937_6.phpt]
Preloading basic test [ext/opcache/tests/preload_001.phpt]
Preloading prototypes [ext/opcache/tests/preload_002.phpt]
Preloading classes linked with traits [ext/opcache/tests/preload_003.phpt]
Preloading class with undefined class constant access [ext/opcache/tests/preload_004.phpt]
Handling of auto globals during preloading [ext/opcache/tests/preload_005.phpt]
Handling of errors during linking [ext/opcache/tests/preload_006.phpt]
Handling of includes that were not executed [ext/opcache/tests/preload_007.phpt]
Preloading of anonymous class [ext/opcache/tests/preload_008.phpt]
Preloading class using trait with undefined class constant access [ext/opcache/tests/preload_009.phpt]
Initializer of overwritten property should be resolved against the correct class [ext/opcache/tests/preload_010.phpt]
Argument/return types must be available for preloading [ext/opcache/tests/preload_011.phpt]
No autoloading during constant resolution [ext/opcache/tests/preload_012.phpt]
Nested function definition [ext/opcache/tests/preload_013.phpt]
Bug #79114 (Eval class during preload causes class to be only half available) [ext/opcache/tests/preload_bug79114.phpt]
Bug #78918: Class alias during preloading causes assertion failure [ext/opcache/tests/preload_class_alias.phpt]
Bug #78918.2: Class alias during preloading causes assertion failure [ext/opcache/tests/preload_class_alias_2.phpt]
Preloading: Loadable class checking (1) [ext/opcache/tests/preload_loadable_classes_1.phpt]
Preloading: Loadable class checking (2) [ext/opcache/tests/preload_loadable_classes_2.phpt]
Preloading: Loadable class checking (3) [ext/opcache/tests/preload_loadable_classes_3.phpt]
Preload trait with static variables in method [ext/opcache/tests/preload_trait_static.phpt]
Preload: Unresolved property type [ext/opcache/tests/preload_unresolved_prop_type.phpt]
pcntl_exec() 2 [ext/pcntl/tests/pcntl_exec_2.phpt]
Multicast support: IPv6 receive options [ext/sockets/tests/mcast_ipv6_recv.phpt]
ext/sockets - socket_bind - basic test [ext/sockets/tests/socket_bind.phpt]
sendmsg()/recvmsg(): test ability to receive multiple messages (WIN32) [ext/sockets/tests/socket_sendrecvmsg_multi_msg.phpt]
proc_open() regression test 1 (proc_open() leak) [ext/standard/tests/file/proc_open01.phpt]
Using proc_open() with a command array (no shell) [ext/standard/tests/general_functions/proc_open_array.phpt]
Bug #46024 stream_select() doesn't return the correct number [ext/standard/tests/streams/bug46024.phpt]
Bug #60120 proc_open hangs with stdin/out with >2048 bytes [ext/standard/tests/streams/proc_open_bug60120.phpt]
Bug #64438 proc_open hangs with stdin/out with 4097+ bytes [ext/standard/tests/streams/proc_open_bug64438.phpt]
stream context tcp_nodelay [ext/standard/tests/streams/stream_context_tcp_nodelay.phpt]
stream context tcp_nodelay fopen [ext/standard/tests/streams/stream_context_tcp_nodelay_fopen.phpt]
=====================================================================

You may have found a problem in PHP.
This report can be automatically sent to the PHP QA team at
http://qa.php.net/reports and http://news.php.net/php.qa.reports
This gives us a better understanding of PHP's behavior.
If you don't want to send the report immediately you can choose
option "s" to save it.  You can then email it to qa-reports@lists.php.net later.
Do you want to send this report now? [Yns]: Y

Please enter your email address.
(Your address will be mangled so that it will not go out on any
mailinglist in plain text): 1414390893@qq.com

Posting to http://qa.php.net/buildtest-process.php

Thank you for helping to make PHP better.
Makefile:222: recipe for target 'test' failed
make: *** [test] Error 1

```
make install
```

查看php版本

```
/usr/local/php/bin/php -v
```

PHP 7.4.3 (cli) (built: Mar 10 2020 10:36:50) ( ZTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies

添加环境变量

```
vim  ~/.bashrc
```

```
export PATH=/usr/local/php/bin/:$PATH
```

```
source  ~/.bashrc
```

```
php -v
```

PHP 7.4.3 (cli) (built: Mar 10 2020 10:36:50) ( ZTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies

lnmp环境nginx无法解析php文件，html正常解析。

需要php-fpm



```
vim  ~/.bashrc
```

```
export PATH=/usr/local/php/sbin/:$PATH
```

```
source  ~/.bashrc
```

```
php-fpm
```

ERROR: failed to open configuration file '/usr/local/php/etc/php-fpm.conf': No such file or directory (2)
ERROR: failed to load configuration file '/usr/local/php/etc/php-fpm.conf'
ERROR: FPM initialization failed

原因：配置文件没有准备好

```
cp php.ini-development /usr/local/php/php.ini
cp /usr/local/php/etc/php-fpm.d/www.conf.default /usr/local/php/etc/php-fpm.d/www.conf
cp sapi/fpm/php-fpm /usr/local/bin
```

```
php-fpm
```


[pool www] please specify user and group other than root
ERROR: FPM initialization failed

```
php-fpm
```



以下为官网文档

https://www.php.net/manual/zh/install.unix.nginx.php

## Unix 系统下的 Nginx 1.4.x[ ¶](https://www.php.net/manual/zh/install.unix.nginx.php#install.unix.nginx)

本文档包括使用 PHP-FPM 为 Nginx 1.4.x HTTP 服务器安装和配置 PHP 的说明和提示。

本指南假定您已经从源代码成功构建 Nginx，并且其二进制文件和配置文件都位于 */usr/local/nginx*。 如果您使用其他方式获取的 Nginx，请参考 [» Nginx Wiki](http://wiki.nginx.org/Main) 并对照本文档完成安装。

本文档仅包含 Nginx 服务器的基本配置，它将通过 80 端口提供 PHP 应用的处理能力。 如果您需要超出本文档范围的安装配置指导，建议您查阅 Nginx 和 PHP-FPM 的文档。

需要注意的是，本文档一律使用 'x' 来表示版本号，请根据实际情况将 'x' 替换为对应的版本号。

1. 建议您访问 Nginx Wiki [» 安装](http://wiki.nginx.org/Install) 页面以获取并在您的系统上安装 Nginx。

2. 获取并解压 PHP 源代码:

   ```
   tar zxf php-x.x.x
   ```

3. 配置并构建 PHP。在此步骤您可以使用很多选项自定义 PHP，例如启用某些扩展等。 运行 ./configure --help 命令来获得完整的可用选项清单。 在本示例中，我们仅进行包含 PHP-FPM 和 MySQL 支持的简单配置。

   ```
   cd ../php-x.x.x
   ./configure --enable-fpm --with-mysql
   make
   sudo make install
   ```

4. 创建配置文件，并将其复制到正确的位置。

   ```
   cp php.ini-development /usr/local/php/php.ini
   cp /usr/local/etc/php-fpm.d/www.conf.default /usr/local/etc/php-fpm.d/www.conf
   cp sapi/fpm/php-fpm /usr/local/bin
   ```

5. 需要着重提醒的是，如果文件不存在，则阻止 Nginx 将请求发送到后端的 PHP-FPM 模块， 以避免遭受恶意脚本注入的攻击。

   将 php.ini 文件中的配置项 [cgi.fix_pathinfo](https://www.php.net/manual/zh/ini.core.php#ini.cgi.fix-pathinfo) 设置为 *0* 。

   打开 php.ini:

   ```
   vim /usr/local/php/php.ini
   ```

   定位到 *cgi.fix_pathinfo=* 并将其修改为如下所示：

   ```
   cgi.fix_pathinfo=0
   ```

6. 在启动服务之前，需要修改 php-fpm.conf 配置文件，确保 php-fpm 模块使用 www-data 用户和 www-data 用户组的身份运行。

   ```
   vim /usr/local/etc/php-fpm.d/www.conf
   ```

   找到以下内容并修改：

   ```
   ; Unix user/group of processes
   ; Note: The user is mandatory. If the group is not set, the default user's group
   ;       will be used.
   user = www-data
   group = www-data
   ```

   然后启动 php-fpm 服务：

   ```
   /usr/local/bin/php-fpm
   ```

   本文档未涵盖对 php-fpm 进行进一步配置的信息，如果您需要更多信息，请查阅相关文档。

7. 配置 Nginx 使其支持 PHP 应用：

   ```
   vim /usr/local/nginx/conf/nginx.conf
   ```

   修改默认的 location 块，使其支持 .php 文件：

   ```
   location / {
       root   html;
       index  index.php index.html index.htm;
   }
   ```

   下一步配置来保证对于 .php 文件的请求将被传送到后端的 PHP-FPM 模块， 取消默认的 PHP 配置块的注释，并修改为下面的内容：

   ```
   location ~* \.php$ {
       fastcgi_index   index.php;
       fastcgi_pass    127.0.0.1:9000;
       include         fastcgi_params;
       fastcgi_param   SCRIPT_FILENAME    $document_root$fastcgi_script_name;
       fastcgi_param   SCRIPT_NAME        $fastcgi_script_name;
   }
   ```

   重启 Nginx。

   ```
   sudo /usr/local/nginx/sbin/nginx -s stop
   sudo /usr/local/nginx/sbin/nginx
   ```

8. 创建测试文件。

   ```
   rm /usr/local/nginx/html/index.html
   echo "<?php phpinfo(); ?>" >> /usr/local/nginx/html/index.php
   ```

   打开浏览器，访问 http://localhost，将会显示 phpinfo() 。

通过以上步骤的配置，Nginx 服务器现在可以以 *SAPI* *SAPI* 模块的方式支持 PHP 应用了。 当然，对于 Nginx 和 PHP 的配置，还有很多可用的选项， 请在对应的源代码目录执行 **./configure --help** 来查阅更多配置选项。