FROM composer:2.5.3 as build
RUN git clone https://github.com/mohamedasri44/backend.git /app
WORKDIR /app
RUN composer install --prefer-dist --no-interaction --optimize-autoloader --no-dev




FROM php:8.2.2-fpm as dev

# Install the required dependencies
RUN apt-get update && apt-get install -y \
    zip \
    unzip \
    && docker-php-ext-install pdo_mysql

COPY ./php/php.dev.ini /usr/local/etc/php/conf.d/

WORKDIR /app

COPY --from=build /app .
COPY --from=composer /usr/bin/composer /usr/bin/composer

COPY .env.dev ./.env
RUN composer install --prefer-dist --no-interaction

RUN chmod 777 -R ./storage/

RUN php artisan key:generate



FROM php:8.2.2-fpm as prod

# Install the required dependencies
RUN apt-get update && apt-get install -y \
    zip \
    unzip \
    && docker-php-ext-install pdo_mysql

COPY ./php/php.prod.ini /usr/local/etc/php/conf.d/

WORKDIR /app

COPY --from=build /app .
COPY .env.prod ./.env

RUN chmod 777 -R ./storage/

RUN php artisan key:generate
RUN php artisan route:cache
RUN php artisan view:cache
RUN php artisan config:cache


