FROM php:7.4-fpm

ARG NEWRELIC_KEY
ARG NEWRELIC_APP_NAME
ARG NEWRELIC_DAEMON_ADDRESS

RUN curl -o newrelic.tar.gz https://download.newrelic.com/php_agent/release/newrelic-php5-9.10.1.263-linux.tar.gz \
  && gzip -dc newrelic.tar.gz | tar xf - \
  && cd newrelic-php5-9.10.1.263-linux \
  && NR_INSTALL_USE_CP_NOT_LN=1 NR_INSTALL_SILENT=1 ./newrelic-install install \
  && rm -rf ../newrelic-php5-9.10.1.263-linux newrelic.tar.gz \
  && sed -i \
           -e 's/"REPLACE_WITH_REAL_KEY"/'"$NEWRELIC_KEY"'/' \
           -e 's/newrelic.appname = "PHP Application"/newrelic.appname = '"$NEWRELIC_APP_NAME"'/' \
           -e 's/;newrelic.daemon.app_connect_timeout =.*/newrelic.daemon.app_connect_timeout=15s/' \
           -e 's/;newrelic.daemon.start_timeout =.*/newrelic.daemon.start_timeout=5s/' \
           -e 's/;newrelic.daemon.address =.*/newrelic.daemon.address='"$NEWRELIC_DAEMON_ADDRESS"'/' \
           /usr/local/etc/php/conf.d/newrelic.ini