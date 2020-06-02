FROM ubuntu:18.04

RUN apt-get update
RUN apt install -yq apache2

#ENV TZ Europe/Madrid
RUN DEBIAN_FRONTEND="noninteractive" apt-get -yq install tzdata

RUN apt-get update
RUN apt-get -y install software-properties-common
RUN LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php
RUN apt-get update
RUN apt-get -yq install php7.3
RUN apt-get -yq install php-pear
RUN apt-get update
RUN apt-get -yq install php7.3-dev
RUN apt-get -yq install php7.3-zip
RUN apt-get -yq install php7.3-curl
RUN apt-get -yq install php7.3-gd
RUN apt-get -yq install php7.3-mysql
#RUN apt-get -yq install php7.3-mcrypt
RUN apt-get -yq install php7.3-xml
RUN apt-get -yq install php7.3-fpm
RUN apt-get -yq install php7.3-cli
RUN apt-get -yq install php7.3-cgi
RUN apt-get -yq install php7.3-intl
RUN apt-get -yq install php7.3-mbstring
#RUN apt-get -yq install libapache2-mod-php7.3

RUN apt-get update
RUN apt-get -yq install nano

RUN pecl install xdebug
RUN export PHP_IDE_CONFIG="serverName=PHPSTORM"

RUN apt-get update
RUN apt-get -yq install nodejs
RUN apt-get -yq install npm
# RUN ln -s /usr/bin/nodejs /usr/bin/node

RUN apt-get update
RUN apt-get -yq install openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:123123' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]


RUN apt-get -yq install composer



RUN a2enmod rewrite

# CMD /etc/init.d/php7.3-fpm start && \
#     /etc/init.d/apache2 start && \
#     tail -f /dev/null
CMD ["apachectl", "-D", "FOREGROUND"]
