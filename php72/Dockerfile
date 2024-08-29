FROM php:7.2-fpm

MAINTAINER jybtx <admin@jybtx.com>

RUN  sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list
RUN  sed -i s@/security.debian.org/@/mirrors.aliyun.com/@g /etc/apt/sources.list
RUN  sed -i s@/deb.debian.org/@/mirrors.aliyun.com/@g /etc/apt/sources.list && apt-get clean

# 安装基础
RUN set -x && \
  apt-get update -y && \
  apt-get upgrade -y && \
  apt-get install -y libfreetype6-dev curl libgmp-dev libjpeg62-turbo-dev libpng-dev libxml2-dev libtidy-dev libxslt1-dev libmagickwand-dev libmcrypt-dev libzip-dev libmemcached-dev supervisor default-mysql-client redis procps  && \
  pecl install imagick mcrypt && \
  docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
  docker-php-ext-install -j$(nproc) gd soap wddx gmp xmlrpc tidy xsl zip bcmath calendar exif sockets pdo_mysql pcntl && \
  docker-php-ext-enable imagick mcrypt  && \
  rm -rf /var/lib/apt/lists/*

# 安装 memcached 扩展
RUN pecl install memcached  && docker-php-ext-enable memcached
# 安装 redis 扩展
RUN pecl install redis && docker-php-ext-enable redis
# 安装 swoole 扩展
RUN pecl install swoole-4.8.12 && docker-php-ext-enable swoole



## 安装 Composer
RUN curl -sS https://getcomposer.org/installer | php \
   && mv composer.phar /usr/local/bin/composer \
   && composer config -g repo.packagist composer https://packagist.org