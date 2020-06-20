FROM dravenk/dp-fpm
COPY ./conf.d/site.conf /etc/nginx/conf.d/

WORKDIR /var/www/html

RUN rm -rf * && rm -rf .*; \
  composer create-project drupal/recommended-project:^9.0 . -vvv; \
  chown -R www-data:www-data web/sites web/modules web/themes
