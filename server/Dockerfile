FROM michaelsauter/php-base
MAINTAINER Michael Sauter, mail@michaelsauter.net

ENV REFRESHED_AT 2014-02-19
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
RUN apt-get update

RUN DEBIAN_FRONTEND=noninteractive apt-get install -q -y nginx php5-fpm

# PHP config
RUN sed -i -e "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" /etc/php5/fpm/php.ini
RUN sed -i -e "s/listen = 127.0.0.1:9000/listen = \/var\/run\/php5-fpm.sock/g" /etc/php5/fpm/pool.d/www.conf

# Cleanup
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# nginx config
ADD ./nginx.conf /etc/nginx/nginx.conf
ADD ./default /etc/nginx/sites-available/default

EXPOSE 80

WORKDIR /srv/www

CMD composer install && service php5-fpm start && nginx