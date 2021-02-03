##
##Dockerfile
##
FROM centos/systemd

##
## facilities
##
RUN rpm --import https://www.centos.org/keys/RPM-GPG-KEY-CentOS-7 && \
 yum install -y memcached chrony postfix && \
 chkconfig memcached on && \
 chkconfig chronyd on && \
 chkconfig postfix on && \
 sed -i 's@^inet_protocols = all@inet_protocol = ipv4@g' /etc/postfix/main.cf

# eror when enabled: Failed to get D-Bus connection: Operation not permitted
#RUN systemctl start memcached && \
# systemctl start postfix start && \
# systemctl start chronyd
##
## Kaltura
##
RUN rpm --import http://installrepo.kaltura.org/releases/RPM-GPG-KEY-kaltura-curr && \
 rpm -ihv http://installrepo.kaltura.org/releases/kaltura-release.noarch.rpm && \
 yum install -y kaltura-postinst kaltura-base && \
 yum install -y vim dos2unix

COPY ./docker/install/* /root/install/
RUN chmod -R 755 /root/install/

EXPOSE 80 443 1935 88 8443

# start services
CMD ["/sbin/init"]