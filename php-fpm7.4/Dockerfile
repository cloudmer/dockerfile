FROM php:7.4.30-fpm
RUN apt-get update && apt-get install -y \
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
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
	&& docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install zip \
    && docker-php-ext-install bcmath \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && wget "https://mirrors.aliyun.com/composer/composer.phar" \
    && chmod +x composer.phar \
    && mv composer.phar /usr/local/bin/composer \
    # 阿里云镜像加速
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ \
    && composer self-update \
    && cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini