FROM mysql:8.0
# for setting up root password we have full doc in https://hub.docker.com/_/mysql under this link we have MYSQL_ROOT_PASSWORD
ENV MYSQL_ROOT_PASSWORD=ExpenseApp@1 
ADD scripts/*.sql /docker-entrypoint-initdb.d
    # MYSQL_DATABASE=transactions \
    # MYSQL_USER=expense \
    # MYSQL_PASSWORD=ExpenseApp@1