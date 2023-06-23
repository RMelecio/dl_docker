FROM debian:bullseye

RUN apt update && apt upgrade -y
RUN apt install -y wget software-properties-common ca-certificates lsb-release apt-transport-https apache2 gnupg2 unzip git curl
COPY ./000-default.conf /etc/apache2/sites-available/000-default.conf
RUN a2enmod rewrite
RUN wget -q https://packages.sury.org/php/apt.gpg -O- | apt-key add -
RUN sh -c 'echo "deb https://packages.sury.org/php/ bullseye main" > /etc/apt/sources.list.d/php.list'
RUN apt update
RUN apt install -y php7.2
RUN apt install -y php7.2-cli php7.2-mbstring php7.2-xml php7.2-common php7.2-curl libapache2-mod-php7.2 php7.2-mcrypt php7.2-mysql php7.2-gd
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === 'e21205b207c3ff031906575712edab6f13eb0b361f2085f1f1237b7126d785e826a450292b6cfd1d64d92e6563bbde02') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
EXPOSE 80
CMD apache2ctl -D FOREGROUND
