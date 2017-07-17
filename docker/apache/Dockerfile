# Set the base image to debian
FROM ubuntu:16.04

# File Author / Maintainer
MAINTAINER William Jones <billy@freshjones.com>

ENV TERM=xterm

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get -y install apache2
RUN apt-get -y install libapache2-mod-fastcgi

COPY ./configs/php7-fpm.conf /etc/apache2/conf-available/
COPY ./configs/fqdn.conf /etc/apache2/conf-available/

RUN a2enconf php7-fpm
RUN a2enconf fqdn

RUN a2enmod rewrite
RUN a2enmod headers
RUN a2enmod alias
RUN a2enmod expires
RUN a2enmod fastcgi
RUN a2enmod actions

RUN rm /var/www/html/index.html

COPY ./configs/www/index.php /var/www/html/index.php

# clean apt cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

COPY ./configs/apache2-foreground /usr/local/bin/

#expose port 80
EXPOSE 80

CMD ["apache2-foreground"]
