FROM centos:centos7
MAINTAINER Pawel M <lolo78@o.pl2>

RUN yum -y --setopt=tsflags=nodocs update && \
    yum -y --setopt=tsflags=nodocs install epel-release && \
    yum -y --setopt=tsflags=nodocs install nginx && \
    yum clean all


ADD nginx.conf /etc/nginx/nginx.conf
RUN mkdir -p /usr/share/nginx/html
RUN chmod -R go+rwx /usr/share/nginx/html

#  for some reason nginx is still trying to create /var/log/nginx/error.log
#  even if error_log /dev/stderr is set
RUN chmod -R go+rwx /var/log/nginx

# copy swagger files to the `/js` folder
ADD ./dist/* /usr/share/nginx/html/
#copy  json files
RUN mkdir -p /usr/share/nginx/html/json
RUN chmod -R go+rwx /usr/share/nginx/html/json
ADD ./json/* /usr/share/nginx/html/json
#ADD ./docker-run.sh /usr/share/nginx/


EXPOSE 8080
RUN chmod -R go+rwx /var/lib/nginx

USER 997

ENTRYPOINT [ "/usr/sbin/nginx" ]
