
FROM php:8.0-fpm

MAINTAINER jybtx <admin@jybtx.com>

# Install Supervisor.
RUN set -x && \
  apt update -y && \
  apt upgrade -y && \
  apt install -y supervisor && \
  rm -rf /var/lib/apt/lists/*


RUN curl -sS https://getcomposer.org/installer | php \
   && mv composer.phar /usr/local/bin/composer \
   && composer config -g repo.packagist composer https://packagist.phpcomposer.com

# ------------------------------------------------------------------------------
# Start supervisor, define default command.
CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
