FROM prima/elixir-official:1.5.3-2  
RUN apt-get update && \  
apt-get install -qqy mysql-client && \  
cp /usr/share/zoneinfo/Europe/Rome /etc/localtime && \  
echo "Europe/Rome" > /etc/timezone && \  
date && \  
rm -rf /var/lib/apt/lists/*  
  
COPY files/entrypoint.sh /entrypoint.sh  
  
ENTRYPOINT ["/entrypoint.sh"]  

