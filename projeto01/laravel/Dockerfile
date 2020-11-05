FROM php:7.4-fpm as build-stage

RUN apt-get update && apt-get install -y wget

ENV DOCKERIZE_VERSION v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

# Final image
FROM php:7.4-fpm

RUN apt-get update && apt-get install -y mariadb-client
RUN docker-php-ext-install pdo pdo_mysql

WORKDIR /var/www
RUN rm -rf html
COPY --from=build-stage /usr/local/bin/dockerize /usr/local/bin/dockerize

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY . /var/www
RUN composer install

RUN chown -R www-data:www-data .
RUN ln -s public html

RUN usermod -u 1000 www-data
USER www-data

EXPOSE 9000
ENTRYPOINT [ "php-fpm" ]
