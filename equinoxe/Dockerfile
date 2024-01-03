FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y
RUN apt-get install vim curl unzip zip -y
RUN apt-get install apt-utils -y
RUN apt-get update -y
RUN apt-get install apache2 -y
RUN apt-get install software-properties-common -y
RUN add-apt-repository ppa:ondrej/php && apt-get update
RUN apt-get install php7.1 -y \
  libapache2-mod-php7.1 php7.1-mcrypt \
  php7.1-cli php7.1-xml php7.1-zip php7.1-mysql php7.1-gd \
  php7.1-imagick php7.1-recode php7.1-tidy php7.1-xmlrpc \
  php7.1-gmp php7.1-bcmath php7.1-curl \
  php7.1-mbstring php7.1-imap \
  php7.1-sybase freetds-common freetds-bin \
  php7.1-xdebug \
  php7.1-redis

COPY config/sites-available/000-default.conf /etc/apache2/sites-enabled/000-default.conf
COPY config/php.ini /etc/php/7.1/apache2/php.ini
COPY config/apache2.conf /etc/apache2/apache2.conf
COPY config/mods-available/xdebug.ini /etc/php/7.1/mods-available/xdebug.ini
COPY config/mods-available/redis.ini /etc/php/7.1/mods-available/redis.ini
COPY config/mods-available/dir.conf /etc/apache2/mods-available/dir.conf

# Install composer
ENV COMPOSER_HOME /composer
ENV PATH ./vendor/bin:/composer/vendor/bin:$PATH
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer

# Install PHP_CodeSniffer
RUN composer global require "squizlabs/php_codesniffer=*" -d /var/www/html

RUN chown -R "www-data:www-data" /var/www/html/
RUN phpenmod xdebug
RUN phpenmod redis
RUN a2enmod rewrite

EXPOSE 80
EXPOSE 9000
# By default, simply start apache.
CMD apachectl -D FOREGROUND
