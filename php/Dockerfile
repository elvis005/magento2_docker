FROM php:7.4-fpm

#COPY ./sources.list.buster /etc/apt/sources.list
#uncomment above line if your server is in China mainland

ADD cacert.pem /var/www/html/cacert.pem

RUN ln -fs /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
#Change the timezone according to your own requirement

# install libraries required by the extensions
RUN apt-get update \
  && apt-get install -y \
    cron \
    libicu-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libxslt1-dev \
    libfreetype6-dev \
    zlib1g-dev \
    libonig-dev \
    libzip-dev

# install extensions
RUN docker-php-ext-configure gd \
    --with-jpeg \
    --with-freetype && \
    docker-php-ext-install \
      bcmath \
      gd \
      intl \
      mbstring \
      pdo_mysql \
      soap \
      xsl \
      zip \
      sockets \
      opcache


WORKDIR /var/www/html

CMD ["php-fpm", "-R"]

