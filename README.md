# practica-docker

## EJECUCIÓN:
```bash
docker-compose up
```

## CONFIG:

### Dockerfile:
```dockerfile
FROM ubuntu:20.04

RUN apt update -y

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata && \
    ln -fs /usr/share/zoneinfo/Europe/Madrid /etc/localtime && \
    dpkg-reconfigure --frontend noninteractive tzdata

RUN apt install software-properties-common -y && add-apt-repository ppa:ondrej/php -y
RUN apt install php8.0 libapache2-mod-php8.0 -y

EXPOSE 80
CMD apachectl -D FOREGROUND
```

### docker-compose.yml:
```yaml
version: "3.5"

services:
  apache:
    build:
      context: .
      dockerfile: Dockerfile
    volumes:
      - ./website:/var/www/html
    ports:
      - "80:80"
```
