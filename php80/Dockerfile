FROM php:apache-buster

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libbz2-dev \
        libgmp-dev \
        libmagickwand-dev \ 
        libpspell-dev \
        libxml2-dev \
        libc-client-dev \
        libicu-dev \
        libkrb5-dev \
        libldap2-dev \
        libtidy-dev \
        libxslt1-dev \
        libzip-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install -j$(nproc) tidy gd bcmath bz2 calendar exif gettext gmp pspell shmop imap intl ldap mysqli pcntl pdo_mysql soap sockets xsl opcache zip

RUN pecl install apcu-5.1.17 \
    && docker-php-ext-enable apcu


# install imagick
# Version is not officially released https://pecl.php.net/get/imagick but following works for PHP 8
RUN mkdir -p /usr/src/php/ext/imagick; \
    curl -fsSL https://github.com/Imagick/imagick/archive/06116aa24b76edaf6b1693198f79e6c295eda8a9.tar.gz | tar xvz -C "/usr/src/php/ext/imagick" --strip 1; \
    docker-php-ext-install imagick;

COPY php.ini "$PHP_INI_DIR/php.ini"