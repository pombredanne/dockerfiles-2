FROM alpine:edge  
MAINTAINER Wodby <admin@wodby.com>  
  
# Create user www-data  
# RUN addgroup -g 82 -S www-data && \  
# adduser -u 82 -D -S -G www-data www-data  
# Install packages  
# Install packages  
RUN echo 'http://alpine.gliderlabs.com/alpine/edge/main' >
/etc/apk/repositories && \  
echo 'http://alpine.gliderlabs.com/alpine/edge/community' >>
/etc/apk/repositories && \  
echo 'http://alpine.gliderlabs.com/alpine/edge/testing' >>
/etc/apk/repositories && \  
  
apk add \--update \  
libressl \  
ca-certificates \  
git \  
curl \  
wget \  
perl \  
pcre \  
imap \  
imagemagick \  
mariadb-client \  
  
# Temp packages  
build-base \  
autoconf \  
libtool \  
php7-dev \  
pcre-dev \  
imagemagick-dev \  
  
# PHP packages  
php7 \  
php7-fpm \  
php7-opcache \  
php7-session \  
php7-xml \  
php7-ctype \  
php7-ftp \  
php7-gd \  
php7-json \  
php7-posix \  
php7-curl \  
php7-dom \  
php7-pdo \  
php7-pdo_mysql \  
php7-sockets \  
php7-zlib \  
php7-mcrypt \  
php7-mysqli \  
php7-bz2 \  
php7-phar \  
php7-openssl \  
php7-posix \  
php7-zip \  
php7-calendar \  
php7-iconv \  
php7-imap \  
php7-soap \  
php7-dev \  
php7-pear \  
php7-redis \  
php7-mbstring \  
php7-xdebug \  
php7-exif \  
php7-xsl \  
php7-ldap \  
php7-bcmath \  
&& \  
  
# Create symlinks for backward compatibility  
ln -sf /usr/bin/php7 /usr/bin/php && \  
ln -sf /usr/sbin/php-fpm7 /usr/bin/php-fpm && \  
  
# Install imagick  
sed -ie 's/-n//g' /usr/bin/pecl && \  
yes | pecl install imagick && \  
echo 'extension=imagick.so' > /etc/php7/conf.d/imagick.ini  
  
# Install uploadprogess  
RUN cd /tmp/ && wget
https://github.com/Jan-E/uploadprogress/archive/master.zip && \  
unzip master.zip && \  
cd uploadprogress-master/ && \  
phpize7 && ./configure --with-php-config=/usr/bin/php-config7 && \  
make && make install && \  
echo 'extension=uploadprogress.so' > /etc/php7/conf.d/20_uploadprogress.ini &&
\  
cd .. && rm -rf ./master.zip ./uploadprogress-master  
  
# Disable Xdebug  
RUN rm /etc/php7/conf.d/xdebug.ini && \  
# Install Tideaways profiler  
git clone https://github.com/tideways/php-profiler-extension.git
/usr/local/src/php-profiler && \  
cd /usr/local/src/php-profiler && \  
phpize7 && ./configure --with-php-config=/usr/bin/php-config7 && \  
make && make install && \  
echo 'extension=tideways.so' >> /etc/php7/conf.d/20_tideways.ini && \  
echo 'tideways.auto_prepend_library=0' >> /etc/php7/conf.d/20_tideways.ini  
  
# Install composer  
RUN curl -sS https://getcomposer.org/installer | php -- --install-
dir=/usr/local/bin --filename=composer && \  
  
# Add composer parallel install plugin  
composer global require "hirak/prestissimo:^0.3" && \  
  
# Install drush  
php -r "readfile('https://s3.amazonaws.com/files.drush.org/drush.phar');" >
/usr/local/bin/drush && \  
chmod +x /usr/local/bin/drush && \  
  
# Install Drupal Console  
curl https://drupalconsole.com/installer -o /usr/local/bin/drupal && \  
chmod +x /usr/local/bin/drupal && \  
  
# Cleanup  
apk del --purge \  
*-dev \  
build-base \  
autoconf \  
libtool \  
&& \  
  
rm -rf \  
/usr/include/php \  
/usr/lib/php/build \  
/var/cache/apk/* \  
/tmp/* \  
/root/.composer  
  
  
# Configure php.ini  
RUN sed -i \  
-e "s/^expose_php.*/expose_php = Off/" \  
-e "s/^;date.timezone.*/date.timezone = UTC/" \  
-e "s/^memory_limit.*/memory_limit = -1/" \  
-e "s/^max_execution_time.*/max_execution_time = 600/" \  
-e "s/^post_max_size.*/post_max_size = 512M/" \  
-e "s/^upload_max_filesize.*/upload_max_filesize = 512M/" \  
-e "s/^error_reporting.*/error_reporting = E_ALL/" \  
-e "s/^display_errors.*/display_errors = On/" \  
-e "s/^display_startup_errors.*/display_startup_errors = On/" \  
-e "s/^track_errors.*/track_errors = On/" \  
-e "s/^mysqlnd.collect _memory_statistics.*/mysqlnd.collect_memory_statistics = On/" \  
/etc/php7/php.ini && \  
  
echo "error_log = \"/proc/self/fd/2\"" | tee -a /etc/php7/php.ini  
  
# Copy PHP configs  
COPY 00_opcache.ini /etc/php7/conf.d/  
COPY 00_xdebug.ini /etc/php7/conf.d/  
COPY php-fpm.conf /etc/php7/  
  
# Add default drush aliases  
RUN mkdir -p /etc/drush/site-aliases  
COPY default.aliases.drushrc.php /etc/drush/site-aliases/  
  
# Create user www-data  
RUN addgroup -g 82 -S www-data && \  
adduser -u 82 -D -S -G www-data www-data  
  
# Create work dir  
RUN mkdir -p /var/www/html  
WORKDIR /var/www/html  
VOLUME /var/www/html  
EXPOSE 9000  
# Init www-data user  
RUN composer global require hirak/prestissimo:^0.3 --optimize-autoloader && \  
rm -rf ~/.composer/.cache && \  
drupal init --override  
  
CMD composer install -d /xhgui  
# configure xhgui simply adding config file to container  
COPY xhgui-conf/config.php /var/www/xhgui/config/  
COPY docker-entrypoint.sh /usr/local/bin/  
CMD docker-entrypoint.sh  

