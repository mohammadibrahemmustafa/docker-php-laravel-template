FROM php:8.2-fpm

# Set working directory
WORKDIR /var/www/html

# Install dependencies

RUN apt-get update && apt-get install -y \
   build-essential \
   libpng-dev \
   libjpeg62-turbo-dev \
   libfreetype6-dev \
   locales \
   zip \
   jpegoptim optipng pngquant gifsicle \
   vim \
   unzip \
   git \
   curl \
   libzip-dev \
   libonig-dev \
   mysql-common \
   libldap2-dev \
   libicu-dev \
   nodejs \
   npm

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install extensions
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl \
   && docker-php-ext-install mysqli && docker-php-ext-enable mysqli \
   && docker-php-ext-install gd \
   && docker-php-ext-enable gd \
   && docker-php-ext-configure ldap \
   &&  docker-php-ext-install ldap \
   && docker-php-ext-configure intl \
   && docker-php-ext-install intl \
   && docker-php-ext-enable intl

#--------------------------------------------------------------------------
# Optional Software's Installation
#--------------------------------------------------------------------------

ARG INSTALL_NODE=true
RUN if [ ${INSTALL_NODE} = true ]; then \
   # Install NodeJS using NVM
   curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.5/install.sh | bash > /dev/null && \
   export NVM_DIR="$HOME/.nvm" > /dev/null && \
   [ -s "$NVM_DIR/nvm.sh" ] > /dev/null && . "$NVM_DIR/nvm.sh" > /dev/null && \
   nvm install 11 && \
   nvm use node \
   nvm install node-sass; \
   npm rebuild node-sass \
   ;fi

ARG INSTALL_GULP=false
RUN if [ ${INSTALL_GULP} = true ]; then \
   # Install globaly gulp
   npm install -g gulp > /dev/null \
   ;fi

ARG INSTALL_BOWER=false
RUN if [ ${INSTALL_BOWER} = true ]; then \
   # Install globaly bower
   npm install -g bower > /dev/null \
   ;fi

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer > /dev/null

ARG INSTALL_MYSQL=false
RUN if [ ${INSTALL_MYSQL} = true ]; then \
   # Install MySQL PDO
   docker-php-ext-install pdo pdo_mysql > /dev/null \
   ;fi

ARG INSTALL_POSTGRESQL=false
RUN if [ ${ISNTALL_POSTGRESQL} = true ]; then \
   # Install PostgreSQL PDO
   docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql > /dev/null && \
   docker-php-ext-install pgsql pdo_pgsql > /dev/null \
   ;fi

ARG INSTALL_GD=false
RUN if [ ${INSTALL_GD} = true ]; then \
   # Install GD library
   docker-php-ext-configure gd \
   --with-freetype-dir=/usr/include/ \
   --with-jpeg-dir=/usr/include/ \
   --with-png-dir=/usr/include/ \
   --with-xpm-dir=/usr/include/ \
   --with-webp-dir=/usr/include/ > /dev/null && \
   docker-php-ext-install gd > /dev/null \
   ;fi

ARG INSTALL_XDEBUG=false
RUN if [ ${INSTALL_XDEBUG} = true ]; then \
   # Install XDebug extention PDO
   pecl install xdebug > /dev/null && \
   docker-php-ext-enable xdebug > /dev/null \
   ;fi

ARG ADD_ALIASES=false
RUN if [ ${ADD_ALIASES} = true ]; then \
   # Install GD library
   echo 'alias sf="php app/console"' >> ~/.bashrc && \
   echo 'alias sf3="php bin/console"' >> ~/.bashrc && \
   echo 'alias lv="php artisan"' >> ~/.bashrc \
   ;fi

# RUN useradd -rm -d /home/ubuntu -s /bin/bash -g root -G sudo -u 1001 mohammad


RUN useradd -ms /bin/bash mohammad
RUN usermod -aG sudo mohammad

USER mohammad

WORKDIR /var/www/html