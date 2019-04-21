
FROM tommylau/php-5.2


# Enable Apache2 modules
# RUN a2enmod rewrite

# Fix packages repo
RUN echo "deb [check-valid-until=no] http://cdn-fastly.deb.debian.org/debian jessie main" > /etc/apt/sources.list.d/jessie.list \
 && echo "deb [check-valid-until=no] http://archive.debian.org/debian jessie-backports main" > /etc/apt/sources.list.d/jessie-backports.list \
 && sed -i '/deb http:\/\/deb.debian.org\/debian jessie-updates main/d' /etc/apt/sources.list \
 && apt-get -o Acquire::Check-Valid-Until=false update \
 && echo "Acquire::Check-Valid-Until \"false\";" > /etc/apt/apt.conf.d/100disablechecks

# Install remaining stuff
RUN apt-get update && apt-get install -y --no-install-recommends \
        git \
        zip \
        g++ \
        libicu-dev \
        zlib1g-dev \
        gnupg2 \
        libmcrypt-dev \
#   && docker-php-ext-configure \
#       intl \
    && docker-php-ext-install \
#       intl \
        gettext \
        zip \
        exif \
        mcrypt


# Install MySQL
###### MySQL already installed in parent Docker image
# RUN apt-get update && apt-get install -y --no-install-recommends \
#         mysql-client \
#     && docker-php-ext-install \
#         mysqli \
#         pdo \
#         pdo_mysql


# Install GD2
###### GD already installed in parent Docker image
# RUN apt-get update && apt-get install -y --no-install-recommends \
#         libfreetype6-dev \
#         libjpeg62-turbo-dev \
#         libpng-dev \
#     && docker-php-ext-configure \
#         gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
#     && docker-php-ext-install \
#         -j$(nproc) gd


# Install XDebug
# RUN pecl install \
#         xdebug-2.2.7 \
#     && docker-php-ext-enable \
#         xdebug


# Install Node & NPM
RUN curl -sL https://deb.nodesource.com/setup_11.x | bash - \
    && apt-get update && apt-get install -y --no-install-recommends \
        nodejs


# Install composer and make the correct dirs writable
###### Composer requires PHP 5.3.2+ to run
# ENV PATH "/composer/vendor/bin:$PATH"
# ENV COMPOSER_ALLOW_SUPERUSER 1
# ENV COMPOSER_HOME /composer
# RUN curl -s -f -L -o /tmp/installer.php https://getcomposer.org/installer \
#     && php /tmp/installer.php --no-ansi --install-dir=/usr/bin --filename=composer \
#     && rm /tmp/installer.php \
#     && mkdir -p /composer \
#     && chmod -R 777 /composer
