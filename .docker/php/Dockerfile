# ベースイメージ取得
FROM php:8.1.3-fpm-bullseye

# 現在のイメージよりも上にある新しい例やでコマンドを実行し、その結果をコミットします。
# 結果が確定されたイメージは、Dockerfileの次のステップで使われる。
# apt-getコマンドは、DebianやUbuntuのパッケージ管理システムであるAPTライブラリを利用してパッケージを操作、管理するコマンド。
# CentOSやFedoraのパッケージ管理には「yumコマンド」を利用する。

RUN apt-get update \
        && apt-get install -y \
            bash \
            git \
            nodejs \
            npm \
            libzip-dev \
            libpng-dev \
            autoconf \
        && git clone https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis \
        && docker-php-ext-install \
            zip \
            pdo_mysql \
            sockets \
            redis \
        && docker-php-ext-enable opcache

# 追加したいファイルディレクトリを<コピー元>で指定すると、これらをイメージのファイルシステム上のパス<コピー先>に追加する。
# COPY <コピー元>, <コピー先>
COPY --from=composer:2.2.10 /usr/bin/composer /usr/bin/composer

# フォルダ作成
RUN mkdir /app
# Dockerfile内で以降に続く処理時に使う作業ディレクトリを指定する。
# WorkDirが存在しなければ作成される。
WORKDIR /app
