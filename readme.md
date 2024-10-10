# php legacy repository

a repository to host legacy php applications.


## docker build
`docker build -t zetanova/php:5.6-fpm ./php5.6`

## docker setup
put regular php-fpm configuration under /etc/php/5.6/fpm/pool.d/*.conf
php-fpm does only support user by name and users need to be created with `RUN useradd --user-group -u 1123 user1`.
unix sockets can be bound under /run/php/*.sock

## docker run
```
docker run --name php5.6 \
    --mount type=bind,source=/etc/php/5.6/fpm/pool.d,target=/usr/local/etc/php-fpm.d \
    --mount type=bind,source=/run/php,target=/run/php \
    --mount type=bind,source=/var/run/mysqld/mysqld.sock,target=/tmp/mysql.sock \
    --mount type=bind,source=/home/user1,target=/home/user1 \
    --rm -it zetanova/php:5.6-fpm
```

## todo
init script to add users to a container
