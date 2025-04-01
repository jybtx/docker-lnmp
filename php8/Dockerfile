
FROM php:8.2-fpm
# FROM php:8.1-fpm

MAINTAINER jybtx <admin@jybtx.com>

#RUN  sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list
#RUN  sed -i s@/security.debian.org/@/mirrors.aliyun.com/@g /etc/apt/sources.list
#RUN  sed -i s@/deb.debian.org/@/mirrors.aliyun.com/@g /etc/apt/sources.list && apt-get clean

# 安装基础
RUN  set -x && \
  apt-get update -y && \
  apt-get upgrade -y && \
  apt-get update && \
  apt-get install -y --no-install-recommends libicu-dev libmemcached-dev libz-dev libpq-dev libzip-dev libonig-dev libjpeg62-turbo-dev libjpeg-dev libpng-dev libfreetype6-dev libssl-dev libmcrypt-dev libtidy-dev libxslt1-dev libmagickwand-dev supervisor zlib1g-dev libxml2-dev libbz2-dev graphviz procps default-mysql-client librdkafka-dev && \

  rm -rf /var/lib/apt/lists/* && \

# 安装PHP扩展
  docker-php-ext-configure bcmath --enable-bcmath \
  && docker-php-ext-configure pcntl --enable-pcntl \
  && docker-php-ext-configure pdo_mysql --with-pdo-mysql \
  && docker-php-ext-configure mbstring --enable-mbstring \
  && docker-php-ext-configure soap --enable-soap \
  && docker-php-ext-configure exif --enable-exif \
  && docker-php-ext-install bcmath intl mbstring mysqli pcntl pdo_mysql sockets zip soap exif \
  && docker-php-ext-install opcache \
  && docker-php-ext-enable opcache && \
  docker-php-ext-configure gd --with-jpeg=/usr/lib --with-freetype=/usr/include/freetype2 && \

  docker-php-ext-install gd && \

# 安装 Redis 扩展
  pecl install -o -f redis && docker-php-ext-enable redis && \

  mysql -V && \

# 安装 grpc 扩展
pecl install -o -f grpc && docker-php-ext-enable grpc && \

# 安装 protobuf 扩展
pecl install -o -f protobuf  && docker-php-ext-enable protobuf && \

# install rdkafka
pecl install -o -f rdkafka && docker-php-ext-enable rdkafka && \

# 安装 imagick 扩展
pecl install -o -f imagick && docker-php-ext-enable imagick && \

# 安装 memcached 扩展
pecl install -o -f memcached  && docker-php-ext-enable memcached && \

# 安装 swoole 扩展
pecl install -o -f swoole && docker-php-ext-enable swoole && \

# 清除安装文件
apt-get clean && \

# 删除php源码，有助于减小生成的镜像大小
docker-php-source delete

# 安装 Composer
RUN curl -sS https://getcomposer.org/installer | php \
   && mv composer.phar /usr/local/bin/composer \
   && composer config -g repo.packagist composer https://packagist.org





