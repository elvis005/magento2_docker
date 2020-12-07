FROM php:7.4-cli

# COPY ./sources.list.buster /etc/apt/sources.list
# uncomment the above line if you are in China mainland

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
    libzip-dev \
    git \
    zip \
    vim \
    libzookeeper-mt-dev

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

RUN pecl install zookeeper-0.7.1
RUN docker-php-ext-enable zookeeper

RUN curl --silent --show-error https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --version=1.10.6

RUN apt-get install -y rsyslog && apt-get clean

#job filedocc
ADD crontab /etc/cron.d/cron
ADD start.sh /start.sh

RUN chmod +x /start.sh; \
  touch /var/log/syslog; \
  touch /var/log/cron.log;

RUN sed -i '/imklog/s/^/#/' /etc/rsyslog.conf

RUN chmod 0644 /etc/cron.d/cron
RUN crontab -u www-data /etc/cron.d/cron

CMD "/start.sh"