# Docker Files

Dockerfiles to deploy.


## Installation

1. Move all proyects to same directory like:
dl/api
dl/admin
```sh
mkdir dl
mv api dl/api
```
2. Copy Dockerfile, docker-compose.yml and 000-default.conf from proyect directory (dl_docker/api) to new location directory (dl/api).
```sh
cp Dockerfile docker-compose.yml 000-default.conf dl/api/
```
3. Copy dl_docker/docker-compose.yml to dl/docker-compose.yml
```sh
cp dl_docker/docker-compose.yml 000-default.conf dl/docker-compose.yml
```
4. Give full access to storage folders inside each proyect directory (only development)
```sh
sudo chmod -R 777 api/storage
```

## Start and Stop
On container directory.
- Start
```sh
docker compose up -d
```
- Stop
```sh
docker compose down -d
```
- Restart
```sh
docker compose restart
```

## From the scratch

When you begin from a new instalacion of a proyect you need install all laravel dependensis from inside of container
```sh
docker exec -it api bin/bash
cd /var/www/html
composer install
```

## Database config .env

You need change datebase host on .env file
- From localhost or IP
```sh
DB_HOST=localhost
```
- TO mysql container name
```sh
DB_HOST=mysql
```