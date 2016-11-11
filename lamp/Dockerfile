From alpine:3.4
MAINTAINER janes - https://github.com/hxer

# Timezone
ENV TIMEZONE Asia/Shanghai

# 替换为阿里云的源，构建速度更快
# RUN sed -i 's#dl-cdn\.alpinelinux\.org#mirrors\.aliyun\.com#' /etc/apk/repositories

# install mysql, apache and php and php extensions, tzdata, wget
RUN echo "@community http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories && \
    apk add --update \
    mysql mysql-client \
    apache2 \
    curl wget \
    tzdata \
    php5-apache2 \
    php5-cli \
    php5-phar \
    php5-zlib \
    php5-zip \
    php5-bz2 \
    php5-ctype \
    php5-mysqli \
    php5-mysql \
    php5-pdo_mysql \
    php5-opcache \
    php5-pdo \
    php5-json \
    php5-curl \
    php5-gd \
    php5-gmp \
    php5-mcrypt \
    php5-openssl \
    php5-dom \
    php5-xml \
    php5-iconv \
    php5-xdebug@community

RUN curl -sS https://getcomposer.org/installer | \
    php -- --install-dir=/usr/bin --filename=composer

# configure timezone, mysql, apache
RUN cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \
    echo "${TIMEZONE}" > /etc/timezone && \
    mkdir -p /run/mysqld && chown -R mysql:mysql /run/mysqld /var/lib/mysql && \
    mysql_install_db --user=mysql --verbose=1 --basedir=/usr --datadir=/var/lib/mysql --rpm > /dev/null && \
    mkdir -p /run/apache2 && chown -R apache:apache /run/apache2 && chown -R apache:apache /var/www/localhost/htdocs/ && \
    sed -i 's#AllowOverride none#AllowOverride All#' /etc/apache2/httpd.conf && \
    sed -i 's#ServerName www.example.com:80#\nServerName localhost:80#' /etc/apache2/httpd.conf

# Configure xdebug
RUN echo "extension=xdebug.so" > /etc/php5/conf.d/xdebug.ini && \ 
    echo -e "\n[XDEBUG]"  >> /etc/php5/conf.d/xdebug.ini && \ 
    echo "xdebug.remote_enable=1" >> /etc/php5/conf.d/xdebug.ini && \  
    echo "xdebug.remote_connect_back=1" >> /etc/php5/conf.d/xdebug.ini && \ 
    echo "xdebug.idekey=PHPSTORM" >> /etc/php5/conf.d/xdebug.ini && \ 
    echo "xdebug.remote_log=\"/tmp/xdebug.log\"" >> /etc/php5/conf.d/xdebug.ini

#start apache
RUN echo "#!/bin/sh" > /start.sh && \
    echo "httpd" >> /start.sh && \
    echo "nohup mysqld --skip-grant-tables --bind-address 0.0.0.0 --user mysql > /dev/null 2>&1 &" >> /start.sh && \
    echo "sleep 3 && mysql -uroot -e \"create database db;\"" >> /start.sh && \
    echo "tail -f /var/log/apache2/access.log" >> /start.sh && \
    chmod u+x /start.sh

WORKDIR /var/www/localhost/htdocs/

EXPOSE 80
EXPOSE 3306

#VOLUME ["/var/www/localhost/htdocs","/var/lib/mysql","/etc/mysql/"]
ENTRYPOINT ["/start.sh"]
