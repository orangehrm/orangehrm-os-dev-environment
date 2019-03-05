## Orangehrm open source Development environment
### Introduction
This project will facilitate inbuilt development environment for developers and testers 

#### Technology 
 - Docker
 - Docker compose 
 - Nginx
 - PHP 5.6, PHP 7.0, PHP 7.1, PHP 7.2, PHP 7.3

### Installation:
 1. Clone this project
 1. Copy the file __.env.dist__ to __.env__ and change (LOCAL_SRC) path to your project path
 1. update /etc/hosts file with following line
 __Example:__
 ```bash
 127.0.0.1	php56 php70 php71 php72 php73
 ```
#### How to up/down containers 
Up all containers
```bash
docker-compose up -d
```

Up only development containers 
```bash
docker-compose up -d php-7.2 mysql57
```
 
Down all container
```bash
docker-compose stop
```
#### Env information 

| PHP Version  | Host | 
| ------------- | ------------- |
| PHP 7.3  | http://php73  | 
| PHP 7.2  | http://php72  | 
| PHP 7.1  | http://php71  | 
| PHP 7.0  | http://php70  | 
| PHP 5.6  | http://php56  | 

### Config & Database

| DB  | Host |User  | Password |
| --- | ---- |---- | ------- |
| Mysql57  | mysql57  |root  | root  |
| mysql56  | mysql56  |root  | root  |
| mysql55  | mysql55  |root  | root  |
| mariadb55  | mariadb55  |root  | root  |
| mariadb100  | mariadb100  |root  | root  |
| mariadb101  | mariadb101  |root  | root  |


To use the command line clients provided by the containers you can use the following commands:

```bash
# MySQL
docker-compose exec mysql` mysql -u root -p"root"

# MariaDB
docker-compose exec mariadb -u root -p"root"
```

#### How to browse Orangehrm

- php 5.6 : http://php56:{PORT}/
- php 7.0 : http://php70:{PORT}/
- php 7.1 : http://php71:{PORT}/
- php 7.2 : http://php72:{PORT}/
- php 7.3 : http://php73:{PORT}/
__Note:__ Here __PORT__ is either __NGINX_PORT__ or __NGINX_SSL_PORT__ which are defined in __.env__. When using __NGINX_SSL_PORT__ as the __PORT__ then URL should start with `https` instead of `http`.

#### How to execute unit tests
 __Execute Test PHP 7.3:__
 ```bash
 docker-compose exec os_dev_php73 /bin/bash
 phpunit
 ```

 __Execute Test PHP 7.2:__
 ```bash
 docker-compose exec os_dev_php72 /bin/bash
 phpunit
 ```
 
  __Execute Test PHP 7.1:__
  ```bash
  docker-compose exec os_dev_php71 /bin/bash
  phpunit
  ```
  
  __Execute Test PHP 7.0:__
  ```bash
   docker-compose exec os_dev_php70 /bin/bash
   phpunit
  ```

  __Execute Test PHP 5.6:__
  ```bash
   docker-compose exec os_dev_php56 /bin/bash
   phpunit
  ```
#### Build Images
```bash
docker-compose -f docker-compose.yml -f docker-compose-build.yml build nginx
```
