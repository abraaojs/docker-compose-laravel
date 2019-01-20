Creat by Abraão Silva
Date 18 Jan 2019 
# Description (How To)

Docker using the compose, configuration file with environment variables, creating a nginx container 1.13.3 and a php container 7.1.9-fpm linked through a link and creating a mysql container 5.7.19. Laravel version 5.5.22

# Nginx Container Configuration

1. Expose Ports

	80 e 443

2. Volume (Note: in the configuration of docker -> shared drivers, the c: and / or d: drives are enabled, for Windows)

	Application: htdocs -> /var/www/html
	
	Logs: nginx/logs -> /var/log/nginx
	
	Virtual Host: nginx/sites -> /etc/nginx/conf.d
	
3. Virtual Host

	Creating the vhost template http://api.dev (vhost modifiable)

# Php Container Configuration

1. Expose Ports Back-End

	9000

2. Volume (Note: in the configuration of docker -> shared drivers, the c: and / or d: drives are enabled, for Windows)

	Application: htdocs -> /var/www/html
	
3. Libraries

	Enabling php libraries via configuration file. Ex: MBSTRING, GD, MCRYPT, PDO_MYSQL, etc..
	
# Configuring Mysql Container

1. Expose Ports

	3306

2. Volume (Note: in the configuration of docker -> shared drivers, the c: and / or d: drives are enabled, for Windows)

	Application: mysql/data -> /var/lib/mysql

3. Connection setup

	- MYSQL_DATABASE      = default
    - MYSQL_USER          = default
    - MYSQL_PASSWORD      = secret
    - MYSQL_ROOT_PASSWORD = root
    - MYSQL_PORT          = 3306
	
# How to use and Execute

1. Clone the repository using the command:

   git clone https://github.com/abraaojs/docker-compose-laravel

2. Enter the docker-compose-laravel folder and copy the env-example file to .env.

   cp env-example .env

3. Rode seu container:

   docker-compose up -d

4. Add domains hosts file to Windows | Linux | MacOS

   127.0.0.1 localhost

   127.0.0.1 api.dev

5. Access the container shell (Check):
    
	docker exec -it nginx bash

	docker exec -it php-fpm bash
	
	docker exec -it mysql bash
   
6. Getting started for running Laravel on localhost:

	Access the folder cd /var/www/html
	
	Run command to create laravel vendor folder: composer install
	
	Run command to create file for laravel environment variables: cp .env.example .env
	
	Run command to generate keys needed to run laravel: php artisan key: generate

7. Getting started for running Laravel on api.dev:

	Access the api.dev folder: cd /var/www/html/api.dev
	
	Run command to create laravel vendor folder: composer install
	
	Run command to create file for laravel environment variables: cp .env.example .env
	
	Run command to generate keys needed to run laravel: php artisan key: generate
	
8. Open in browser

   http://localhost

   http://api.dev

9. Access the database inside the Mysql container

	mysql -u root -p

10. Basic commands for using the database

	show databases;

	CREATE DATABASE teste;
	
	use teste;
	
	show tables;