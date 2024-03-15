ARG VERSION
FROM php:${VERSION}-cli

RUN apt update && apt upgrade -y && \
    apt install -y libxml2-dev wget

# Copy over our script to check if the extension is already installed
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /opt/php-ext-check

RUN apt-get install -y \
    libzip-dev \
    zip

# Check and/or Install core modules
RUN /opt/php-ext-check bcmath ctype fileinfo json mbstring openssl tokenizer xml zip curl

# Install PHP Database Extensions
RUN /opt/php-ext-check mysql mysqli pdo_mysql pdo

# Install Composer
# e3e43bde99447de1c13da5d1027545be81736b27 = 04DEC2020
RUN wget https://raw.githubusercontent.com/composer/getcomposer.org/e3e43bde99447de1c13da5d1027545be81736b27/web/installer -O - -q | php -- --quiet
RUN mv composer.phar /usr/local/bin/composer

# Install Xdebug
RUN /opt/php-ext-check xdebug

WORKDIR var/www/html
