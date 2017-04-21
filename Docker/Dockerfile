FROM romeoz/docker-apache-php:7.1
WORKDIR /var/www/app/

RUN apt-get update
RUN apt-get install -y software-properties-common python-software-properties php7.1 php-mbstring php7.1-dev apt-transport-https net-tools

RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

RUN  apt-get update
RUN  ACCEPT_EULA=Y apt-get install -y msodbcsql mssql-tools 
RUN  apt-get install -y unixodbc-dev
RUN echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
RUN echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
#RUN source ~/.bashrc

RUN pecl install sqlsrv-4.1.6.1
RUN pecl install pdo_sqlsrv-4.1.6.1

COPY docker_config/php.ini /etc/php/7.1/apache2/
COPY docker_config/php.ini /etc/php/7.1/cli/
COPY docker_config/app.conf ${APACHE_CONF_DIR}/sites-enabled/app.conf

ENV PHP_APP_DIR=/var/www/app

EXPOSE 80

CMD ["/sbin/entrypoint.sh"]
