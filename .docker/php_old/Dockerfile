FROM php:8.2-fpm

RUN  apt-get update -y \
    && apt-get install -y apt-utils  \
    && apt-get install -y curl \
    && apt-get install -y unzip \
    && apt-get install -y dbconfig-common \
    && apt-get install -y libcurl4-openssl-dev \
    && apt-get install -y libfreetype6-dev \
    && docker-php-ext-install pdo_mysql

RUN docker-php-ext-configure exif \
	&& docker-php-ext-install exif \
	&& docker-php-ext-enable exif \
	&& docker-php-ext-install bcmath


#instalando Node
ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION v18.17.0

# install nvm
# https://github.com/creationix/nvm#install-script
RUN curl --silent -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.2/install.sh | bash

# install node and npm
RUN rm /bin/sh && ln -s /bin/bash /bin/sh
RUN source $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default

# add node and npm to path so the commands are available
ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# INSTALL EXT-ZIP
RUN apt-get install -y \
    libzip-dev \
    zip \
    && docker-php-ext-install zip

WORKDIR /var/www/html

USER 1000
