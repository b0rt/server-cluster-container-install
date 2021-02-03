FROM centos/systemd
ENV container=docker
##
## install nfs , chrony and vim
##
RUN rpm --import https://www.centos.org/keys/RPM-GPG-KEY-CentOS-7 && \
 yum install -y chrony vim && \
 chkconfig chronyd on

RUN yum -y --setopt=tsflags=nodocs install nfs-utils && \
    mkdir -p /opt/kaltura/web && \
    yum clean all	

EXPOSE 111/tcp 111/udp 2049/tcp 2049/udp

RUN mkdir /root/install
COPY ./docker/install/* /root/install/
#COPY ./docker/install/default.config.ans /root/install/default.config.ans
#COPY ./docker/install/nfs_run.sh /root/install/nfs_run.sh
#COPY ./docker/install/nfs_settings.sh /root/install/nfs_settings.sh
#COPY ./docker/install/kaltura.template.ans /root/install/kaltura.template.ans

RUN chmod -R 755 /root/install/

RUN ls /root/install/
##
## configure nfs
# @todo review setup step
##
#RUN /root/install/nfs_settings.sh

##
## entry to bash(run nfs)
##
CMD ["/root/install/nfs_run.sh"]