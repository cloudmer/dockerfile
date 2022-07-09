FROM php:7.4.30-fpm

# 时区
ENV TZ=Asia/Shanghai

# 阿里云源 加速
RUN mv /etc/apt/sources.list /etc/apt/sources.list-bak \
        && echo "deb http://mirrors.aliyun.com/debian/ bullseye main non-free contrib" > /etc/apt/sources.list \
        && echo "deb-src http://mirrors.aliyun.com/debian/ bullseye main non-free contrib" >> /etc/apt/sources.list \
        && echo "deb http://mirrors.aliyun.com/debian-security/ bullseye-security main" >> /etc/apt/sources.list \
        && echo "deb-src http://mirrors.aliyun.com/debian-security/ bullseye-security main" >> /etc/apt/sources.list \
        && echo "deb http://mirrors.aliyun.com/debian/ bullseye-updates main non-free contrib" >> /etc/apt/sources.list \
        && echo "deb-src http://mirrors.aliyun.com/debian/ bullseye-updates main non-free contrib" >> /etc/apt/sources.list \
        && echo "deb http://mirrors.aliyun.com/debian/ bullseye-backports main non-free contrib" >> /etc/apt/sources.list \
        && echo "deb-src http://mirrors.aliyun.com/debian/ bullseye-backports main non-free contrib" >> /etc/apt/sources.list \
        && apt-get update && apt-get install -y \
            libfreetype6-dev \
            libjpeg62-turbo-dev \
            libpng-dev \
            zlib1g-dev \
            libzip-dev \
            vim \
            net-tools \
            iputils-ping \
            wget \
            curl \
            htop \
            git \
            unzip \
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
	&& docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install zip \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install tokenizer \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && wget "https://mirrors.aliyun.com/composer/composer.phar" \
    && chmod +x composer.phar \
    && mv composer.phar /usr/local/bin/composer \
    # 阿里云镜像加速
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ \
    && composer self-update \
    && cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini