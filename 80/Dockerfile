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
RUN apt-get install php8.0 -y \
  php8.0-common php8.0-cli php8.0-curl php8.0-intl\
  php8.0-bz2  php8.0-mysqli php8.0-mysql  \
  php8.0-fpm php8.0-gd php8.0-mbstring ibapache2-mod-php8.0 \
  php8.0-xdebug php8.0-imap \
  php8.0-ldap
RUN  apt-get update 
RUN apt-get install openssl
RUN apt-get install -y php8.0-xml
RUN apt-get install -y php8.0-zip 
RUN apt-get install -y php8.0-fpm
RUN apt-get install -y php8.0-opcache 

COPY mods-available/suite.com.conf /etc/apache2/sites-available/suite.com.conf
COPY mods-available/php.ini /etc/php/8.0/apache2/php.ini
COPY mods-available/xdebug.ini /etc/php/8.0/mods-available/xdebug.ini
COPY mods-available/apache2.conf /etc/apache2/apache2.conf
RUN chown -R "$APACHE_RUN_USER:$APACHE_RUN_GROUP" /var/www/html/
RUN phpenmod xdebug
RUN a2enmod rewrite
RUN a2ensite suite.com.conf
RUN  a2dissite 000-default.conf
# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer install
RUN composer dumpautoload
#install Node js
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y nodejs \
    npm
WORKDIR  /var/www/html/
#Install Angular and Yarn
RUN npm install -g @angular/cli
RUN npm install --global yarn
RUN npm install n -g
RUN n stable
RUN n latest
RUN export NODE_OPTIONS=--openssl-legacy-provider
#execute it on docker container 
#RUN npm i --only=dev --force
#RUN yarn run build-dev:common
#RUN yarn run build-dev:core
#RUN yarn run build-dev:shell


EXPOSE 80
EXPOSE 9000
CMD apachectl -D FOREGROUND
