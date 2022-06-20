# Guide
## Upload images:
`docker-compose pull`
### First init:
`docker-compose up -d --build`
### Other start:
`docker-compose up -d`
### Stop:
`docker-compose down`

_By default, the local development environment is launched. To run a test or production environment, you need to specify the appropriate docker-compose file_
#### Start stage environment:
`docker-compose up -d --build -f docker-compose.stage.yml`
#### Start prod environment:
`docker-compose up -d --build -f docker-compose.prod.yml`

## The development environment includes the following systems by default:
	- php-fpm 8 alpine

## Link by default:
	- ...

Or you can add it to `/etc/hosts` under the desired domains (example for local environment):
```bash
127.0.0.1 tarrissarh.local
```

Add to /etc/hosts to specify base project domains (example for local environment):
```bash
127.0.0.1 api.tarrissarh.local
```