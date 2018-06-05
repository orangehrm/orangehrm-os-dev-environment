## Orangehrm open source Development environment
### Introduction
This project will facilitate inbuilt development environment for developers and testers 

#### Technology 
 - Docker
 - Docker compose 
 - Nginx
 - PHP 5.6, PHP 7.0, PHP 7.1, PHP 7.2

### Installation:
 1. Clone this project
 1. Copy the file __.env.dist__ to __.env__ and change (LOCAL_SRC) path to your project path
 1. update /etc/hosts file with following line
 __Example:__
 ```bash
 127.0.0.1	php56 php70 php71 php72
 ```
#### How to up/down containers 
Up all containers
```bash
docker-compose up -d
```
 
Down all container
```bash
docker-compose stop
```
#### Env information 

| PHP Version  | Host | 
| ------------- | ------------- |
| PHP 7.2  | http://php72  | 
| PHP 7.1  | http://php71  | 
| PHP 7.0  | http://php70  | 
| PHP 5.6  | http://php56  | 

### Config & Database

| DB  | Host |User  | Password |
| --- | ---- |---- | ------- |
| Mysql  | mysql  |root  | root  |
| Mysql  | mariadb  |root  | root  |


To use the command line clients provided by the containers you can use the following commands:

```bash
# MySQL
docker-compose exec mysql` mysql -u root -p"root"

# MariaDB
docker-compose exec mariadb -u root -p"root"
```

#### How to browse Orangehrm

- php 5.6 : http://php56/
- php 7.0 : http://php70/
- php 7.1 : http://php71/
- php 7.2 : http://php72/

#### How to execute unit tests
 __Execute Test PHP 7.2:__
 ```bash
 docker-compose exec php-7.2 /bin/bash
 phpunit
 ```
 
  __Execute Test PHP 7.1:__
  ```bash
  docker-compose exec php-7.1 /bin/bash
  phpunit
  ```
  
  __Execute Test PHP 7.0:__
  ```bash
   docker-compose exec php-7.0 /bin/bash
   phpunit
  ```
#### Build Images
```bash
docker-compose -f docker-compose.yml -f docker-compose-build.yml build nginx
```
