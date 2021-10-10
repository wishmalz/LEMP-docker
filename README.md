# LEMP stack in docker
## What is LEMP stack?
Programs underlying the LEMP stack are:
* L = Linux
* E = Nginx 
* M = MySQL 
* P = PHP
## Containers
We need following containers for LEMP stack:
* Linux (Nginx)
* PHP ([PHP-FPM](https://php-fpm.org/))
* MySQL
* phpMyAdmin

Images is using alpine versions.
## Requirements
1. Computer
2. Docker
3. [Docker Compose](https://docs.docker.com/compose/)
## Settings
You can write source code in `src` folder. You can change this in `docker-compose.yaml` file.
### Docker compose
Docker compose config is in file `docker-compose.yaml`. PHP Dockerfile is in `.docker/php/Dockerfile`.
All configurations is in `.docker` folder.
### Domain name
You need to add `server_name`'s to your hosts file.

server_name for PHP container is `php.test`(`.docker/nginx/conf.d/php.conf`)
server_name for phpMyAdmin container is `pma.test`(`.docker/nginx/conf.d/phpmyadmin.conf`)

Where is hosts file?
* UNIX: `/etc/hosts`
* Windows: `c:\windows\system32\drivers\etc\hosts`

You need to add lines like this: `127.0.0.1 php.test`
### Env
1. Rename `.env.example` to `.env`
2. In `.env` set `COMPOSE_PROJECT_NAME=example` variable.

Why you need this? By assigning a unique name to your project, you ensure that no name collision will happen with 
other ones. If there are multiple Docker-based projects on your system that share the same name or directory name, 
and more than one use a service called `nginx`, Docker may complain that another container named `example_nginx` already 
exists when you bring up a Docker environment.
Don't forget to add your `.env` to a `.gitignore`.
## Installation
1. Open terminal in folder where you put this project.
2. Type `docker compose up -d --build`
3. Go to [http://php.test/](http://php.test/) and [http://pma.test/](http://pma.test/) in browser
## Useful commands
* Start containers `docker compose up -d`
* Stop containers `docker compose down`
* Stop and/or destroy the containers and their volumes `docker compose down -v`
* Delete everything, including images and orphan containers `docker compose down -v --rmi all --remove-orphans`