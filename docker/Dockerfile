#
# HamNetDB image with Perl & PHP
#
FROM php:8.5.1-apache

RUN apt update && \
	apt install -y \
    bash \
    ca-certificates \
    coreutils \
    curl \
    dnsutils \
    iproute2 \
    inetutils-ping \
    libapache2-mod-perl2 \
    libcgi-pm-perl \
    libdbd-mysql-perl \
    libdbi-perl \
    net-tools \
    sudo \
    tar \
    traceroute \
    tzdata \
    unzip \
    wget && \
	apt clean && \
  rm -rf /var/lib/apt/lists/* && \
  a2enmod cgi && \
  a2enmod headers

# Add install util
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

# Install additional packages
# @see https://github.com/mlocati/docker-php-extension-installer
RUN chmod +x /usr/local/bin/install-php-extensions && sync && \
    install-php-extensions \
    @composer \
    bcmath \
    bz2 \
    calendar \
    gd \
    gettext \
    gmp \
    intl \
    mcrypt \
    mysqli \
    pcntl \
    pdo_mysql \
    pspell \
    sockets \
    sysvmsg \
    sysvsem \
    sysvshm \
    tidy \
    xmlrpc \
    xsl \
    zip && \
    a2enmod rewrite

# Copy configuration
COPY root /

# Configure services
RUN a2dissite 000-default && \
  a2ensite hamnetdb
