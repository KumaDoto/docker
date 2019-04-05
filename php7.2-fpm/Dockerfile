FROM php:7.2-fpm

##install php-lib
RUN apt-get update  \
    && apt-get install -y --no-install-recommends \
    git \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libpcre3-dev \
    libxml2-dev \
    zlib1g-dev \
    gcc \
    libmcrypt-dev \
    libpq-dev \
    libssl-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \   
    && docker-php-ext-install mbstring \
    && docker-php-ext-install pdo pdo_mysql pdo_pgsql\
    && docker-php-ext-install mysqli \
    && docker-php-ext-install zip xml

#pecl install lib
RUN pecl install mcrypt-1.0.1 mongodb xdebug \
    && echo "extension=mcrypt.so" > /usr/local/etc/php/conf.d/mcrypt.ini \
    && echo "extension=mongodb.so" > /usr/local/etc/php/conf.d/mongo.ini \
    && echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20170718/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini

    #compile phalcon
RUN git clone --depth 1 -b 3.4.x https://github.com/phalcon/cphalcon /cphalcon \
    && cd /cphalcon/build \
    && ./install \
    && echo "extension=phalcon.so" > /usr/local/etc/php/conf.d/phalcon.ini

#install composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

#clean
RUN rm -rf /cphalcon
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN rm -rf /root/.cache