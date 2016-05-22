FROM php:7.0-apache
MAINTAINER Jaynarol <Jaynarol@gmail.com>


# enable mods
RUN a2enmod remoteip


# customs
RUN sed -i "s/\%h \%l/\%a \%l/" /etc/apache2/apache2.conf
COPY config/apache/*.conf /etc/apache2/conf-enabled/
COPY config/php/*.ini /usr/local/etc/php/conf.d/
COPY config/mod/*.conf /etc/apache2/mods-enabled/


# override
EXPOSE 443