
FROM php:7.4-fpm

MAINTAINER jybtx <admin@jybtx.com>

RUN  sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list
RUN  sed -i s@/security.debian.org/@/mirrors.aliyun.com/@g /etc/apt/sources.list
RUN  sed -i s@/deb.debian.org/@/mirrors.aliyun.com/@g /etc/apt/sources.list && apt-get clean && \

# 安装基础
  set -x && \
  apt-get update -y && \
  apt-get upgrade -y && \
  apt-get install -y libcurl4-openssl-dev libssl-dev git zip libbz2-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev libicu-dev libmemcached-dev libz-dev libpq-dev libzip-dev libonig-dev libjpeg-dev libmcrypt-dev libtidy-dev libxslt1-dev libmagickwand-dev supervisor zlib1g-dev libxml2-dev graphviz redis  \
  && docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j$(nproc) gd \
  && docker-php-ext-install pdo_mysql intl pcntl sockets soap exif opcache zip \
# && docker-php-ext-install bcmath intl pcntl sockets soap exif opcache swoole redis \
  && rm -rf /var/lib/apt/lists/* \

  && apt-get clean \


# 删除php源码，有助于减小生成的镜像大小
 && docker-php-source delete;

# 安装 Composer
RUN curl -sS https://getcomposer.org/installer | php \
   && mv composer.phar /usr/local/bin/composer \
   && composer config -g repo.packagist composer https://packagist.org
