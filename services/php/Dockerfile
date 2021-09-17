FROM php:8.0-fpm-alpine3.13

# Install PHP extensions
RUN docker-php-ext-install pdo pdo_mysql

RUN apk --no-cache add pcre-dev ${PHPIZE_DEPS} \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && apk del pcre-dev ${PHPIZE_DEPS}

# Add PHP-FPM config: UDS
ADD uds.conf /usr/local/etc/php-fpm.d/zz-docker.conf

# Add PHP-FPM config: TCP
# ADD tcp.conf /usr/local/etc/php-fpm.d/www.conf

# Create web user and group
RUN addgroup -g 1000 laravel
RUN adduser -G laravel -g laravel -s /bin/sh -D laravel

# Create web directory
RUN mkdir -p /var/www/html

RUN chown laravel:laravel /var/www/html

# Install Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
    php -r "unlink('composer-setup.php');"
