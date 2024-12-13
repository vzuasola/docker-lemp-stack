FROM mariadb:10.3

ADD my.cnf /etc/mysql/conf.d/my.cnf
RUN chmod 644 /etc/mysql/conf.d/my.cnf

EXPOSE 3306

CMD ["mysqld"]
