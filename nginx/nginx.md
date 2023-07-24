# nginx 转发
## windows安装
> https://github.com/nginx/nginx/tags

下载相应的zip包，解压后直接进入目录执行 ```start nginx``` 启动服务

结束服务
> nginx.exe -s stop

重启服务
> nginx.exe -s reload

## Ubuntu
下载文件包 并解压
> http://nginx.org/en/download.html

> sudo apt-get install openssl libssl-dev

> cd /opt && wget http://nginx.org/download/nginx-1.25.1.tar.gz && tar -zxvf nginx-1.25.1.tar.gz

编译

> cd nginx-1.25.1 && ./configure  --with-http_ssl_module

> make && make install

配置映射文件

> vim /usr/local/nginx/conf/nginx.conf

命令

> /usr/local/nginx/sbin/nginx -s start/reload/stop

nginx.conf转接8880到本地的4000端口示例, 并建立ws连接
```text

#user  nobody;
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

map $http_upgrade $connection_upgrade {
    default upgrade;
    ''      close;
}

    server {
        listen       5000;
        #server_name  127.0.0.1;
        location / {
            # root   html;
            # index  index.html index.htm;
            proxy_pass http://172.21.87.231:4000;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection $connection_upgrade;
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
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

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
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}
```