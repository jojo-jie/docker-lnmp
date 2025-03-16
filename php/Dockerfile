FROM php:7.4-fpm
MAINTAINER walker "2725445401@qq.com"
 
# 设置时区
ENV TZ=Asia/Shanghai

# 安装依赖包和PHP核心拓展
RUN set -eux; \
    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libxml2-dev \
        libssl-dev \
        libz-dev \
        libzip-dev \
        libmemcached-dev \
        zlib1g-dev \
        procps \
        net-tools; \
    # 配置和安装PHP扩展
    docker-php-ext-configure gd --with-jpeg=/usr/include --with-freetype=/usr/include/freetype2/; \
    docker-php-ext-install -j$(nproc) \
        gd \
        zip \
        bcmath \
        pdo_mysql \
        opcache \
        mysqli \
        pcntl \
        soap \
        shmop; \
    # 安装PECL扩展
    pecl install redis mongodb-1.20.1 memcached; \
    docker-php-ext-enable redis mongodb memcached; \
    # 清理
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false; \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# 安装composer
COPY composer.phar /usr/local/bin/composer
RUN chmod 755 /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ \
    && composer selfupdate

WORKDIR /var/www

# 设置权限
RUN usermod -u 1000 www-data