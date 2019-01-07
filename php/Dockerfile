FROM php:7.1-fpm

# Get repository and install wget and vim
RUN apt-get update && apt-get install -y \
    wget \
    apt-utils \
    gnupg \
    software-properties-common \
    apt-transport-https \
    libxml2-dev \
    unixodbc-dev

# necessário para sqlsrv
RUN wget -qO - https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && wget -qO - https://packages.microsoft.com/config/debian/9/prod.list \
        > /etc/apt/sources.list.d/mssql-release.list

# Install PHP extensions deps
RUN apt-get update \
&& apt-get install --no-install-recommends -y \
libfreetype6-dev \
libjpeg62-turbo-dev \
libmcrypt-dev \
libpng-dev \
zlib1g-dev \
libicu-dev \
g++ \
unixodbc-dev \
&& ACCEPT_EULA=Y apt-get install --no-install-recommends -y msodbcsql17 mssql-tools \
&& apt-get install --no-install-recommends -y libxml2-dev \
libaio-dev \
libmemcached-dev \
freetds-dev \
libssl-dev \
openssl \
supervisor

# Install PHP extensions
RUN pecl install sqlsrv pdo_sqlsrv

# PRA VER SE TEM ALGUM BUG NO PHP
# RUN php -i | grep "Configure Command"

RUN docker-php-ext-install \
iconv \
mcrypt \
sockets \
pdo \
pdo_mysql \
&& docker-php-ext-enable \
sqlsrv \
pdo_sqlsrv

# Clean repository
RUN apt-get autoremove -y && \
apt-get clean && \
rm -rf /var/lib/apt/lists/*