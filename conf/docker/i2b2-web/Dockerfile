#adpted from https://raw.githubusercontent.com/CentOS/CentOS-Dockerfiles/master/httpd/centos7/Dockerfile
FROM centos:latest
MAINTAINER <Kevin Mullins>

#LABEL Vendor="CentOS" \
#        License=GPLv2 \
#        Version=2.4.6-40



RUN yum -y update && yum clean all
RUN yum -y install httpd mod_ssl php && yum clean all

#RUN yum -y --setopt=tsflags=nodocs update && \
#      yum -y --setopt=tsflags=nodocs install httpd && \
#      yum clean all

EXPOSE 80 443 8080

# Simple startup script to avoid some issues observed with container restart 
ADD run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh


ADD ../../httpd/i2b2_proxy.conf /etc/httpd/conf.d/i2b2_proxy.conf
ADD ../../httpd/i2b2_proxy.conf /conftemp/etc/httpd/conf.d/i2b2_proxy.conf

ADD ../../webclient /var/www/html/webclient/
ADD ../../webclient /conftemp/var/www/html/webclient/

ADD ../../admin /var/www/html/admin/
#ADD ../../admin /conftemp/var/www/html/admin/

ENV APP_IP ${APP_IP:-i2b2-wildfly}

COPY prescript.sh /
RUN chmod -v +x /prescript.sh

CMD ["/run-httpd.sh"]
