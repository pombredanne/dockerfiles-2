FROM php:7.1.0-alpine  
MAINTAINER Adam Kuśmierz <adam@kusmierz.be>  
  
## Install php and dependencies  
RUN set -ex \  
&& apk add --no-cache postgresql-dev sqlite-dev \  
&& docker-php-ext-install pdo pdo_sqlite pdo_mysql pdo_pgsql  
  
## php odbc hack (@see https://github.com/docker-library/php/issues/103)  
RUN set -x \  
&& apk add --no-cache unixodbc-dev ${PHPIZE_DEPS} \  
&& docker-php-source extract \  
&& cd /usr/src/php/ext/odbc \  
&& phpize \  
&& sed -ri 's@^ *test +"\$PHP_.*" *= *"no" *&& *PHP_.*=yes *$@#&@g' configure
\  
&& ./configure --with-unixODBC=shared,/usr \  
&& docker-php-ext-install odbc \  
&& apk del ${PHPIZE_DEPS} \  
&& docker-php-source delete  
  
## Add Tini  
RUN apk add --no-cache tini  
ENTRYPOINT ["/sbin/tini", "--"]  
  
## Add the files  
ADD php.ini /usr/local/etc/php/conf.d/php.ini  
  
## install adminer and default theme  
RUN mkdir -p /var/www  
ADD http://www.adminer.org/latest.php /var/www/index.php  
ADD https://raw.github.com/vrana/adminer/master/designs/hever/adminer.css
/var/www/adminer.css  
RUN chown www-data:www-data -R /var/www  
  
## Expose the port  
EXPOSE 80  
CMD php -S 0.0.0.0:80 -t /var/www/  

