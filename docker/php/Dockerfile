# PHP Version environment variable
ARG PHP_VERSION

  # PHP Version alpine image to install based on the PHP_VERSION environment variable
FROM php:$PHP_VERSION-fpm-alpine

  # Application environment variable
ARG APP_ENV

  # Remote working directory environment variable
ARG REMOTE_WORKING_DIR

  # Install dev dependencies
RUN apk add --no-cache --virtual .build-deps \
$PHPIZE_DEPS \
curl-dev \
imagemagick-dev \
libtool \
libxml2-dev \
postgresql-dev \
sqlite-dev

  # Install production dependencies
RUN apk add --no-cache \
bash \
curl \
freetype-dev \
g++ \
gcc \
git \
icu-dev \
icu-libs \
imagemagick \
libc-dev \
libjpeg-turbo-dev \
libpng-dev \
libzip-dev \
make \
mysql-client \
nodejs \
nodejs-npm \
yarn \
openssh-client \
postgresql-libs \
rsync \
zlib-dev

  # Install PECL and PEAR extensions
RUN pecl install \
redis \
imagick \
xdebug

  # Enable PECL and PEAR extensions
RUN docker-php-ext-enable \
redis \
imagick \
xdebug

  # Configure php extensions
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
&& docker-php-ext-configure zip --with-libzip

  # Install php extensions
RUN docker-php-ext-install \
bcmath \
calendar \
curl \
exif \
gd \
iconv \
intl \
mbstring \
pdo \
pdo_mysql \
pdo_pgsql \
pdo_sqlite \
pcntl \
tokenizer \
xml \
zip

  # install xdebug and enable it if the development environment is local
RUN if [ $APP_ENV = "local" ]; then \
pecl install xdebug; \
docker-php-ext-enable xdebug; \
fi;

  # Install PHP Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

  # Remove Cache
RUN rm -rf /var/cache/apk/*

  # Add UID '1000' to www-data
RUN apk add shadow && usermod -u 1001 www-data && groupmod -g 1001 www-data

  # Copy existing application directory permissions
COPY --chown=www-data:www-data . $REMOTE_WORKING_DIR

  # Change current user to www
USER www-data