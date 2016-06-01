FROM php:7-fpm
MAINTAINER Don B. Stringham <donbstringham@gmail.com>

# Install modules
RUN apt-get update && apt-get install -y \
    apt-utils \
    autoconf \
    automake \
    build-essential \
    gcc \
    git \
    libpcre3-dev \
    libmcrypt-dev \
    libtool \
    pkg-config \
    wget \
    && docker-php-ext-install mbstring mcrypt opcache pdo_mysql
RUN git clone https://github.com/phpredis/phpredis.git \
    && cd phpredis \
    && git checkout php7 \
    && phpize \
    && ./configure \
    && make && make install \
    && echo "extension=redis.so" > /usr/local/etc/php/conf.d/docker-php-ext-redis.ini \
    && cd .. \
    && rm -fr phpredis
RUN wget -c "http://xdebug.org/files/xdebug-2.4.0.tgz" \
    && tar -xf xdebug-2.4.0.tgz \
    && cd xdebug-2.4.0/ \
    && phpize \
    && ./configure \
    && make && make install \
    && echo "zend_extension=xdebug.so" > /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
#Install composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/bin/composer
ENTRYPOINT ["php-fpm"]
