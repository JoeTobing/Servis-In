# Stage 1: Build dependencies dengan Composer
FROM composer:2 AS build

# Set working directory
WORKDIR /app

# Copy semua file project
COPY . .

# Install dependencies Laravel (tanpa dev, dengan optimized autoloader)
RUN cd PROYEK_COBA1/backend-servis && composer install --no-dev --optimize-autoloader

# Stage 2: Production image PHP
FROM php:8.2-fpm

# Install PHP extensions yang dibutuhkan Laravel
RUN apt-get update && apt-get install -y \
    libzip-dev \
    unzip \
    git \
    && docker-php-ext-install pdo_mysql zip

# Copy hasil build dari stage 1
COPY --from=build /app /app

# Set working directory ke folder backend
WORKDIR /app/PROYEK_COBA1/backend-servis

# Expose port 8080
EXPOSE 8080

# Jalankan server PHP built-in (development/demo)
CMD ["php", "-S", "0.0.0.0:8080", "-t", "public"]
