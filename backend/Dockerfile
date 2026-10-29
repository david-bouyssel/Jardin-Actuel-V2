FROM ghcr.io/openclassrooms-student-center/jardin-actuel-backend:2-0-0 AS app

FROM php:8.5-cli-bookworm
RUN apt-get update && apt-get install -y --no-install-recommends curl libicu-dev libzip-dev \
    && docker-php-ext-install -j"$(nproc)" intl pdo_mysql zip \
    && rm -rf /var/lib/apt/lists/*
RUN printf "display_errors=Off\nerror_reporting=E_ALL & ~E_DEPRECATED\nzend.assertions=-1\n" > /usr/local/etc/php/conf.d/zz-app.ini
WORKDIR /var/www/html
COPY --from=app /var/www/html /var/www/html
CMD ["/bin/sh", "-c", "php -S 0.0.0.0:8081 -t public/"]
