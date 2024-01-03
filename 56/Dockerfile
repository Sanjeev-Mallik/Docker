FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update
RUN apt-get install vim -y
RUN apt-get install apt-utils -y
RUN apt-get install apache2 -y
RUN apt-get install software-properties-common -y
RUN add-apt-repository ppa:ondrej/php
RUN apt-get update
RUN apt-get install php5.6 php5.6-dev -y \
  libapache2-mod-php5.6 php5.6-mcrypt \
  php5.6-cli php5.6-xml php5.6-zip php5.6-mysql php5.6-gd \
  php5.6-imagick php5.6-recode php5.6-tidy php5.6-xmlrpc \
  php5.6-gmp php5.6-bcmath php5.6-curl \
  php5.6-mbstring php5.6-imap \
  php5.6-sybase freetds-common freetds-bin \
  php5.6-xdebug php5.6-xhprof

COPY php.ini /etc/php/5.6/apache2/php.ini
COPY apache2.conf /etc/apache2/apache2.conf

COPY mods-available/xdebug.ini /etc/php/5.6/mods-available/xdebug.ini
COPY mods-available/xhprof.ini /etc/php/5.6/mods-available/xhprof.ini
RUN phpenmod xdebug
RUN phpenmod xhprof

RUN chown -R "$APACHE_RUN_USER:$APACHE_RUN_GROUP" /var/www/html/

RUN a2enmod rewrite

WORKDIR "/var/www/html"

EXPOSE 80
EXPOSE 9000
CMD apachectl -D FOREGROUND
