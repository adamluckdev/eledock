ARG MARIADB_VERSION=latest
FROM mariadb:${MARIADB_VERSION}

#####################################
# Set Timezone
#####################################

ARG MARIADB_TZ=UTC
RUN ln -snf /usr/share/zoneinfo/${MARIADB_TZ} /etc/localtime && echo ${MARIADB_TZ} > /etc/timezone && chown -R mysql:root /var/lib/mysql/
COPY my.cnf /etc/mysql/conf.d/my.cnf

RUN chmod -R 644 /etc/mysql/conf.d/my.cnf

CMD ["mariadbd"]

EXPOSE 3306
