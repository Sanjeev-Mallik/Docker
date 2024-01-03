FROM php:7.2-apache

RUN apt-get update && \
apt-get install -y --no-install-recommends \
# Tools
    apt-utils \
# Configure PHP
    libxml2-dev libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install -j$(nproc) mysqli soap gd zip opcache && \
    echo 'always_populate_raw_post_data = -1\nmax_execution_time = 240\nmemory_limit = 512M\nmax_input_vars = 1500\nupload_max_filesize = 200M\npost_max_size = 300M' > /usr/local/etc/php/conf.d/typo3.ini && \
# Configure Apache & clean
    a2enmod rewrite && \
    apt-get clean && \
    apt-get -y purge \
        libxml2-dev libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev && \
    rm -rf /var/lib/apt/lists/* /usr/src/*
# Install ioncube PHP extension
RUN mkdir -p setup && cd setup && \
  curl -sSL https://downloads.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz -o ioncube.tar.gz && \
  tar -xzf ioncube.tar.gz && \
  export PHP_EXT_DIR=$(php-config --extension-dir) && \
  mv ./ioncube/ioncube_loader_lin_7.2.so  $PHP_EXT_DIR/ && \
  echo "zend_extension = $PHP_EXT_DIR/ioncube_loader_lin_7.2.so" >> /usr/local/etc/php/conf.d/docker-php-ext-ioncube.ini && \
  cd .. && rm -rf setup
