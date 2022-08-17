# syntax=docker/dockerfile:1
FROM debian:11
RUN apt-get update -y && apt-get install -y nginx apache2 php libapache2-mod-php
RUN rm /etc/nginx/sites-available/default && rm -r /var/www/*
RUN rm /etc/apache2/sites-available/000-default.conf && rm /etc/apache2/ports.conf
COPY default /etc/nginx/sites-available/
COPY static /etc/nginx/sites-available/
COPY 000-default.conf /etc/apache2/sites-available/
COPY ports.conf /etc/apache2/

#configure apache2 vars
ENV APACHE_RUN_USER  www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR   /var/log/apache2
ENV APACHE_PID_FILE  /var/run/apache2/apache2.pid
ENV APACHE_RUN_DIR   /var/run/apache2
ENV APACHE_LOCK_DIR  /var/lock/apache2
ENV APACHE_LOG_DIR   /var/log/apache2
RUN ln -s /etc/nginx/sites-available/static /etc/nginx/sites-enabled/static
RUN echo 'ServerName localhost' >> /etc/apache2/apache2.conf
COPY www /var/www
RUN service apache2 restart
EXPOSE 80 81 82 83 84
ENTRYPOINT ["nginx", "-g", "daemon off;"]