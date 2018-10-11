# Docker for Drupal7
Docker file to create Drupal 7 environment image. Cloned from [offical Drupal docker file](https://github.com/docker-library/drupal/tree/ff8962fc943001457c6919fa42e3d875b9fab9f7/7/apache).

# Usage
* Build image from Dockerfile (work under current repo path), image named 'drupal7docker'
```
docker build -t drupal7docker .
```
* Prepare the Drupal working dir.
```
mkdir /path/to/drupal7/ && cd $_
curl -fsSL "https://ftp.drupal.org/files/projects/drupal-7.59.tar.gz" -o drupal.tar.gz \
&& tar -xz --strip-components=1 -f drupal.tar.gz \
&& rm drupal.tar.gz
```
* Start MySQL container
```
mkdir -p /path/to/mysql/ && cd $_
docker run --rm --name mysql56local -v `pwd`/mysql:/var/lib/mysql -p 33066:3306 -e MYSQL_ROOT_PASSWORD=root mysql:5.6
```
* create an empty database with name 'd7'.
```
docker exec mysql56local /usr/bin/mysql -uroot -proot -e "create database d7"
```
* Start app container with mysql container linked from drupal directory.
```
cd /path/to/drupal7/
docker run --rm --name drupal7dewen1 --link mysql56local:mysql -p 8803:80  -v `pwd`:/var/www/html drupal7docker
```
* Open the Drupal install page from browser and setup the site.
```
http://localhost:8803/
```
Pay attention to database host, should be `mysql56local`, dbuser: root, dbpassword: root, dbname: d7.
