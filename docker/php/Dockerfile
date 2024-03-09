# Pull Alpine image
FROM alpine:3.19
# Work has been done by
LABEL maintainer="Mohamad Yaman Shahbandar"
# Set the timezone
ARG TIMEZONE=UTC
# PHP version
ENV PHP_VERSION=8.3.3
# Node.js version
ENV NODE_VERSION=21
# Set the working directory
WORKDIR /var/www/html
# Use the root user
USER root
# Configure the timezone
RUN apk add --no-cache tzdata && \
    cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \
    echo ${TIMEZONE} > /etc/timezone
# Update package lists and install the necessary packages
RUN apk update && \
    apk add --no-cache \
    curl ca-certificates zip unzip git \
    python3 py3-pip py3-requests py3-beautifulsoup4 \
    net-tools sqlite-dev \
    gcc g++ make cmake pkgconf autoconf \
    openssl-dev libxml2-dev bison re2c libtool \
    libsodium-dev libpng libpng-dev libjpeg-turbo libjpeg-turbo-dev oniguruma-dev gmp-dev \
    freetype freetype-dev bzip2 bzip2-dev gettext-dev freetds freetds-dev postgresql-dev libxslt-dev \
    nodejs npm vim \
    bash
# Download PHP 8.3 source code
RUN wget -O php.tar.gz https://www.php.net/distributions/php-${PHP_VERSION}.tar.gz && tar -xvf php.tar.gz
# Configure and build PHP from source with extensions
RUN cd php-$PHP_VERSION && \
    ./configure --prefix=/usr/local/php \
    --with-openssl --with-libxml --with-xmlrpc \
    --with-pdo-mysql --with-freetype --with-jpeg \
    --with-cli --with-mcrypt --with-iconv \
    --enable-bcmath --enable-zip --enable-mbstring \
    --enable-opcache --enable-gd --enable-imap --enable-debug \
    --with-soap --with-intl --with-gmp --with-redis --with-memcached --with-xdebug \
    --enable-amqp=shared --enable-apcu=shared --with-gettext=shared \
    --with-bz2=shared --with-exif=shared --with-igbinary=shared \
    --with-lz4=shared --with-mongodb=shared --with-mysqli=shared \
    --with-oauth=shared --with-pdo_mysql=shared --with-pdo_dblib=shared \
    --enable-pcntl=shared --with-pdo_pgsql=shared --with-pgsql=shared \
    --with-rdkafka=shared --with-ssh2=shared  \
    --with-uuid=shared --with-xsl=shared --with-yaml=shared \
    --with-mysql --with-zlib --with-xml --with-json \
    --enable-fpm --with-fpm-user=www-data --with-fpm-group=www-data \
    && make && make install
# Cleanup and add PHP to PATH
RUN rm -rf php-$PHP_VERSION php.tar.gz
# Add PHP binary path to system PATH
ENV PATH="/usr/local/php/bin:${PATH}"
# Add PHP-fpm path to system PATH
ENV PATH="/usr/local/php/sbin:${PATH}"
# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
# Ensure www-data user exists. 82 is the standard uid/gid for "www-data" in Alpine
RUN set -eux; \
	adduser -u 82 -D -S -G www-data www-data
# Install the sudo package
RUN apk add --no-cache sudo
# Expose port 9000
EXPOSE 9000
# Copy php-fpm config file
COPY php-fpm.conf /usr/local/php/etc/php-fpm.conf
# Change ownership of the project to www-data user and group
RUN chown -R www-data:www-data /var/www/html
# Make sure the project is writable
RUN chmod o+w /var/www/html -R
# Start php-fpm in the foreground
CMD ["php-fpm", "-F"]
