FROM php:8.0-fpm
#COPY php.ini /usr/local/etc/php/

ENV TZ=Asia/Tokyo

RUN apt-get update \
  && apt-get install -y zlib1g-dev mariadb-client vim libzip-dev unzip \
     libfreetype6-dev \
     libjpeg62-turbo-dev \
     libpng-dev \
  && docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j$(nproc) gd zip pdo_mysql

#Composer install
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php --version=2.2.4
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

ENV COMPOSER_ALLOW_SUPERUSER 1

ENV COMPOSER_HOME /composer

ENV PATH $PATH:/composer/vendor/bin

#nodejs
RUN curl -sL https://deb.nodesource.com/setup_16.x | bash -
RUN apt-get install -y nodejs

#laravel installer
RUN composer global require laravel/installer
RUN export PATH=$PATH:/root/.config/composer/vendor/bin

WORKDIR /usr/share/nginx/html