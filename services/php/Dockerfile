FROM php:7.1-fpm

# updates
RUN apt-get update && apt-get install -y \
    libmcrypt-dev \
    libxml2-dev \
    libssl-dev \
    libpq-dev \
    libbz2-dev \
    libpng-dev \
    libjpeg-dev \
    libgmp-dev \
    git

# extensions
RUN docker-php-ext-install opcache && \
    docker-php-ext-install zip && \
    docker-php-ext-install bz2 && \
    docker-php-ext-install iconv && \
    docker-php-ext-install calendar && \
    docker-php-ext-install dom && \
    docker-php-ext-install gd && \
    docker-php-ext-install mbstring && \
    docker-php-ext-install mcrypt && \
    docker-php-ext-install mysqli && \
    docker-php-ext-install pdo pdo_mysql && \
    docker-php-ext-install bcmath && \
    docker-php-ext-install gmp


RUN apt-get install -y build-essential libssl-dev zlib1g-dev libpng-dev libjpeg-dev libfreetype6-dev

# pecl
RUN pecl install mongodb && \
    echo "extension=mongodb.so" > /usr/local/etc/php/conf.d/ext-mongodb.ini

# APC
RUN pecl install apcu && \
    echo "extension=apcu.so" > /usr/local/etc/php/conf.d/apcu.ini

# xdebug
ARG XDEBUG_ON=true
ARG XDEBUG_REMOTE_HOST=127.0.0.1
RUN if [ ${XDEBUG_ON} = true ]; then \
    pecl install xdebug && \
    docker-php-ext-enable xdebug && \
    echo "xdebug.default_enable = 1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_enable = 1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_autostart = 1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_connect_back = 1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.profiler_enable = 0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_host = ${XDEBUG_REMOTE_HOST}" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_port = 9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    ;fi

# Install Tideways and Configure
RUN cd /usr/src && \
    git clone https://github.com/tideways/php-profiler-extension.git && \
    cd php-profiler-extension && \
    git checkout tags/v4.1.4 && \
    /usr/local/bin/phpize && \
    ./configure  CFLAGS="-O2 -g" --enable-tideways  --enable-shared  --with-php-config=/usr/local/bin/php-config && \
    make -j `cat /proc/cpuinfo | grep processor | wc -l` && \
    make install

RUN docker-php-ext-enable tideways

RUN echo "tideways.api_key=0" >> /usr/local/etc/php/conf.d/docker-php-ext-tideways.ini
RUN echo "tideways.auto_prepend_library=0" >> /usr/local/etc/php/conf.d/docker-php-ext-tideways.ini
RUN echo "tideways.auto_start=0" >> /usr/local/etc/php/conf.d/docker-php-ext-tideways.ini

RUN groupadd -g 1000 appuser && \
    useradd -r -u 1000 -g appuser appuser

# USER appuser

# mark volume/s as externally mounted
VOLUME ["/var/www"]

# starting point
WORKDIR /var/www

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

# make web server connect to this port
EXPOSE 9000

CMD ["php-fpm"]
