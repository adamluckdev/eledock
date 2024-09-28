FROM adminer:latest

USER root

RUN rm /etc/php/7.4/cli/conf.d/0-upload_large_dumps.ini && \
    rm /etc/php/7.4/fpm/conf.d/0-upload_large_dumps.ini

USER adminer

EXPOSE 8080
