FROM openjdk:8-jdk  
  
RUN \  
apt-get update && \  
apt-get install -y unzip  
  
ENV ADMIN_USER admin  
  
ENV PAYARA_PATH /opt/payara5  
  
RUN \  
mkdir -p ${PAYARA_PATH}/deployments && \  
useradd -b /opt -m -s /bin/bash -d ${PAYARA_PATH} payara && echo payara:payara
| chpasswd  
  
# specify Payara version to download  
ENV PAYARA_PKG https://s3-eu-west-1.amazonaws.com/payara.fish/payara-5-web-
prerelease.zip  
ENV PAYARA_VERSION 5-SNAPSHOT  
  
ENV PKG_FILE_NAME payara-web-${PAYARA_VERSION}.zip  
  
# Download Payara Server and install  
RUN \  
wget --quiet -O /opt/${PKG_FILE_NAME} ${PAYARA_PKG} && \  
unzip -qq /opt/${PKG_FILE_NAME} -d /opt && \  
chown -R payara:payara /opt && \  
# cleanup  
rm /opt/${PKG_FILE_NAME}  
  
USER payara  
WORKDIR ${PAYARA_PATH}  
  
# set credentials to admin/admin  
ENV ADMIN_PASSWORD admin  
  
RUN echo 'AS_ADMIN_PASSWORD=\n\  
AS_ADMIN_NEWPASSWORD='${ADMIN_PASSWORD}'\n\  
EOF\n'\  
>> /opt/tmpfile  
  
RUN echo 'AS_ADMIN_PASSWORD='${ADMIN_PASSWORD}'\n\  
EOF\n'\  
>> /opt/pwdfile  
  
# domain1  
RUN ${PAYARA_PATH}/bin/asadmin --user ${ADMIN_USER}
\--passwordfile=/opt/tmpfile change-admin-password && \  
${PAYARA_PATH}/bin/asadmin start-domain domain1 && \  
${PAYARA_PATH}/bin/asadmin --user ${ADMIN_USER} \--passwordfile=/opt/pwdfile
enable-secure-admin && \  
${PAYARA_PATH}/bin/asadmin stop-domain domain1 && \  
rm -rf ${PAYARA_PATH}/glassfish/domains/domain1/osgi-cache  
  
# production domain  
RUN \  
${PAYARA_PATH}/bin/asadmin --user ${ADMIN_USER} \--passwordfile=/opt/tmpfile
change-admin-password --domain_name=production && \  
${PAYARA_PATH}/bin/asadmin start-domain production && \  
${PAYARA_PATH}/bin/asadmin --user ${ADMIN_USER} \--passwordfile=/opt/pwdfile
enable-secure-admin && \  
${PAYARA_PATH}/bin/asadmin stop-domain production && \  
rm -rf ${PAYARA_PATH}/glassfish/domains/production/osgi-cache  
  
# cleanup  
RUN rm /opt/tmpfile  
  
ENV PAYARA_DOMAIN domain1  
ENV DEPLOY_DIR ${PAYARA_PATH}/deployments  
ENV AUTODEPLOY_DIR
${PAYARA_PATH}/glassfish/domains/${PAYARA_DOMAIN}/autodeploy  
  
# Default payara ports to expose  
EXPOSE 4848 8009 8080 8181  
ENV DEPLOY_COMMANDS=${PAYARA_PATH}/post-boot-commands.asadmin  
COPY generate_deploy_commands.sh ${PAYARA_PATH}/generate_deploy_commands.sh  
USER root  
RUN \  
chown -R payara:payara ${PAYARA_PATH}/generate_deploy_commands.sh && \  
chmod a+x ${PAYARA_PATH}/generate_deploy_commands.sh  
USER payara  
  
ENTRYPOINT ${PAYARA_PATH}/generate_deploy_commands.sh &&
${PAYARA_PATH}/bin/asadmin start-domain -v --postbootcommandfile
${DEPLOY_COMMANDS} ${PAYARA_DOMAIN}  

