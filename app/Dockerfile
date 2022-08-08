FROM node:18-alpine

LABEL maintainer="Tarrissarh <tarrissarh@gmail.com>"

ARG START
ARG USER_NAME
ARG USER_ID
ARG USER_GROUP_NAME
ARG USER_GROUP_ID
ARG APP_ENV
ARG APP_DIR
ARG APP_HOST_DIR

ENV USER_NAME=${USER_NAME:-"www-data"}
ENV USER_ID=${USER_ID:-1001}
ENV USER_GROUP_NAME=${USER_GROUP_NAME:-"www-data"}
ENV USER_GROUP_ID=${USER_GROUP_ID:-1001}
ENV APP_ENV=${APP_ENV:-"dev"}
ENV APP_DIR=${APP_DIR:-"/app"}
ENV APP_HOST_DIR=${APP_HOST_DIR:-"../projects/app"}

# Create directory and set current permissions and owners
RUN set -x ; \
    addgroup -g ${USER_GROUP_ID} -S ${USER_GROUP_NAME} && \
    adduser -u ${USER_ID} -D -S -G ${USER_GROUP_NAME} ${USER_NAME} && \
    mkdir -p ${APP_DIR} && \
    chown -R ${USER_GROUP_NAME}:${USER_NAME} ${APP_DIR}

WORKDIR ${APP_DIR}

#COPY ${APP_HOST_DIR}/package.json ${APP_HOST_DIR}/package-lock.json ./

#RUN npm config set strict-ssl false && npm i
#RUN npm run build

#COPY ${APP_HOST_DIR}/.dev.yml ${APP_HOST_DIR}/nest-cli.json ${APP_HOST_DIR}/tsconfig-build.json ${APP_HOST_DIR}/tsconfig.json ./
#COPY ${APP_HOST_DIR}/src ./src
#COPY ${APP_HOST_DIR}/test ./test

#CMD ["npm", "run", "start:${APP_ENV}"]