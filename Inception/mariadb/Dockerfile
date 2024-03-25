FROM debian:buster

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y mariadb-server

COPY config/50-server.cnf /etc/mysql/mariadb.conf.d/50-server.cnf

RUN service mysql start && \
    mysql -e "CREATE DATABASE IF NOT EXISTS wordpress;" && \
    mysql -e "CREATE USER IF NOT EXISTS 'kigo'@'localhost' IDENTIFIED BY '12345';" && \
    mysql -e "GRANT ALL PRIVILEGES ON wordpress.* TO 'kigo'@'%' IDENTIFIED BY '12345';" && \
    mysql -e "ALTER USER 'root'@'localhost' IDENTIFIED BY '12345';" && \
    mysql -e "FLUSH PRIVILEGES;"

RUN mysqladmin -u root -p12345 shutdown
CMD ["mysqld_safe"]
