##############################################################################
# Primeiro cria uma imagem no php7.14 cli e chama ele de builder, 
# depois instala o que precisa, e por fim instala o laravel
##############################################################################
FROM  php:7.4-cli AS builder

WORKDIR /var/www

RUN apt-get update && \
	apt-get install libzip-dev -y && \
	docker-php-ext-install zip

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');"

RUN php composer.phar create-project --prefer-dist laravel/laravel laravel

##############################################################################
# Depois de instalar o laravel, cria outra imagem alpine, que é um linux compacto,
# mas sem apt-get, por isso a primeira imagem, e copia o laravel criado em builder, para essa nova imagem.
##############################################################################
FROM php:7.4-fpm-alpine

WORKDIR /var/www

RUN rm -rf /var/www/html

COPY --from=builder /var/www/laravel .

#criado indice simbolico
RUN ln -s public html

RUN chown -R www-data:www-data /var/www

# 9000 é a porta do php-fpm
EXPOSE 9000

# vai fazer o php ficar "ouvindo" o nginx
CMD ["php-fpm"]