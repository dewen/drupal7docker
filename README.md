# Docker for Drupal7
Docker file to create Drupal 7 environment image. Cloned from [offical Drupal docker file](https://github.com/docker-library/drupal/tree/ff8962fc943001457c6919fa42e3d875b9fab9f7/7/apache).

# Usage
* Build image from Dockerfile
```
docker build -t drupal7docker .
```
* Prepare the Drupal working dir.
mkdir /path/to/drupal7/
* Start MySQL container
* Start app container.
