ARG ELEDOCK_PHP_VERSION=8.3

FROM php:${ELEDOCK_PHP_VERSION}-fpm

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

# Used for additional extensions or extensions not supported in every PHP version
ARG ADDITIONAL_PHP_EXTENSIONS=''

RUN chmod uga+x /usr/local/bin/install-php-extensions && \
    sync && \
    install-php-extensions bcmath gd exif zip imap intl opcache pdo_mysql pdo_pgsql redis xdebug soap ${ADDITIONAL_PHP_EXTENSIONS} && \
    #Disable Xdebug by default
    sed -i 's/^zend_extension=/;zend_extension=/g' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN apt-get update && \
    apt-get -y install git --no-install-recommends

WORKDIR /var/www

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php -r "if (hash_file('sha384', 'composer-setup.php') === file_get_contents('https://composer.github.io/installer.sig')) { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

#Non-root user
ARG NON_ROOT_UID=1000
ARG NON_ROOT_GID=1000

RUN groupmod -o -g ${NON_ROOT_GID} www-data && \
    usermod -o -u ${NON_ROOT_UID} -g www-data www-data

CMD ["php-fpm"]

EXPOSE 9000
