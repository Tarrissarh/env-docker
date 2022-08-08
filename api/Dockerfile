FROM php:8.1-fpm-alpine

LABEL maintainer="Tarrissarh <tarrissarh@gmail.com>"

ARG USER_NAME
ARG USER_ID
ARG USER_GROUP_NAME
ARG USER_GROUP_ID
ARG API_ENV
ARG API_DIR
ARG API_HOST_DIR

ENV USER_NAME=${USER_NAME:-"www-data"}
ENV USER_ID=${USER_ID:-1000}
ENV USER_GROUP_NAME=${USER_GROUP_NAME:-"www-data"}
ENV USER_GROUP_ID=${USER_GROUP_ID:-1000}
ENV API_ENV=${API_ENV:-"dev"}
ENV API_DIR=${API_DIR:-"/api"}
ENV API_HOST_DIR=${API_HOST_DIR:-"../projects/api"}

# Replace http to https in repo & install apps
RUN sed -i 's/https/http/' /etc/apk/repositories && \
    apk add --no-cache \
        autoconf \
        curl \
        zip \
        unzip \
        wget \
        git \
        nano

# Install extensions (02.08.2022 updated)
# https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions
COPY ./api/install-php-extensions /usr/local/bin/
RUN chmod +x /usr/local/bin/install-php-extensions && \
        install-php-extensions \
        gd \
        mongodb \
        zip \
        iconv \
        soap \
        sockets \
        intl \
        pdo_mysql \
        pdo_pgsql \
        exif \
        bz2 \
        pcntl \
        http \
        @composer

# Install XDEBUG (only for local/dev environment)
RUN if [[ ${API_ENV} == 'local' || ${API_ENV} == 'dev' ]]; then \
    install-php-extensions xdebug-stable \
; fi

# Some config for php
RUN touch /usr/local/etc/php/conf.d/uploads.ini \
    && echo "upload_max_filesize = 128M;" >> /usr/local/etc/php/conf.d/uploads.ini \
    && echo "post_max_size = 128M;" >> /usr/local/etc/php/conf.d/uploads.ini \
    && echo "memory_limit = 256M;" >> /usr/local/etc/php/conf.d/main.ini

# Create directory and set current permissions and owners
RUN set -x ; \
    addgroup -g ${USER_GROUP_ID} -S ${USER_GROUP_NAME} && \
    adduser -u ${USER_ID} -D -S -G ${USER_GROUP_NAME} ${USER_NAME} && \
    mkdir -p ${API_DIR} && \
    chown -R ${USER_GROUP_NAME}:${USER_NAME} ${API_DIR} && \
    rm -rf /tmp/* /var/cache/apk/*

WORKDIR ${API_DIR}

#COPY ${API_HOST_DIR}/composer.json ./
#RUN composer install

CMD ["php-fpm"]