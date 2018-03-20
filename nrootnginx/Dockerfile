FROM debian:jessie

MAINTAINER NGINX Docker Maintainers "docker-maint@nginx.com"

ENV NGINX_VERSION 1.10.3-1~jessie

RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62 \
	&& echo "deb http://nginx.org/packages/debian/ jessie nginx" >> /etc/apt/sources.list \
	&& apt-get update \
	&& apt-get install --no-install-recommends --no-install-suggests -y \
						ca-certificates \
						nginx=${NGINX_VERSION} \
						nginx-module-xslt \
						nginx-module-geoip \
						nginx-module-image-filter \
						nginx-module-perl \
						nginx-module-njs \
						gettext-base \
	&& rm -rf /var/lib/apt/lists/*

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log

COPY nginx.conf /etc/nginx/nginx.conf
COPY default.conf /etc/nginx/conf.d/default.conf
COPY index.html /usr/share/nginx/html/index.html

EXPOSE 8080 8443

RUN chgrp -R 0 /var/cache/nginx
RUN chmod -R g+rw /var/cache/nginx
RUN find /var/cache/nginx -type d -exec chmod g+x {} +

RUN chgrp -R 0 /etc/nginx
RUN chmod -R g+rw /etc/nginx
RUN find /etc/nginx -type d -exec chmod g+x {} +

RUN chgrp -R 0 /usr/share/nginx/html
RUN chmod -R g+rw /usr/share/nginx/html
RUN find /usr/share/nginx/html -type d -exec chmod g+x {} +

RUN chgrp -R 0 /var/run
RUN chmod -R g+rw /var/run
RUN find /var/run -type d -exec chmod g+x {} +

USER 1001

CMD ["nginx", "-g", "daemon off;"]