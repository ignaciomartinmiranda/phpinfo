# phpinfo

[![CI](https://github.com/academiaonline-org/phpinfo/actions/workflows/ci.yaml/badge.svg?branch=main)](https://github.com/academiaonline-org/phpinfo/actions/workflows/ci.yaml)

```
git clone https://github.com/academiaonline-org/phpinfo
cd phpinfo
git checkout main
```
```
php -f src/index.php -S 0.0.0.0:8080
```
```
curl localhost:8080/src/index.php
```
```
docker run --entrypoint php -p 8080:8080 -v $PWD/src/index.php:/src/index.php redhat_php -f src/index.php -S 0.0.0.0:8080
```
