FROM php:fpm

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN install-php-extensions bcmath bz2 calendar exif gd gettext gmp igbinary imagick memcached mongodb mysqli pcntl pdo_mysql pdo_pgsql pgsql redis shmop sockets swoole sysvmsg sysvsem sysvshm wddx xhprof xsl zip
