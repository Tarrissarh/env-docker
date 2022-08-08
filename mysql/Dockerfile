FROM mysql:8.0

LABEL maintainer="Tarrissarh <tarrissarh@gmail.com>"

ARG MYSQL_PORT
ARG TIMEZONE

ENV MYSQL_PORT=${MYSQL_PORT:-3306}
ENV TIMEZONE=${TIMEZONE:-"UTC"}

RUN ln -snf /usr/share/zoneinfo/$TIMEZONE /etc/localtime && echo $TIMEZONE > /etc/timezone && chown -R mysql:root /var/lib/mysql/

COPY ./env/mysql/my.cnf /etc/mysql/conf.d/my.cnf

RUN chmod 0444 /etc/mysql/conf.d/my.cnf

EXPOSE ${MYSQL_PORT}

CMD ["mysqld"]
