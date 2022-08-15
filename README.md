# Guide

## Upload images:

`docker-compose pull`

### First init:

`docker-compose up -d --build`

### Other start:

`docker-compose up -d`

### Stop:

`docker-compose stop`

### Down:

`docker-compose down`

_By default, the local development environment is launched. To run a test or production environment, you need to specify
the appropriate docker-compose file_

#### Start stage environment:

`docker-compose up -d --build -f docker-compose.stage.yml`

#### Start prod environment:

`docker-compose up -d --build -f docker-compose.prod.yml`

## The development environment includes the following systems by default:

	- php-fpm 8 alpine
    - nginx 1.23 alpine
    - mysql 8
    - redis 7.0 alpine
    - node js 18 alpine
    - mailcatcher

## Link by default:

- [Mailer](http://localhost:1080/)
- [RabbitMQ management](http://localhost:15672/)

Or you can add it to `/etc/hosts` under the desired domains (example for local environment):

```bash
127.0.0.1 tarrissarh.local
```

Add to /etc/hosts to specify base project domains (example for local environment):

```bash
127.0.0.1 api.tarrissarh.local
```