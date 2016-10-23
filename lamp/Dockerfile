From alpine:3.4
MAINTAINER janes - https://github.com/hxer

RUN apk update
# install mysql
RUN apk add mysql mysql-client

#configure mysql
RUN mkdir -p /run/mysqld && chown -R mysql:mysql /run/mysqld /var/lib/mysql && \
    mysql_install_db --user=mysql --verbose=1 --basedir=/usr --datadir=/var/lib/mysql --rpm > /dev/null

#install apache and php and php extensions
RUN apk add apache2 \
    php5-apache2 php5-cli php5-phar php5-zlib php5-zip php5-ctype php5-mysqli php5-xml php5-pdo_mysql  \
    php5-opcache php5-pdo php5-json php5-curl php5-gd php5-mcrypt php5-openssl php5-dom  wget 


# configure apache
RUN sed -i 's#AllowOverride none#AllowOverride All#' /etc/apache2/httpd.conf && \
    sed -i 's#ServerName www.example.com:80#\nServerName localhost:80#' /etc/apache2/httpd.conf
RUN mkdir -p /run/apache2 && chown -R apache:apache /run/apache2

#start apache
RUN echo "#!/bin/sh" >> /start.sh
RUN echo "httpd" >> /start.sh

#start mysql

RUN echo "nohup mysqld --skip-grant-tables --bind-address 0.0.0.0 --user mysql > /dev/null 2>&1 &" >> /start.sh

RUN echo "tail -f /var/log/apache2/access.log" >> /start.sh
RUN chmod +x /start.sh

EXPOSE 80
EXPOSE 3306

#VOLUME ["/var/www/localhost/htdocs","/var/lib/mysql","/etc/mysql/"]
ENTRYPOINT ["/start.sh"]




