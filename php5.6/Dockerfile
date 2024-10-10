FROM php:5.6-fpm

RUN echo "deb http://archive.debian.org/debian stretch main" > /etc/apt/sources.list
RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt upgrade -y

RUN apt-get update && \
    apt-get install -yq tzdata && \
    ln -fs /usr/share/zoneinfo/America/New_York /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata

RUN DEBIAN_FRONTEND=noninteractive apt-get update -q \
        && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        libmcrypt-dev libcurl4-openssl-dev libxslt1-dev \
        libpng-dev libjpeg-dev libbz2-dev \
        imagemagick \
        tzdata \
        && ln -fs /usr/share/zoneinfo/Europe/Vienna /etc/localtime \
        && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV TZ="Europe/Vienna"

RUN docker-php-ext-configure mbstring --enable-mbstring \
        && docker-php-ext-configure pdo_mysql --with-pdo-mysql \
        && docker-php-ext-install mbstring mysql fileinfo opcache zip gd \
        && docker-php-ext-install pdo pdo_mysql xml bz2

RUN pecl channel-update pecl.php.net

RUN pecl install apcu-4.0.11 \
    && docker-php-ext-enable apcu

RUN pecl install igbinary-2.0.8 \
    && docker-php-ext-enable igbinary

#todo add user by init script
#RUN useradd --user-group -u 1123 user1