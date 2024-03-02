Docker app for PHP, MySQL, NGINX. REDIS, xDebug, phpMyAdmin and multi stage building
==================================

# Short Description

This docker app provides the installation of PHP, MySQL, Redis, xDebug, phpMyAdmin.

Important is to know that this docker app provides the ability for installation with multi stage building

This means that the development environment is a copy of productin enviroment but with additional installation of xDebug and phpMAdmin. You can see it in `php/Dockerfile`

Multi stage building provides the ability of building different environments which are copy of each other but with additional or less settings.


# How to run

Production:
  * Set the environment settings in `.env`
  * Run in your terminal: `docker compose up --build -d`

Development:
  * Set the environment settings in `.env.local`
  * Simply run the command in your terminal -> `sh ./bin/dev-mode.sh -d` You can place also other flags like --build -d at the end of the command.
  * To enable xDebug run the command like this -> `XDEBUG_MODE=debug sh ./bin/dev-mode.sh -d`
  * Check your installation in your browser: `localhost`
  * phpMyAdmin ist available: `http://localhost:4000/`

General:
`app/public` is the entry folder and contains the index.php

You can install any project with composer to this folder. Place your composer.json and run it.
Due to your project could it be necessarey that some changes in Dockerfiles of nginx and php have to be done before executing composer install command.


# Docker compose cheatsheet

  * Start containers in the background: `docker compose up -d`
  * Rebuild changes in dockerfile or build images: `docker compose up --build -d`
  * Start containers on the foreground: `docker compose up`. You will see a stream of logs for every container running.
  * Stop containers: `docker compose stop`
  * Stops containers and removes containers, networks, volumes, and images created by up: `docker compose down`
  * View container logs: `docker compose logs`
  * Execute command inside of container: `docker exec -it SERVICE_NAME COMMAND sh` where `COMMAND` is whatever you want to run. Examples:
        * Shell into the PHP container, `docker exec -it php-docker-app-1 sh`
        * Open a mysql shell, `php-docker-db-1 mysql -uroot -p sh`

# Docker general cheatsheet

**Note:** these are global commands and you can run them from anywhere.

  * To clear containers: `docker rm -f $(docker ps -a -q)`
  * To clear images: `docker rmi -f $(docker images -a -q)`
  * To clear volumes: `docker volume rm $(docker volume ls -q)`

