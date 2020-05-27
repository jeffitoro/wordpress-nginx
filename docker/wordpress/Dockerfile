FROM wordpress:php7.4-fpm-alpine

RUN apk update && \
    apk upgrade && \
    apk add nginx && \
    apk add php-mysqli && \
    mkdir /run/nginx;

RUN apk --no-cache add \
    curl \
    bash \
    less

### WP-CLI Installation
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
    chmod +x wp-cli.phar && \
    mv wp-cli.phar /usr/bin/wp && \
    chown nginx:www-data /usr/bin/wp && \
    \
    ### Cleanup
    rm -rf /var/cache/apk/*

# nginx conf
ADD docker/wordpress/config/default.conf /etc/nginx/conf.d/default.conf

# entrypoint run php-fpm and nginx
COPY docker/wordpress/config/start.sh /opt
RUN chmod +x /opt/start.sh
CMD [ "/opt/start.sh" ]

WORKDIR /var/www/html