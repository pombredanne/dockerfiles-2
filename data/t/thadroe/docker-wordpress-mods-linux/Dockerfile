FROM php:7.1-apache  
  
# install the PHP extensions we need  
RUN set -ex; \  
\  
apt-get update; \  
apt-get install -y \  
libjpeg-dev \  
libpng-dev \  
; \  
rm -rf /var/lib/apt/lists/*; \  
\  
docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr; \  
docker-php-ext-install gd mysqli opcache  
# TODO consider removing the *-dev deps and only keeping the necessary lib*
packages  
# set recommended PHP.ini settings  
# see https://secure.php.net/manual/en/opcache.installation.php  
RUN { \  
echo 'opcache.memory_consumption=128'; \  
echo 'opcache.interned_strings_buffer=8'; \  
echo 'opcache.max_accelerated_files=4000'; \  
echo 'opcache.revalidate_freq=2'; \  
echo 'opcache.fast_shutdown=1'; \  
echo 'opcache.enable_cli=1'; \  
} > /usr/local/etc/php/conf.d/opcache-recommended.ini  
  
RUN a2enmod rewrite expires  
  
# Begin mod  
# Generate self-signed certs and enable ssl module  
RUN openssl req \  
-new \  
-newkey rsa:2048 \  
-days 365 \  
-nodes \  
-x509 \  
-subj "/C=DE/ST=Berlin/L=Berlin/O=gesellix/CN=${DOMAIN} CA" \  
-keyout /etc/ssl/private/ssl-cert-snakeoil.key \  
-out /etc/ssl/certs/ssl-cert-snakeoil.pem  
RUN a2enmod ssl  
RUN a2ensite default-ssl.conf  
  
# Custom user and group for apache  
RUN sed -i 's/www-data/user/g' /etc/apache2/envvars  
RUN useradd -M -u 1000 user  
RUN chown -R user:user /var/www/html  
RUN service apache2 restart  
  
# Install wp-cli  
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-
cli.phar \  
&& chmod +x wp-cli.phar \  
&& mv wp-cli.phar /usr/local/bin/wp  
  
# End mod  
VOLUME /var/www/html  
  
ENV WORDPRESS_VERSION 4.9.4  
ENV WORDPRESS_SHA1 0e630bf940fd586b10e099cd9195b3e825fb194c  
  
RUN set -ex; \  
curl -o wordpress.tar.gz -fSL
"https://wordpress.org/wordpress-${WORDPRESS_VERSION}.tar.gz"; \  
echo "$WORDPRESS_SHA1 *wordpress.tar.gz" | sha1sum -c -; \  
# upstream tarballs include ./wordpress/ so this gives us /usr/src/wordpress  
tar -xzf wordpress.tar.gz -C /usr/src/; \  
rm wordpress.tar.gz; \  
# Begin mod  
chown -R user:user /usr/src/wordpress  
# End mod  
COPY docker-entrypoint.sh /usr/local/bin/  
  
ENTRYPOINT ["docker-entrypoint.sh"]  
CMD ["apache2-foreground"]  

