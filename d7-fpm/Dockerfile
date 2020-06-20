FROM drupal:7-fpm

# set timezone
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update -y \
    && apt-get install -y git vim nginx \
    && apt-get clean

ENV DRUSH_VERSION 8.3.5
    ## Install composer
RUN curl -sS https://getcomposer.org/installer | \
    php -- --install-dir=/usr/bin/ --filename=composer \
    ## Install drush
    && curl -L --silent https://github.com/drush-ops/drush/releases/download/${DRUSH_VERSION}/drush.phar \
    > /usr/local/bin/drush && chmod +x /usr/local/bin/drush

## Install drush-launcher
# RUN wget -O /usr/local/bin/drush https://github.com/drush-ops/drush-launcher/releases/latest/download/drush.phar \
#   && chmod +x /usr/local/bin/drush

# RUN pecl install xdebug-2.6.0 \
#     && docker-php-ext-enable xdebug

EXPOSE 80
EXPOSE 443

COPY ./conf.d/site.conf /etc/nginx/conf.d/
COPY php-upload.ini /usr/local/etc/php/conf.d/php-uploads.ini
COPY entrypoint.sh /etc/entrypoint.sh

ENTRYPOINT ["sh", "/etc/entrypoint.sh"]
