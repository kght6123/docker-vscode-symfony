FROM php:7-alpine3.6
LABEL maintainer="kght6123"

RUN apk --update --no-cache add $PHPIZE_DEPS \
unzip git vim wget shadow icu-dev sudo \
freetype-dev libjpeg-turbo-dev libpng-dev

RUN docker-php-ext-install intl gd

# add docker sudo user
RUN groupadd -g 1000 docker && \
    useradd  -g      docker -m -s /bin/bash docker && \
    echo 'docker:docker' | chpasswd

RUN echo 'Defaults visiblepw'            >> /etc/sudoers
RUN echo 'docker ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# copy php.ini
COPY ./php.ini /usr/local/etc/php/

# install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"

# create project folder
RUN mkdir -p /home/docker/project/symfony

# change packagist.jp
RUN composer config -g repos.packagist composer https://packagist.jp

# install prestissimo plugin
RUN composer global require hirak/prestissimo

# install xdebug
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug
# RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/php.ini

# copy xdebug.ini
COPY ./xdebug.ini /usr/local/etc/php/conf.d/

# 以降は、rootではなくdockerユーザで実行される
# ENV HOME /home/docker
# WORKDIR /home/docker
# USER docker
