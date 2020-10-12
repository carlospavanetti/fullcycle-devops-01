FROM php:7.4-fpm

WORKDIR /var/www
RUN rm -rf html
COPY . ./
RUN chown -R www-data:www-data .
RUN ln -s public html

RUN usermod -u 1000 www-data
USER www-data

EXPOSE 9000
ENTRYPOINT [ "php" ]
CMD [ "artisan", "serve", "--host=0.0.0.0" ]
