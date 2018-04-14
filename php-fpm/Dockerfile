#
#--------------------------------------------------------------------------
# Image Setup
#--------------------------------------------------------------------------

FROM php:7.2.4-fpm-alpine3.7

#
#--------------------------------------------------------------------------
# Mandatory Software's Installation
#--------------------------------------------------------------------------
RUN apk add --no-cache libmemcached-dev \
    zlib-dev \
    postgresql-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    freetype-dev \
    libmcrypt-dev \
    shadow

# Install the PHP pdo_mysql extention
RUN docker-php-ext-install pdo_mysql \
    # Install the PHP pdo_pgsql extention
    && docker-php-ext-install pdo_pgsql \
    # Install the PHP gd library
    && docker-php-ext-configure gd \
        --enable-gd-native-ttf \
        --with-jpeg-dir=/usr/lib \
        --with-freetype-dir=/usr/include/freetype2 \
    && docker-php-ext-install gd


#--------------------------------------------------------------------------
# Optional Software's Installation
#--------------------------------------------------------------------------
#
# Optional Software's will only be installed if you set them to `true`
# in the `docker-compose.yml` before the build.
# Example:
#   - INSTALL_ZIP_ARCHIVE=true
#

###########################################################################
# Check PHP version:
###########################################################################

ARG PHP_VERSION=7.2

RUN php -v | head -n 1 | grep -q "PHP ${PHP_VERSION}."

#
#--------------------------------------------------------------------------
# Final Touch
#--------------------------------------------------------------------------
#

COPY ./laravel.ini /usr/local/etc/php/conf.d
COPY ./xlaravel.pool.conf /usr/local/etc/php-fpm.d/

USER root

RUN usermod -u 82 www-data

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000
