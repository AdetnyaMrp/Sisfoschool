FROM php:8.1-apache

# Install ekstensi PHP yang diperlukan
RUN docker-php-ext-install mysqli pdo pdo_mysql

# Aktifkan mod_rewrite
RUN a2enmod rewrite

# Copy semua file project ke container
COPY . /var/www/html

# Atur VirtualHost Apache
RUN echo '<VirtualHost *:80>\n\
    ServerAdmin webmaster@localhost\n\
    DocumentRoot /var/www/html\n\
    <Directory /var/www/html>\n\
        Options Indexes FollowSymLinks\n\
        AllowOverride All\n\
        Require all granted\n\
    </Directory>\n\
    ErrorLog ${APACHE_LOG_DIR}/error.log\n\
    CustomLog ${APACHE_LOG_DIR}/access.log combined\n\
</VirtualHost>' > /etc/apache2/sites-enabled/000-default.conf

# Perbaiki permission
RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 755 /var/www/html \
    && chmod -R 777 /var/www/html/application/

# Jalankan Apache di foreground
CMD ["apache2-foreground"]
