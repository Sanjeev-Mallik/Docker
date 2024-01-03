FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update
RUN apt-get install vim -y
RUN apt-get install apt-utils -y
RUN apt-get update
RUN apt-get install apache2 -y
RUN apt-get install software-properties-common -y
RUN add-apt-repository ppa:ondrej/php
RUN apt-get update
RUN apt-get install php7.1 -y \
  libapache2-mod-php7.1 php7.1-mcrypt \
  php7.1-cli php7.1-xml php7.1-zip php7.1-mysql php7.1-gd \
  php7.1-imagick php7.1-recode php7.1-tidy php7.1-xmlrpc \
  php7.1-gmp php7.1-bcmath php7.1-curl \
  php7.1-mbstring php7.1-imap \
  php7.1-sybase freetds-common freetds-bin \
  php7.1-xdebug

COPY php.ini /etc/php/7.1/apache2/php.ini
COPY apache2.conf /etc/apache2/apache2.conf
COPY mods-available/xdebug.ini /etc/php/7.1/mods-available/xdebug.ini

RUN chown -R "$APACHE_RUN_USER:$APACHE_RUN_GROUP" /var/www/html/
RUN phpenmod xdebug
RUN a2enmod rewrite

EXPOSE 80
EXPOSE 9000
CMD apachectl -D FOREGROUND
