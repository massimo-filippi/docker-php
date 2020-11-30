
FROM php:8.0-rc-apache


# Enable Apache2 modules
RUN a2enmod rewrite headers


# Install remaining stuff
RUN apt-get update && apt-get install -y --no-install-recommends \
        git \
        zlib1g-dev \
        g++ \
        libicu-dev \
        libzip-dev \
        gnupg2 \
    && docker-php-ext-configure \
        intl \
    && docker-php-ext-install \
        intl \
        gettext \
        zip \
        exif


# Install MySQL
RUN apt-get update && apt-get install -y --no-install-recommends \
        default-mysql-client \
    && docker-php-ext-install \
        mysqli \
        pdo \
        pdo_mysql


# Install GD2
RUN apt-get update && apt-get install -y --no-install-recommends \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-configure \
        gd --with-freetype --with-jpeg \
    && docker-php-ext-install \
        -j$(nproc) gd


# Install XDebug
RUN pecl install \
        xdebug \
    && docker-php-ext-enable \
        xdebug


# Install Node & NPM
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash - \
    && apt-get update && apt-get install -y --no-install-recommends \
        nodejs


# Install composer and make the correct dirs writable
ENV PATH "/composer/vendor/bin:$PATH"
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
RUN curl -s -f -L -o /tmp/installer.php https://getcomposer.org/installer \
    && php /tmp/installer.php --no-ansi --install-dir=/usr/bin --filename=composer \
    && rm /tmp/installer.php \
    && mkdir -p /composer \
    && chmod -R 777 /composer
