FROM php:fpm  
  
RUN apt-get update && apt-get install -y \  
libfreetype6-dev \  
libjpeg62-turbo-dev \  
libpng-dev \  
&& docker-php-ext-configure gd \--with-freetype-dir=/usr/include/ \--with-
jpeg-dir=/usr/include/ \  
&& docker-php-ext-install -j$(nproc) gd \  
&& docker-php-ext-install -j$(nproc) bcmath pdo_mysql opcache \  
&& pecl install redis-4.0.2 \  
&& pecl install xdebug-2.6.0 \  
&& docker-php-ext-enable redis xdebug  
  
RUN mkdir -p /www  

