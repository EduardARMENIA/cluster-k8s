# Используем официальный PHP образ с FPM
FROM php:8.2-fpm

# Устанавливаем зависимости
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libzip-dev \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    curl \
    && docker-php-ext-install pdo_mysql zip mbstring exif pcntl bcmath gd

# Устанавливаем Composer
COPY --from=composer:2.8 /usr/bin/composer /usr/bin/composer

# Устанавливаем рабочую директорию
WORKDIR /var/www

# Копируем проект Laravel
COPY . .

# Устанавливаем зависимости Laravel
RUN composer install --no-dev --optimize-autoloader

# Генерация ключа Laravel (можно закомментировать, если используешь секреты)
# RUN php artisan key:generate

# Настройка прав
RUN chown -R www-data:www-data /var/www \
    && chmod -R 755 /var/www/storage /var/www/bootstrap/cache

# Expose порт Laravel FPM
EXPOSE 9000

# Запуск PHP-FPM
CMD ["php-fpm"]

