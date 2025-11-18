# Composerのベースイメージ
FROM composer as composer

# PHPのベースイメージ（FPMでNginxと連携）
FROM php:8.3-fpm-bookworm

# Composer をインストール
COPY --from=composer /usr/bin/composer /usr/bin/composer

# 必要なシステムパッケージをインストール
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    unzip \
    default-mysql-client \
    default-libmysqlclient-dev \
    && docker-php-ext-install pdo_mysql mysqli \
    && rm -rf /var/lib/apt/lists/*

RUN useradd -ms /bin/bash phper

# php.iniをコピー
COPY ./php.ini /usr/local/etc/php/php.ini

WORKDIR /app

# アプリケーションのファイルをコピー
COPY . .

USER phper
