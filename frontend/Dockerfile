FROM debian:stretch

RUN apt-get update && apt-get install -y apt-transport-https lsb-release ca-certificates

RUN apt-get install wget

RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg

RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list

RUN apt-get update && apt-get install -y php7.2 php7.2-cli php7.2-common php7.2-json php7.2-opcache php7.2-pgsql php7.2-zip php7.2-fpm php7.2-mbstring

RUN apt-get install -y nginx

#RUN /etc/init.d/nginx restart
#RUN /etc/init.d/php7.2-fpm restart

RUN apt-get install -y curl && apt-get install -y procps && apt-get install -y nano postgresql-client

RUN mkdir /run/php

#COPY conf/php-fpm.conf /etc/php/7.2/fpm/php-fpm.conf
COPY conf/default /etc/nginx/sites-available/default
COPY conf/run.sh /run.sh
COPY web /var/www/html

EXPOSE 80 9000

ENTRYPOINT ["/bin/bash","/run.sh"]