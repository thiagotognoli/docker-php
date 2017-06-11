FROM php5.6-fpm-zts-alpine
MAINTAINER Thiago Tognoli <t@t>

###### default build deps
RUN	apk add --no-cache --virtual .default-build-deps \
		$PHPIZE_DEPS

###### iconv install
RUN \
	docker-php-ext-install -j "$(getconf _NPROCESSORS_ONLN)" iconv

###### mcrypt install
RUN \
	apk add --no-cache \
		libmcrypt \
	&& apk add --no-cache --virtual .build-deps \
		libmcrypt-dev \
	&& docker-php-ext-install -j "$(getconf _NPROCESSORS_ONLN)" mcrypt \
	&& apk del .build-deps

###### gd install
RUN \
	apk add --no-cache \
		freetype \
		libpng \
		libjpeg-turbo \
	&& apk add --no-cache --virtual .build-deps \
		freetype-dev \
		libpng-dev \
		libjpeg-turbo-dev \
	&& docker-php-ext-configure gd \
		--with-freetype-dir=/usr/include/ \
		--with-png-dir=/usr/include/ \
		--with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j "$(getconf _NPROCESSORS_ONLN)" gd \
	&& apk del .build-deps
	
###### pthreads install
RUN \
	pecl install pthreads-2.0.10 \
	&& docker-php-ext-enable  pthreads
	
###### xdebug install
RUN \
	pecl install xdebug \
    && docker-php-ext-enable xdebug
	
###### clear
RUN \
	apk del .default-build-deps \
	&& apk del --no-cache \
	&& rm -rf  /tmp/* /var/tmp/* /var/cache/apk/*


EXPOSE 8000

COPY src/. /usr/src/myapp
WORKDIR /usr/src/myapp
#CMD [ "php", "./teste.php" ]
#CMD [ "/bin/sh" ] 
CMD [ "php", "-S", "0.0.0.0:8000" ]

#--enable-debug
		
#	&& sed -i "s/^;date.timezone =$/date.timezone = \"UTC\"/" /usr/local/lib/php.ini \

#&& echo "xdebug.remote_enable=on\n" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo "xdebug.remote_autostart=off\n" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo "xdebug.remote_port=9000\n" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo "xdebug.remote_handler=dbgp\n" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo "xdebug.remote_connect_back=0\n" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    
    
    
    
#RUN \
#    && docker-php-source extract \
#	&& docker-php-source delete \
##clear install
#	&& apk del --no-cache \
##install support to gd
#		freetype-dev \
#		libpng-dev \
#		libjpeg-turbo-dev \
##install support to mcrypt
#		libmcrypt-dev
 


#gd iconv opcache readline soap xml mysqli curl json mcrypt curl redis mbstring xdebug zip

#RUN apk add --no-cache --virtual .build-deps \
#            # for all
#            zlib-dev \
