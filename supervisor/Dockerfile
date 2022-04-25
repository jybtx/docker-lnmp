
FROM php:7.3-fpm

MAINTAINER jybtx <admin@jybtx.com>

RUN export CFLAGS="PHP_CPPFLAGS" LDFLAGS="$PHP_LDFLAGS"

# 国内换源
RUN  sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list
RUN  sed -i s@/security.debian.org/@/mirrors.ustc.edu.cn/@g /etc/apt/sources.list
RUN  sed -i s@/deb.debian.org/@/mirrors.aliyun.com/@g /etc/apt/sources.list && apt-get clean && \

  set -x && \
  apt-get update -y && \
  apt-get upgrade -y && \
  apt-get update && \
  apt-get install -y --no-install-recommends libfreetype6-dev libjpeg62-turbo-dev libpng-dev libxml2-dev libtidy-dev libxslt1-dev libmagickwand-dev libmcrypt-dev libzip-dev supervisor wget vim git redis && \
  rm -r /var/lib/apt/lists/* && \
  pecl install imagick-3.4.3 mcrypt-1.0.3 && \
# 安装swoole
  pecl install -o -f swoole && \
# 安装 memcached 扩展
  # pecl install -o -f memcached && docker-php-ext-enable memcached && \
  docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
  docker-php-ext-install -j$(nproc) gd soap wddx xmlrpc tidy xsl zip bcmath calendar exif sockets pdo_mysql && \
  docker-php-ext-enable imagick mcrypt swoole && \

  curl -sS https://getcomposer.org/installer | php \
  && mv composer.phar /usr/local/bin/composer \
  && composer config -g repo.packagist composer https://packagist.phpcomposer.com


