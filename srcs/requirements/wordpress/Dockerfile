FROM debian:bookworm

ENV PHP_VERSION=8.2

RUN mkdir -p /run/php

RUN	apt-get update -y && apt-get upgrade -y

RUN apt-get install -y mariadb-client && \
	apt-get install -y \
	curl \
	wget \
	php${PHP_VERSION} \
	php${PHP_VERSION}-cgi \
	php${PHP_VERSION}-mysql \
	php${PHP_VERSION}-fpm \
	php${PHP_VERSION}-pdo \
	php${PHP_VERSION}-gd \
	php${PHP_VERSION}-cli \
	php${PHP_VERSION}-mbstring \
	&& rm -rf /var/lib/apt/lists/*

RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
	&& chmod +x wp-cli.phar \
	&& mv wp-cli.phar /usr/local/bin/wp

COPY ./conf/www.conf /etc/php/${PHP_VERSION}/fpm/pool.d/

RUN mkdir -p /var/www/html
WORKDIR /var/www/html

RUN chmod -R 755 /var/www/html && \
	chown -R www-data:www-data /var/www/html

COPY ./tools/run_wordpress.sh /
RUN chmod +x /run_wordpress.sh

EXPOSE 9000

CMD [ "/run_wordpress.sh"]
