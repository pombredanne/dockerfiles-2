FROM php:7-fpm  
RUN apt-get update \  
&& apt-get upgrade -y \  
&& apt-get install -y \  
build-essential \  
php5-dev \  
libfreetype6-dev \  
libjpeg62-turbo-dev \  
libmcrypt-dev \  
libpng12-dev \  
&& docker-php-ext-install iconv mcrypt mysqli pdo pdo_mysql zip \  
&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ \--with-jpeg-
dir=/usr/include/ \  
&& docker-php-ext-install gd \  
&& rm -rf /var/cache/apt/*  
COPY ./php.conf /usr/local/etc/php/conf.d/php.conf  
COPY ./site /var/www/site  

