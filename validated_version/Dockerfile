# **************************************************************************** #
#                                                                              #
#                                                         :::      ::::::::    #
#    Dockerfile                                         :+:      :+:    :+:    #
#                                                     +:+ +:+         +:+      #
#    By: pmaldagu <marvin@42.fr>                    +#+  +:+       +#+         #
#                                                 +#+#+#+#+#+   +#+            #
#    Created: 2020/02/20 15:40:33 by pmaldagu          #+#    #+#              #
#    Updated: 2020/03/03 17:39:23 by pmaldagu         ###   ########.fr        #
#                                                                              #
# **************************************************************************** #

FROM debian:buster

MAINTAINER Pierre Maldague <pmaldagu@student.s19.be>

# ----- Install (LEMP & Others) --------
# Utils
RUN apt-get update -y \
	&& apt-get install vim -y \
	&& apt-get install wget -y \
	&& apt-get install curl -y 

# Nginx
RUN apt-get install nginx -y

# mySQL
# système de gestion de base de données.
RUN apt-get install mariadb-server -y

# Php
RUN apt-get install php -yq \
	&& apt-get install php-mysql -yq \
	&& apt install php7.3 php7.3-fpm php7.3-mysql php-common php7.3-cli php7.3-common php7.3-json php7.3-opcache php7.3-readline -yq \
	&& apt install php-json php-mbstring -y

# Phpmyadmin
# application Web de gestion pour les systèmes de gestion de base de données MySQL
RUN wget https://files.phpmyadmin.net/phpMyAdmin/5.0.1/phpMyAdmin-5.0.1-all-languages.tar.gz
RUN	tar -zxzf phpMyAdmin-5.0.1-all-languages.tar.gz \
	&& mv phpMyAdmin-5.0.1-all-languages /var/www/html/phpMyAdmin \
	&& rm phpMyAdmin-5.0.1-all-languages.tar.gz \
	&& mkdir /var/www/html/phpMyAdmin/tmp \
	&& chmod 777 /var/www/html/phpMyAdmin/tmp

# install SSL
# protocoles de sécurisation des échanges
RUN wget https://github.com/FiloSottile/mkcert/releases/download/v1.1.2/mkcert-v1.1.2-linux-amd64
RUN mv mkcert-v1.1.2-linux-amd64 mkcert \
	&& chmod 777 /mkcert && /mkcert -install && /mkcert localhost.com

# Wordpress
RUN cd /tmp \ 
	&& curl -LO https://wordpress.org/latest.tar.gz \
	&& tar xzvf latest.tar.gz \
	&& mkdir /var/www/html/wordpress \
	&& cp -a /tmp/wordpress/. /var/www/html/wordpress \
	&& chown -R www-data:www-data /var/www/

# ------ Remove Samples -------
RUN rm /var/www/html/phpMyAdmin/config.sample.inc.php
RUN rm var/www/html/index.nginx-debian.html
RUN rm var/www/html/wordpress/wp-config-sample.php

# ------ Copy Sources -------
ADD /srcs/nginx.conf /etc/nginx/sites-available/
ADD /srcs/nginx.conf /etc/nginx/sites-enabled/
ADD /srcs/config.inc.php /var/www/html/phpMyAdmin
ADD srcs/wp-config.php /var/www/html/wordpress
ADD /srcs/index.html /var/www/html/
ADD /srcs/mysql_db_config.sh ./

# ------ Start Services --------
RUN service nginx start \
&& service php7.3-fpm start \
&& service mysql start

# L'instruction EXPOSE permet d'indiquer le port sur lequel votre application écoute
# 443 est le port https
EXPOSE 80 443

# placer en dernière ligne pour plus de compréhension
# permet à notre conteneur de savoir quelle commande il doit exécuter lors de son démarrage
CMD /bin/bash ./mysql_db_config.sh && sleep infinity & wait
