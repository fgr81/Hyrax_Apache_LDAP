FROM --platform=amd64 ubuntu:22.04 

ARG AUTH_LDAP_URL
ARG AUTH_LDAP_BIND_DN
ARG AUTH_LDAP_BIND_PASSWORD
ARG HOSTNAME
ARG SERVER_ADMIN_MAIL

ENV AUTH_LDAP_URL $AUTH_LDAP_URL
ENV AUTH_LDAP_BIND_DN $AUTH_LDAP_BIND_DN
ENV AUTH_LDAP_BIND_PASSWORD $AUTH_LDAP_BIND_PASSWORD
ENV HOSTNAME $HOSTNAME
ENV SERVER_ADMIN_MAIL $SERVER_ADMIN_MAIL

ENV DEBIAN_FRONTEND=noninteractive 

RUN apt-get update && apt-get -y install certbot python3-certbot-apache cron rsyslog
RUN apt-get -y install libapache2-mod-authnz-external

# Add periodic renew task of certificates
RUN crontab /etc/cron.d/certbot

# Enable cron logs via rsyslog
RUN sed -i \
    -e 's,^#\(cron.*\)$,\1,' \
    -e 's,^\(module.*imklog.*\)$,#\1,' \
    /etc/rsyslog.conf

RUN rm -f /etc/apache2/sites-available/*.conf

COPY conf/site.conf /etc/apache2/sites-available/
RUN sed -i 's#{{HOSTNAME}}#'"$HOSTNAME"'#g' /etc/apache2/sites-available/site.conf
RUN sed -i 's#{{SERVER_ADMIN_MAIL}}#'"$SERVER_ADMIN_MAIL"'#g' /etc/apache2/sites-available/site.conf
RUN a2ensite site

COPY conf/hyrax.conf     /etc/apache2/conf-available/
RUN a2enconf hyrax

COPY conf/ldap.conf      /etc/apache2/conf-available/
RUN sed -i 's#{{AUTH_LDAP_URL}}#'"$AUTH_LDAP_URL"'#g' /etc/apache2/conf-available/ldap.conf
RUN sed -i 's#{{AUTH_LDAP_BIND_DN}}#'"${AUTH_LDAP_BIND_DN}"'#g' /etc/apache2/conf-available/ldap.conf
RUN sed -i 's#{{AUTH_LDAP_BIND_PASSWORD}}#'"${AUTH_LDAP_BIND_PASSWORD}"'#g' /etc/apache2/conf-available/ldap.conf
RUN a2enconf ldap

RUN a2enmod proxy_http
RUN a2enmod proxy_ajp
RUN a2enmod proxy
RUN a2enmod ssl
RUN a2enmod ldap
RUN a2enmod authnz_ldap
RUN a2enmod authnz_external

#RUN apache2ctl restart

COPY launcher.sh /usr/local/bin/launcher.sh
RUN chmod +x /usr/local/bin/launcher.sh

CMD ["/usr/local/bin/launcher.sh"]
