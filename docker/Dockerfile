FROM php:8.0.13-fpm

RUN apt-get update \
&& apt-get install -y libpq-dev libicu-dev \
&& docker-php-ext-configure intl \
&& docker-php-ext-install intl
RUN apt-get install -y \
        libzip-dev \
        zip \
  && docker-php-ext-install zip
RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pgsql pdo_pgsql pdo_mysql
RUN apt-get remove -y libicu-dev libpq-dev

RUN php -r "copy('http://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

CMD ["php-fpm"]
