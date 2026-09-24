ARG PHP_VERSION=8.5

FROM php:8.1-apache

# I-install ang database extensions
RUN docker-php-ext-install mysqli pdo pdo_mysql

# I-enable ang mod_rewrite para sa URL routing
RUN a2enmod rewrite

# Baguhin ang Apache DocumentRoot sa 'public' folder
ENV APACHE_DOCUMENT_ROOT /var/www/html/public

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

# Payagan ang .htaccess overrides para gumana ang routing
RUN echo '<Directory /var/www/html/public>\n\tOptions Indexes FollowSymLinks\n\tAllowOverride All\n\tRequire all granted\n</Directory>' > /etc/apache2/conf-available/override.conf \
    && a2enconf override

# Kopyahin ang lahat ng files sa web server directory
COPY . /var/www/html/

# Ayusin ang permissions para sa www-data
RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 755 /var/www/html

EXPOSE 80