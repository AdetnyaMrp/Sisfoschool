FROM php:8.1-apache

# Install ekstensi PHP
RUN docker-php-ext-install mysqli pdo pdo_mysql

# Aktifkan mod_rewrite
RUN a2enmod rewrite

# Copy semua file project
COPY . /var/www/html

# Konfigurasi Apache untuk CodeIgniter 3
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

# Pastikan folder penting ada
RUN mkdir -p /var/www/html/application/cache /var/www/html/uploads

# Perbaiki permission
RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 755 /var/www/html \
    && chmod -R 777 /var/www/html/application/cache \
    && chmod -R 777 /var/www/html/uploads

CMD ["apache2-foreground"]
