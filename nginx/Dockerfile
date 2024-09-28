FROM nginx:1.27

COPY nginx.conf /etc/nginx/

RUN rm /etc/nginx/conf.d/default.conf

#Non-root user
ARG NON_ROOT_UID=1000
ARG NON_ROOT_GID=1000

RUN set -x && \
    groupmod -o -g ${NON_ROOT_GID} www-data && \
    usermod -o -u ${NON_ROOT_UID} -g www-data www-data

CMD ["nginx", "-g", "daemon off;"]
