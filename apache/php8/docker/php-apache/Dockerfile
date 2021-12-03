FROM php:8.0-apache as base

ENV APACHE_DOCUMENT_ROOT /path/to/new/root
ENV PHP_INI_DIR /usr/local/etc/php

RUN apt-get update \
    && apt-get install -y libxml2-dev git zip unzip nano \
	libicu-dev \
    libonig-dev \
	libmcrypt-dev \
	openssl \
    zlib1g-dev \
    libpq-dev \
    libzip-dev \
    libpcre3-dev \
    msmtp vim git cron zip \
    mcrypt \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    && docker-php-ext-install \
    pdo \
    pdo_pgsql \
    pdo_mysql \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/local/bin/ --filename=composer \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && docker-php-ext-install -j$(nproc) iconv \
    #&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

#RUN openssl req -x509 -nodes -days 3650 -newkey rsa:4096 -keyout /etc/ssl/private/ssl-cert-snakeoil.key -out /etc/ssl/certs/ssl-cert-snakeoil.pem -subj "/C=AT/ST=Venezuela/L=Venezuela/O=Security/OU=Development/CN=example.com"

RUN a2enmod rewrite
#RUN a2ensite default-ssl && a2enmod ssl
#RUN pecl install xdebug-2.7.0beta1
#RUN pecl install xdebug-3.1.1
RUN docker-php-ext-enable xdebug

RUN docker-php-ext-install gd
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install soap
RUN docker-php-ext-install zip

ADD php.ini /usr/local/etc/php/

COPY conf/000-default.conf /etc/apache2/sites-available/000-default.conf
#COPY conf/default-ssl.conf /etc/apache2/sites-available/default-ssl.conf

EXPOSE 80
EXPOSE 443