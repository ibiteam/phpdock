FROM php:8.1.3-fpm

LABEL maintainer="foryoufeng"

USER root

RUN apt-get update -y && apt-get install -y zlib1g=1:1.2.8.dfsg-5 --allow-downgrades && apt-get install -y  git libz-dev libzip-dev libfreetype6-dev libmcrypt-dev  libjpeg-dev libpng-dev

RUN docker-php-ext-install gd \
    && docker-php-ext-install zip \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install sockets \
    && docker-php-ext-install pdo_mysql \
    && rm -r /var/lib/apt/lists/*

# install composer
RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && rm -f composer-setup.php \
    && mv composer.phar /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

#RUN pecl install xdebug && docker-php-ext-enable xdebug \
#   &&pecl install -o -f redis  &&  rm -rf /tmp/pear  &&  docker-php-ext-enable redis\
#    && pecl install swoole &&  docker-php-ext-enable swoole
# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && rm /var/log/lastlog /var/log/faillog

RUN usermod -u 1000 -s /bin/bash www-data

USER www-data

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000
