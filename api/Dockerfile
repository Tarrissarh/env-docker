FROM php:8.1-fpm-alpine

LABEL maintainer="Tarrissarh <tarrissarh@gmail.com>"

ARG USER_NAME
ARG USER_ID
ARG USER_GROUP_NAME
ARG USER_GROUP_ID
ARG API_ENV
ARG API_DIR
ARG API_HOST_DIR
ARG API_REPO
ARG GIT_EMAIL
ARG GIT_NAME

ENV USER_NAME=${USER_NAME:-"tarrissarh"}
ENV USER_ID=${USER_ID:-1000}
ENV USER_GROUP_NAME=${USER_GROUP_NAME:-"tarrissarh"}
ENV USER_GROUP_ID=${USER_GROUP_ID:-1000}
ENV API_ENV=${API_ENV:-"dev"}
ENV API_DIR=${API_DIR:-"/api"}
ENV API_HOST_DIR=${API_HOST_DIR:-"../projects/api"}
ENV API_REPO=${API_REPO:-"git@github.com:Tarrissarh/api.git"}
ENV GIT_EMAIL=${GIT_EMAIL:-"tarrissarh@gmail.com"}
ENV GIT_NAME=${GIT_NAME:-"Tarrissarh"}

# Replace http to https in repo & install apps
RUN sed -i 's/https/http/' /etc/apk/repositories && \
    apk add --no-cache \
        autoconf \
        curl \
        zip \
        unzip \
        wget \
        git \
        nano \
        openssh-client \
        bash \
        libxslt-dev

# Install extensions (02.08.2022 updated)
RUN docker-php-ext-install xsl
# https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions
COPY ./api/install-php-extensions /usr/local/bin/
RUN chmod +x /usr/local/bin/install-php-extensions && \
        install-php-extensions \
        apcu \
        opcache \
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
COPY ./api/php.ini /usr/local/etc/php/php.ini
COPY ./api/conf.d/* /usr/local/etc/php/conf.d/

# Create directory and set current permissions and owners
RUN set -x ; \
    addgroup -g ${USER_GROUP_ID} -S ${USER_GROUP_NAME} && \
    adduser -u ${USER_ID} -D -S -G ${USER_GROUP_NAME} ${USER_NAME} && \
    mkdir -p ${API_DIR} && \
    chown -R ${USER_GROUP_NAME}:${USER_NAME} ${API_DIR} && \
    rm -rf /tmp/* /var/cache/apk/*

RUN curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.alpine.sh' | bash
RUN apk add symfony-cli

WORKDIR ${API_DIR}

USER ${USER_NAME}

#RUN git clone ${API_REPO} && \
#    composer install && \
#    git config --global --add safe.directory ${API_DIR} && \
#    git config --global user.email ${GIT_EMAIL} && \
#    git config --global user.name ${GIT_NAME}

CMD ["php-fpm"]