####################################
# PHPDocker.io PHP 5.6 / CLI image #
####################################

FROM debian:jessie

# Fixes some weird terminal issues such as broken clear / CTRL+L
ENV TERM=linux

RUN apt-get update \
    && apt-get -y --no-install-recommends install \
        curl \
        ca-certificates \
        unzip \
        php5-cli \
        php5-apcu \
        php5-curl \
        php5-json \
        php5-mcrypt \
        php5-readline \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

WORKDIR "/var/www/html"

COPY apps/sugarcron /usr/bin/sugarcron
RUN chmod +x /usr/bin/sugarcron

CMD ["/usr/bin/sugarcron"]
