FROM php:5.6-fpm-alpine

RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli

# Set timezone
ENV TZ=Europe/Brussels
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
COPY php.ini /usr/local/etc/php/php.ini
COPY www.conf /usr/local/etc/php-fpm.d/www.conf



# Create users, directories and update permissions
RUN addgroup -g 1000 app \
    && adduser -D -H -h /var/www/html -s /sbin/nologin -G app -u 1000 app \
    && mkdir -p /var/www/html /sock /var/log/php \
    && chown -R app:app /var/www/html /usr/local/etc /sock /var/log/php

# Change owner and group
USER app:app

# Change workdir
WORKDIR /var/www/html

# Expose port 9000
EXPOSE 9000