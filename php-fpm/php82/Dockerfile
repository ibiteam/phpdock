FROM php:8.2.11-fpm

LABEL maintainer="wuqiang"

USER root

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' >/etc/timezone

RUN apt-get update -y &&  apt-get install -y  git libz-dev libzip-dev libfreetype6-dev libmcrypt-dev  libjpeg-dev libpng-dev

RUN docker-php-ext-install gd \
    && docker-php-ext-install zip \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install sockets \
    && docker-php-ext-install pcntl \
    && docker-php-ext-install pdo_mysql \
    && pecl install swoole &&  docker-php-ext-enable swoole

RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && rm -f composer-setup.php \
    && mv composer.phar /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

COPY php.ini /usr/local/etc/php/php.ini

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && rm /var/log/lastlog /var/log/faillog

RUN usermod -u 1000 -s /bin/bash www-data

USER www-data

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000