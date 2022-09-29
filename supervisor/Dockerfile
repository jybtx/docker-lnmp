
FROM php:7.3-fpm

MAINTAINER jybtx <admin@jybtx.com>

RUN export CFLAGS="PHP_CPPFLAGS" LDFLAGS="$PHP_LDFLAGS"

# COPY sources.list /etc/apt

RUN  sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list
RUN  sed -i s@/security.debian.org/@/mirrors.aliyun.com/@g /etc/apt/sources.list
RUN  sed -i s@/deb.debian.org/@/mirrors.aliyun.com/@g /etc/apt/sources.list && apt-get clean


RUN set -x && \
  apt-get update -y && \
  apt-get upgrade -y && \
  apt-get update && \
  apt-get install -y --no-install-recommends libfreetype6-dev libjpeg62-turbo-dev libpng-dev libxml2-dev libtidy-dev libxslt1-dev libmagickwand-dev libmcrypt-dev libzip-dev libmemcached-dev supervisor vim git redis procps && \
  rm -r /var/lib/apt/lists/* && \  
  pecl install imagick-3.7.0 mcrypt-1.0.5  swoole && \
  docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
  docker-php-ext-install -j$(nproc) gd soap wddx xmlrpc tidy xsl zip bcmath calendar exif sockets pdo_mysql pcntl && \
  docker-php-ext-enable imagick mcrypt swoole && \
# 安装 memcached 扩展
pecl install memcached  && docker-php-ext-enable memcached && \

  docker-php-source delete


RUN curl -sS https://getcomposer.org/installer | php \
   && mv composer.phar /usr/local/bin/composer \
   && composer config -g repo.packagist composer https://packagist.org
