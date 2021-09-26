# phpinfo

DOWNLOAD GITHUB REPOSITORY
```
git clone https://github.com/academiaonline/phpinfo
cd phpinfo
git checkout main
```
## TRADITIONAL DEPLOYMENT (WITHOUT CONTAINERS)
RUN THE APPLICATION WITHOUT CONTAINERIZATION (AFTER INSTALLING PHP IN YOUR SYSTEM)
```
php -f src/index.php -S 0.0.0.0:8080
```
TEST THE RUNNING APPLICATION (AFTER INSTALLING CURL IN YOUR SYSTEM)
```
curl localhost:8080/src/index.php
```
## MODERN DEPLOYMENT (WITH CONTAINERS)
CHECKOUT THE BRANCH WITH THE CONTAINERIZED APPLICATION
```
git checkout 2021-10
git pull
```
BUILD THE DOCKER IMAGE
```
mkdir /build-context/
docker build --file Dockerfile --tag academiaonline/phpinfo:latest /build-context/
```
(ALTERNATIVE WAY) BUILD THE DOCKER IMAGE USING DOCKERIGNORE
```
docker build --file Dockerfile --tag academiaonline/phpinfo:latest .
```
RUN THE CONTAINER CREATING A (HOST BIND) VOLUME TO INCLUDE THE ARTIFACT (NOT INCLUDED INSIDE THE IMAGE) (POSSIBLE USECASE: YOUR LAPTOP)
```
PHP_HOST=0.0.0.0
PHP_PORT=8080
CONTAINER_ID=$( docker run --detach --publish ${PHP_PORT} --volume ${PWD}/src/index.php:/src/index.php:ro academiaonline/phpinfo:latest -f src/index.php -S ${PHP_HOST}:${PHP_PORT} )
curl --head http://localhost:$( docker port ${CONTAINER_ID} | cut --delimiter : --field 2 )/src/index.php
```
RUN THE CONTAINER CREATING A DOCKER VOLUME TO INCLUDE THE ARTIFACT (NOT INCLUDED INSIDE THE IMAGE) (WE WILL NEED A SECOND CONTAINER TO DOWNLOAD THE ARTIFACT)
```
VOLUME=phpinfo

# WORK IN PROGRESS ...

PHP_HOST=0.0.0.0
PHP_PORT=8080
CONTAINER_ID=$( docker run --detach --publish ${PHP_PORT} --volume ${VOLUME}:/src/index.php:ro academiaonline/phpinfo:latest -f src/index.php -S ${PHP_HOST}:${PHP_PORT} )
curl --head http://localhost:$( docker port ${CONTAINER_ID} | cut --delimiter : --field 2 )/src/index.php
```
