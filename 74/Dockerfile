FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update
RUN apt-get install vim -y
RUN apt-get install apt-utils -y
RUN apt-get update
RUN apt-get install apache2 -y
RUN apt-get install software-properties-common -y
RUN add-apt-repository ppa:ondrej/php
RUN apt-get install curl
RUN apt-get update
RUN apt-get install php7.4 -y \
  php7.4-common php7.4-cli php7.4-curl php7.4-intl\
  php7.4-bz2  php7.4-mysqli php7.4-mysql  \
  php7.4-fpm php7.4-gd php7.4-mbstring ibapache2-mod-php7.4 \
  php7.4-xdebug php7.4-imap \
  php7.4-ldap
RUN  apt-get update 
RUN apt-get install openssl
RUN apt-get install -y php7.4-xml
RUN apt-get install -y php7.4-zip 
RUN apt-get install -y php7.4-fpm
RUN apt-get install -y php7.4-opcache 

COPY mods-available/suite.com.conf /etc/apache2/sites-available/suite.com.conf
COPY mods-available/php.ini /etc/php/7.4/apache2/php.ini
COPY mods-available/xdebug.ini /etc/php/7.4/mods-available/xdebug.ini
COPY mods-available/apache2.conf /etc/apache2/apache2.conf
RUN chown -R "$APACHE_RUN_USER:$APACHE_RUN_GROUP" /var/www/html/
RUN phpenmod xdebug
RUN a2enmod rewrite
RUN a2ensite suite.com.conf
RUN  a2dissite 000-default.conf
WORKDIR  /var/www/html/

EXPOSE 80
EXPOSE 9000
CMD apachectl -D FOREGROUND
