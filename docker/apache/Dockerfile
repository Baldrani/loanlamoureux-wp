FROM wordpress:php7.0

# Xdebug
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

# Installs sendmail
RUN apt-get update && apt-get -q -y install ssmtp mailutils && rm -rf /var/lib/apt/lists/*

# set up sendmail config
RUN echo "hostname=localhost" > /etc/ssmtp/ssmtp.conf
RUN echo "root=<your email address>" >> /etc/ssmtp/ssmtp.conf
RUN echo "mailhub=maildev" >> /etc/ssmtp/ssmtp.conf
# The above 'maildev' is the name you used for the link command
# in your docker-compose file or docker link command.
# Docker automatically adds that name in the hosts file
# of the container you're linking MailDev to.

# Set up php sendmail config
RUN echo "sendmail_path=sendmail -i -t" >> /usr/local/etc/php/conf.d/php-sendmail.ini

# Fully qualified domain name configuration for sendmail on localhost.
# Without this sendmail will not work.
# This must match the value for 'hostname' field that you set in ssmtp.conf.
RUN echo "localhost localhost" >> /etc/hosts