# image
FROM php:7.2-apache

# Set php.ini
COPY ./php.ini /usr/local/etc/php/

# Set apache conf (Before tag:5.4-apache)
# COPY ./apache2.conf /etc/apache2/
# COPY ./sites/*.conf /etc/apache2/sites-available/

# Set apache conf (After tag:5.5-apache)
ENV APACHE_DOCUMENT_ROOT /var/www/html
# COPY src/ /var/www/html/
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

# Install MySQL connection module
RUN apt-get update \
  && apt-get install -y libpq-dev vim \
  && docker-php-ext-install pdo_mysql pdo_pgsql mysqli mbstring

# RUN rm /etc/apache2/sites-available/000-default.conf
# RUN rm /etc/apache2/ports.conf


# COPY ./conf/000-default.conf etc/apache2/sites-available
COPY ./.conf/ports.conf /etc/apache2/ports.conf
RUN chmod 644 /etc/apache2/ports.conf
COPY ./.conf/proxy.conf /etc/apache2/mods-available/proxy.conf
RUN chmod 644 /etc/apache2/mods-available/proxy.conf
COPY ./.conf/apache2.conf /etc/apache2/apache2.conf
RUN chmod 644 /etc/apache2/apache2.conf
COPY ./.conf/000-default.conf /etc/apache2/sites-available/000-default.conf
RUN chmod 644 /etc/apache2/sites-available/000-default.conf
COPY ./.conf/000-default.conf /etc/apache2/sites-available/default-ssl.conf
RUN chmod 644 /etc/apache2/sites-available/default-ssl.conf

RUN a2enmod proxy_http
# RUN a2ensite default-ssl
# RUN a2enmod ssl
# RUN a2enmod rewrite