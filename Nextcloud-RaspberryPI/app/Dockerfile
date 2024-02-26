FROM docker.io/debian:bookworm
RUN apt update
RUN apt install -y nginx php8.2 php8.2-fpm php8.2-common php8.2-curl php8.2-opcache php8.2-xml php8.2-gd php-json php8.2-mbstring php8.2-zip openssl php8.2-mysql php8.2-bz2 php8.2-intl php-ldap php-imap php-bcmath php-apcu php-redis ffmpeg unzip python3-pymysql
COPY nginx.conf /etc/nginx/sites-enabled/default
COPY latest.zip /var/www/html/
COPY php.ini /etc/php/8.2/fpm/php.ini
COPY www.conf /etc/php/8.2/fpm/pool.d/www.conf
COPY apcu /etc/php/8.2/fpm/conf.d/20-apcu.ini
COPY opcache /etc/php/8.2/fpm/conf.d/10-opcache.ini
RUN unzip /var/www/html/latest.zip -d /var/www/html/
RUN chown www-data:www-data -R /var/www/html/nextcloud
WORKDIR /var/www/html/nextcloud
COPY ./entrypoint.sh /
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]