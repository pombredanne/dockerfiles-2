FROM alpine:3.6  
  
RUN cd /tmp \  
&& apk add --no-cache curl \  
&& curl -L http://cs.sensiolabs.org/download/php-cs-fixer-v2.phar > cs-
fixer.phar \  
&& curl -LO http://get.sensiolabs.de/deptrac.phar \  
&& curl -L http://www.phing.info/get/phing-latest.phar > phing.phar \  
&& curl -LO https://getcomposer.org/download/1.6.3/composer.phar \  
&& curl -LO
https://github.com/borisrepl/boris/releases/download/v1.0.7/boris.phar \  
&& curl -LO
https://github.com/phpstan/phpstan/releases/download/0.9.2/phpstan.phar \  
&& curl -L https://phar.phpunit.de/phpunit-5.7.phar > phpunit.phar \  
&& chmod +x /tmp/*  
  
  
FROM 1maa/php:5.6  
  
COPY etcdev /etc/php  
  
COPY --from=0 /tmp/* /usr/local/bin/  

