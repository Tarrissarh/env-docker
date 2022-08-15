FROM nginx:1.23-alpine

LABEL maintainer="Tarrissarh <tarrissarh@gmail.com>"

ARG USER_GROUP_ID
ARG USER_GROUP_NAME
ARG USER_ID
ARG USER_NAME
ARG API_HOST
ARG APP_HOST
ARG API_DIR
ARG APP_DIR
ARG ENV_PREFIX

ENV USER_GROUP_ID=${USER_GROUP_ID:-1000}
ENV USER_GROUP_NAME=${USER_GROUP_NAME:-tarrissarh}
ENV USER_ID=${USER_ID:-1000}
ENV USER_NAME=${USER_NAME:-tarrissarh}
ENV API_HOST=${API_HOST:-api.tarrissarh.local}
ENV APP_HOST=${APP_HOST:-tarrissarh.local}
ENV API_DIR=${API_DIR:-"/api"}
ENV APP_DIR=${APP_DIR:-"/app"}
ENV ENV_PREFIX=${ENV_PREFIX:-tarrissarh}

# Remove default project in /var/www/html & install base apps
RUN rm -rf /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh && \
    rm -rf /etc/nginx/conf.d/default.conf && \
    rm -rf /var/www/html && \
    apk add --no-cache \
        nano \
        htop \
        wget \
        curl \
        zip \
        unzip

# @TODO: Доделать....
# Install ssl for local development
#RUN if [[ ${API_ENV} == 'local' || ${API_ENV} == 'dev' ]]; then \
#  apk add --no-cache nss && \
#  curl -JLO "https://dl.filippo.io/mkcert/latest?for=linux/amd64" && \
#  chmod +x mkcert-v*-linux-amd64 && \
#  cp mkcert-v*-linux-amd64 /usr/local/bin/mkcert && \
#  mkcert -install && \
#  mkdir ${SSL_DIR_PATH} && cd ${SSL_DIR_PATH} && \
#  mkcert localhost "*.localhost" local "*.local" 127.0.0.1 ::1 \
#; fi

# Copy hosts
COPY ./server/hosts/api.conf /tmp
COPY ./server/hosts/app.conf /tmp
COPY ./server/nginx.conf /tmp

RUN set -x ; \
    addgroup -g $USER_GROUP_ID -S $USER_GROUP_NAME && \
    adduser -u $USER_ID -D -S -G $USER_GROUP_NAME $USER_NAME && \
    envsubst '${USER_NAME} ${USER_GROUP_NAME}' < /tmp/nginx.conf > /etc/nginx/nginx.conf && rm /tmp/nginx.conf && \
    mkdir -p /var/log/nginx/api && cd /var/log/nginx/api && touch access.log && touch error.log && \
    envsubst '${API_HOST} ${API_DIR} ${ENV_PREFIX}' < /tmp/api.conf > /etc/nginx/conf.d/api.conf && \
    mkdir -p /var/log/nginx/app && cd /var/log/nginx/app && touch access.log && touch error.log && \
    envsubst '${APP_HOST} ${APP_DIR}' < /tmp/app.conf > /etc/nginx/conf.d/app.conf

CMD ["nginx", "-g", "daemon off;"]