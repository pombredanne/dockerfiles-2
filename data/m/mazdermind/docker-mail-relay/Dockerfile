FROM alpine:latest  
MAINTAINER Michael Struski <michael@struscode.com>  
  
# Packages: update  
RUN apk --no-cache add postfix ca-certificates libsasl py-pip supervisor
rsyslog  
RUN pip install j2cli  
  
# Add files  
ADD conf /root/conf  
RUN mkfifo /var/spool/postfix/public/pickup \  
&& ln -s /etc/postfix/aliases /etc/aliases  
  
# Configure: supervisor  
ADD bin/dfg.sh /usr/local/bin/  
ADD conf/supervisor-all.ini /etc/supervisor.d/  
  
# Runner  
ADD run.sh /root/run.sh  
RUN chmod +x /root/run.sh  
  
# Declare  
EXPOSE 25  
CMD ["/root/run.sh"]  

