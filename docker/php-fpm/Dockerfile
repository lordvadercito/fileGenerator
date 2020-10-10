FROM php:7.4-fpm

# install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === '795f976fe0ebd8b75f26a6dd68f78fd3453ce79f32ecb33e7fd087d39bfeb978342fb73ac986cd4f54edd0dc902601dc') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --filename=composer --install-dir /usr/local/bin
RUN php -r "unlink('composer-setup.php');"

# install missing extensions (and locales)
RUN apt-get update && \
    apt-get install -y libzip-dev zlib1g-dev libonig-dev zlibc libicu-dev libpq-dev libmemcached-dev locales vim.tiny git

# install missing extensions
RUN docker-php-ext-install mbstring zip pdo_pgsql

# Generate locale for es_AR
RUN echo "es_AR.UTF-8 UTF-8" >> /etc/locale.gen
RUN locale-gen
RUN echo "es 		es_AR.UTF-8" >> /etc/locale.alias

# Set file owner
RUN chown -R www-data:www-data /var/www/html

WORKDIR /var/www