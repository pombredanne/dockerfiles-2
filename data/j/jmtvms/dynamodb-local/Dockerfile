FROM openjdk:8-jre-slim  
  
LABEL maintainer="joao@miguel.ms"  
LABEL description="DynamoDB Container to be used locally for development"  
LABEL repository="https://github.com/jmtvms/dynamodb-local.git"  
LABEL bugs="https://github.com/jmtvms/dynamodb-local/issues"  
LABEL github="https://github.com/jmtvms/dynamodb-local"  
LABEL version="1.1.0"  
  
ENV DYNAMO_DB_DOWNLOAD_REGION="us-west-2"  
ENV DYNAMO_DB_VERSION="latest"  
ENV
DOWNLOAD_URL="https://s3-${DYNAMO_DB_DOWNLOAD_REGION}.amazonaws.com/dynamodb-
local/dynamodb_local_${DYNAMO_DB_VERSION}.tar.gz"  
ENV JAVA_OPTS=""  
# Installing DynamoDB  
RUN apt-get update  
RUN apt-get install wget -y  
RUN wget ${DOWNLOAD_URL}  
RUN apt-get remove wget -y  
RUN apt-get autoremove -y  
RUN apt-get clean -y  
WORKDIR /opt/dynamodb-local/  
RUN tar zxvf /dynamodb_local_${DYNAMO_DB_VERSION}.tar.gz -C /opt/dynamodb-
local/  
RUN rm /dynamodb_local_${DYNAMO_DB_VERSION}.tar.gz  
RUN mkdir /var/dynamodb-data  
COPY start.sh ./  
RUN chmod +x start.sh  
  
ENTRYPOINT ["./start.sh"]  
CMD ["--sharedDb"]  
  
EXPOSE 8000  
VOLUME [ "/var/dynamodb-data" ]  

