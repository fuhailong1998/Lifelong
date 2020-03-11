更新包

sudo apt-get update

apt install screen

安装依赖包

sudo apt-get install libpcre3 libpcre3-dev openssl libssl-dev zlib1g-dev

http://nginx.org/en/download.html

wget http://nginx.org/download/nginx-1.16.1.tar.gz

mkdir nginx-1.16.1

tar -xzvf nginx-1.16.1.tar.gz -C nginx-1.16.1/

在nginx文件夹配置

./configure --prefix=/usr/local/nginx --with-http_ssl_module

安装

make && make install

启动nginx

/usr/local/nginx/sbin/nginx

查看Nginx进程是否启动

ps aux | grep nginx


查看Nginx占用的端口号

netstat -tlnp

停止Nginx的三种方式

停止Nginx服务

/usr/local/nginx/sbin/nginx -s stop

2.完成当前任务后停止

/usr/local/nginx/sbin/nginx -s quit

3.杀死Nginx进程

killall nginx



显示当前环境变量PATH

echo $PATH
编辑.bashrc文件

```
vim ~/.bashrc
```

在.bash_profile文件末尾加入以下内容

```
export PATH=/usr/local/nginx/sbin:$PATH
```

引用.bash_profile文件

```
source ~/.bashrc
```


使用nginx命令

启动nginx

```
nginx
```

停止nginx

```
nginx -s quit
```

把nginx命令添加到系统服务

进入/etc/init.d目录下创建nginx脚本

```
#!/bin/sh

### BEGIN INIT INFO

# Provides:    nginx

# Required-Start:

# Required-Stop:

# Default-Start:        2 3 4 5

# Default-Stop:        0 1 6

# Short-Description: nginx

# Description: nginx server

### END INIT INFO

#. /lib/lsb/init-functions

PROGRAM=/usr/local/nginx/nginx


test -x $PROGRAM || exit 0

case "$1" in
  start)
    log_begin_msg "Starting Nginx server"
    /usr/local/nginx/nginx
    log_end_msg 0
    ;;
  stop)
    PID=`cat /usr/local/nginx/nginx.pid`
    log_begin_msg "Stopping Nginx server"
    if [ ! -z "$PID" ]; then
        kill -15 $PID
    fi
    log_end_msg 0
    ;;
  restart)
    $0 stop
    $0 start
    ;;
  *)
    log_success_msg "Usage: service nginx {start|stop|restart}"
    exit 1
esac

exit 0
```

然后运行下面的命令：
sudo chmod +x nginx
sudo update-rc.d nginx defaults
现在可以使用下面的命令了，重新启动nginx会自动启动
sudo service nginx start
sudo service nginx stop

赋予可执行限权

```
chmod +x /etc/init.d/nginx
```

注册为系统服务

```
update-rc.d nginx defaults
```

重载

```
systemctl daemon-reload
```

通过service命令管理nginx

```
service nginx start/stop/restart/status
```

```
deb http://archive.ubuntu.com/ubuntu/ trusty main universe restricted multiverse
```

配置证书

查看nginx模块

```
/usr/local/nginx/sbin/nginx -V
```

重新编译nginx

```
./configure --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module --with-file-aio --with-http_realip_module
```

```
make
```

```
cp objs/nginx  /usr/local/nginx/sbin/nginx 
```

```
vim /usr/local/nginx/conf/nginx.conf
```

```
server {
listen       443 ssl;
server_name  localhost;

ssl_certificate      3539117_fxkxb.com_nginx/3539117_fxkxb.com.pem;
ssl_certificate_key  3539117_fxkxb.com_nginx/3539117_fxkxb.com.key;

ssl_session_cache    shared:SSL:1m;
ssl_session_timeout  5m;

ssl_ciphers  HIGH:!aNULL:!MD5;
ssl_prefer_server_ciphers  on;

location / {
root   html;
index  index.html index.htm;
}

}
```

```
vim /usr/local/nginx/conf/nginx.conf
```

    server {
        listen       80;
        server_name  localhost;
        return 301 https://fxkxb.com$request_uri;

开机自启

进入 etc/apt

```
cd /etc/apt
```

使用vim sources.list命令 在里面sources.list 添加镜像源:

```
deb http://archive.ubuntu.com/ubuntu/ trusty main universe restricted multiverse
```

 更新安装源

```
sudo apt-get update 
```

开始安装

```
sudo apt-get install sysv-rc-conf
```

链接 chkconfig

```
sudo cp /usr/sbin/sysv-rc-conf /usr/sbin/chkconfig
```

执行

```
sysv-rc-conf
```

界面说明(上下键切换到nginx选项，空格选中，q保存退出)
运行级别说明：
S   表示开机后就会运行的服务
0   表示关机
1   表示单用户模式  （类似windows的安全模式）
2   表示无网络服务的多用户模式
3   表示多用户模式
4   系统预留（暂没使用）
5   表示多用户图形模式
6   表示重启

```
sysv-rc-conf nginx on
```

```
nginx -s reload
```

nginx: [error] open() "/usr/local/nginx/logs/nginx.pid" failed (2: No such file or directory)

```
/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
```

linux环境下nginx文件彻底删除

第一步：输入以下指令全局查找nginx相关的文件：

sudo find / -name nginx*


第二步：删除查找出来的所有nginx相关文件

sudo rm -rf file 此处跟查找出来的nginx文件


说明：全局查找往往会查出很多相关文件，但是前缀基本都是相同，后面不同的部分可以用*代替，以便快速删除~

举例说明：

sudo rm -rf file /usr/local/nginx*

添加nginx对php解析

```
location ~* \.php$ {

            fastcgi_pass   127.0.0.1:9000;
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
            include        fastcgi_params;
        }
```

完整nginx.conf文件

```

#user  root;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    server {
        listen       80;
        server_name  localhost;
	return 301 https://fxkxb.com$request_uri;
        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            root   html;
            index  index.php index.html index.htm;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        location ~* \.php$ {

            fastcgi_pass   127.0.0.1:9000;
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
            include        fastcgi_params;
        }

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    server {
	listen       443 ssl;
	server_name  localhost;

	ssl_certificate      3539117_fxkxb.com_nginx/3539117_fxkxb.com.pem;
	ssl_certificate_key  3539117_fxkxb.com_nginx/3539117_fxkxb.com.key;

	ssl_session_cache    shared:SSL:1m;
	ssl_session_timeout  5m;

	ssl_ciphers  HIGH:!aNULL:!MD5;
	ssl_prefer_server_ciphers  on;

	location / {
	root   html;
	index index.php index.html index.htm;
	}
	location ~* \.php$ {

            fastcgi_pass   127.0.0.1:9000;
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
            include        fastcgi_params;
        }
	

	}
}

```

