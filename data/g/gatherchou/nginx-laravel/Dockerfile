FROM gatherchou/ubuntu-nginx  
  
RUN apt-get update  
RUN apt-get install -y nginx php-fpm php-mysql php-mbstring  
COPY default /etc/nginx/sites-available/default  
  
RUN apt-get clean && \  
rm -rf /var/lib/apt/lists/*  
  
COPY run.sh /root/run.sh  
RUN chmod +x /root/run.sh  
  
WORKDIR /var/www/html  
  
EXPOSE 80  
CMD /root/run.sh

