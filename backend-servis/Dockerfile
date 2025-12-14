# Base image PHP + Composer
FROM php:8.2-cli

# Install dependencies Laravel
RUN apt-get update && apt-get install -y \
    unzip \
    git \
    libzip-dev \
    && docker-php-ext-install pdo_mysql zip

# Set working directory
WORKDIR /app

# Copy project
COPY . .

# Install Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && php -r "unlink('composer-setup.php');"

# Install PHP dependencies Laravel
RUN composer install --no-dev --optimize-autoloader

# Expose port 8080
EXPOSE 8080

# Jalankan start.sh saat container dijalankan
CMD ["./start.sh"]
