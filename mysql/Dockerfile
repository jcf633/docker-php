FROM mysql:${MYSQL_VERSION}

MAINTAINER Jean Fonseca

COPY ./db/ /docker-entrypoint-initdb.d/

EXPOSE 3306;