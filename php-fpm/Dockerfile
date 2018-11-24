FROM alpine:3.8

RUN apk add --no-cache openssh-client php7-fpm curl

# essential php libs
RUN apk add --no-cache \
    php7-curl \
    php7-dom \
    php7-gd \
    php7-ctype \
    php7-zip \
    php7-xml \
    php7-iconv \
    php7-sqlite3 \
    php7-mysqli \
    php7-pgsql \
    php7-json \
    php7-phar \
    php7-openssl \
    php7-pdo \
    php7-pdo_mysql \
    php7-session \
    php7-mbstring \ 
    php7-bcmath \ 
    php7-tokenizer \ 
    php7-fileinfo

# Environments
ARG TIMEZONE
ARG PHP_MEMORY_LIMIT
ARG MAX_UPLOAD
ARG PHP_MAX_FILE_UPLOAD
ARG PHP_MAX_POST

RUN sed -i "s|;*daemonize\s*=.*|daemonize = no|g" /etc/php7/php-fpm.conf && \
	# sed -i "s|;*run/php/php7.2-fpm.sock|listen = 9000|g" /etc/php7/php-fpm.d/www.conf && \
	sed -i "s|;*listen\s*=.*|listen = 9000|g" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|;*user\s*=.*|user = 1000|g" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|;*group\s*=.*|group = 1000|g" /etc/php7/php-fpm.d/www.conf && \
	sed -i "s|;*date.timezone =.*|date.timezone = ${TIMEZONE}|i" /etc/php7/php.ini && \
	sed -i "s|;*memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|i" /etc/php7/php.ini && \
    sed -i "s|;*upload_max_filesize =.*|upload_max_filesize = ${MAX_UPLOAD}|i" /etc/php7/php.ini && \
    sed -i "s|;*max_file_uploads =.*|max_file_uploads = ${PHP_MAX_FILE_UPLOAD}|i" /etc/php7/php.ini && \
    sed -i "s|;*post_max_size =.*|post_max_size = ${PHP_MAX_POST}|i" /etc/php7/php.ini && \
    sed -i "s|;*cgi.fix_pathinfo=.*|cgi.fix_pathinfo= 0|i" /etc/php7/php.ini

# Set Workdir
RUN mkdir /www
WORKDIR /www

# Expose volumes
VOLUME ["/www"]

# Expose ports
EXPOSE 9000

# Entry point
ENTRYPOINT ["/usr/sbin/php-fpm7"]