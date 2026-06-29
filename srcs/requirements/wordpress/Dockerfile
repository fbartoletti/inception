FROM alpine:3.24.0

RUN apk update && apk add --no-cache \
        php82 \
        php82-fpm \
        php82-mysqli \
        php82-json \
        php82-curl \
        php82-dom \
        php82-exif \
        php82-fileinfo \
        php82-mbstring \
        php82-openssl \
        php82-xml \
        php82-zip \
        php82-phar \
        php82-iconv \
        php82-tokenizer \
        php82-session \
        php82-ctype \
        curl \
        bash \
        mariadb-client \
    && ln -sf /usr/sbin/php-fpm82 /usr/sbin/php-fpm \
    && ln -sf /usr/bin/php82 /usr/bin/php \
    && rm -rf /var/cache/apk/*

# wp-cli
RUN curl -fsSL -o /usr/local/bin/wp \
        https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
    && chmod +x /usr/local/bin/wp

COPY conf/www.conf /etc/php82/php-fpm.d/www.conf
COPY tools/entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh

RUN mkdir -p /var/www/html /run/php \
    && chown -R nobody:nobody /var/www/html /run/php

WORKDIR /var/www/html

EXPOSE 9000

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
CMD ["php-fpm", "-F"]
