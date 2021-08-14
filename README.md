# 使用 Docker-compose 搭建 PHP 开发环境
PHP（7.3）/ MySQL8.0 / Nginx / Redis / RabbitMQ集群 / Supervisor守护进程

请确保你的电脑上面安装好了docker以及docker-compose,如果没有请自行google 或者  百度,使用这个请确保对docker的命令有一定的了解。如果有需要修改配置的话，请在docker-compose.yml文件中修改，然后重新执行一遍命令即可。

## 目录结构：
```html
docker-lnmp
├─mysql
│  └─data
├─nginx
│  ├─conf.d
│  └─log
├─php
│  └─log
├─rabbitmq
│  ├─data
│  ├─data2
│  └─data3
├─redis
│  ├─conf
│  └─data
└─supervisor
    ├─conf.d
    └─log
```
# 创建镜像与安装
 > 直接使用docker-compose一键制作镜像并启动容器
```shell
> git clone https://github.com/jybtx/docker-lnmp.git
> cd docker-lnmp
> docker-compose up -d  
```
 > 将你的域名配置文件放在nginx -> conf.d里面   

 > RabbitMQ集群，请cd rabbitmq目录下执行 shell文件，然后执行
 ```shell
> docker exec rabbitmq1 /bin/bash
> rabbitmqctl set_policy ha-all "^" '{"ha-mode":"all","ha-sync-mode":"automatic"}'
```
# nginx配置
```shell
server {
    listen       80;
    server_name  www.laravel.test;
    root   /var/www/html/laravel/public;
    index  index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
        if (!-e $request_filename){  
            rewrite ^/(.*) /index.php last;  
        }
    }
    
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {}
    
    location ~ \.php$ {
        fastcgi_pass   my_php:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }
}
```
# RabbitMQ配置
```shell
> my_nginx:5675
```
