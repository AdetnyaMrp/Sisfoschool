FROM php:8.1-apache

# Install ekstensi PHP
RUN docker-php-ext-install mysqli pdo pdo_mysql

# Aktifkan mod_rewrite
RUN a2enmod rewrite

# Copy semua file project ke container
COPY . /var/www/html

# Konfigurasi Apache untuk CI3
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

# Perbaiki permission (gunakan "|| true" agar tidak error jika folder belum ada)
RUN chown -R www-data:www-data /var/www/html || true \
    && chmod -R 755 /var/www/html || true \
    && mkdir -p /var/www/html/application/views/v_home \
    && chmod -R 777 /var/www/html/application/cache || true \
    && mkdir -p /var/www/html/uploads \
    && chmod -R 777 /var/www/html/uploads || true

CMD ["apache2-foreground"]
