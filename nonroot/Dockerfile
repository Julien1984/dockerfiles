FROM centos:centos7
MAINTAINER Pawel M <lolo78@o.pl2>

RUN yum -y --setopt=tsflags=nodocs update && \
    yum -y --setopt=tsflags=nodocs install epel-release && \
    yum -y --setopt=tsflags=nodocs install nginx && \
    yum clean all


ADD nginx.conf /etc/nginx/nginx.conf

#  for some reason nginx is still trying to create /var/log/nginx/error.log
#  even if error_log /dev/stderr is set
RUN chmod -R go+rwx /var/log/nginx

# copy swagger files to the `/js` folder
ADD ./dist/* /usr/share/nginx/html
#ADD ./docker-run.sh /usr/share/nginx/


EXPOSE 8080
RUN chmod -R go+rwx /var/lib/nginx

USER 997

ENTRYPOINT [ "/usr/sbin/nginx" ]
