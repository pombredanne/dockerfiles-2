FROM php:7.2-fpm  
  
RUN apt-get update \  
&& echo "postfix postfix/mailname string example.com" | debconf-set-selections
\  
&& echo "postfix postfix/main_mailer_type string 'Internet Site'" | debconf-
set-selections \  
&& apt-get install -y \  
libfreetype6-dev \  
libjpeg62-turbo-dev \  
libpng-dev \  
libz-dev \  
less \  
postfix \  
mysql-client \  
libmemcached11 \  
libmemcachedutil2 \  
libmemcached-dev \  
unzip \  
&& docker-php-ext-install -j$(nproc) \  
mysqli \  
pdo \  
pdo_mysql \  
sockets \  
zip \  
&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-
dir=/usr/include/ \  
&& docker-php-ext-install -j$(nproc) gd \  
&& pecl install xdebug-beta \  
&& pecl install memcached \  
&& docker-php-ext-enable xdebug memcached \  
&& apt-get remove -y build-essential libz-dev libmemcached-dev \  
&& apt-get autoremove -y \  
&& apt-get clean  
  
RUN curl https://getcomposer.org/download/$(curl -LSs
https://api.github.com/repos/composer/composer/releases/latest | grep
'tag_name' | sed -e 's/.*: "//;s/".*//')/composer.phar > composer.phar \  
&& chmod +x composer.phar \  
&& mv composer.phar /usr/local/bin/composer \  
&& curl https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-
cli.phar > wp-cli.phar \  
&& chmod +x wp-cli.phar \  
&& mv wp-cli.phar /usr/local/bin/wp  
  
EXPOSE 9000  
  
CMD ["php-fpm"]  
  
RUN curl -L https://phar.phpunit.de/phpunit.phar > /tmp/phpunit.phar \  
&& chmod +x /tmp/phpunit.phar \  
&& mv /tmp/phpunit.phar /usr/local/bin/phpunit  
  
RUN apt-get update && apt-get install -y \  
git \  
subversion \  
wget \  
libxml2-dev \  
ssmtp \  
imagemagick \  
libmagickwand-dev  
  
RUN pecl install imagick  
RUN docker-php-ext-enable imagick  
  
RUN docker-php-ext-install soap  
RUN echo "mailhub=mailcatcher:1025\nUseTLS=NO\nFromLineOverride=YES" >
/etc/ssmtp/ssmtp.conf  
  
RUN apt-get remove -y libmagickwand-dev libxml2-dev && \  
apt-get autoremove -y && \  
apt-get clean  
  
CMD ["php-fpm"]  
  
EXPOSE 9000  

