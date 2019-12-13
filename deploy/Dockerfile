FROM wordpress:5.3.0

# New Relic PHP Agent Download Link
ENV AGENT_DOWNLOAD_LINK=https://download.newrelic.com/php_agent/release/newrelic-php5-8.5.0.235-linux.tar.gz

# New Relic Application Details
ENV NR_LICENSE_KEY=YOUR_LICENSE_KEY
ENV NR_APPLICATION_NAME=YOUR_APPLICATION_NAME

# Install New Relic
RUN curl -L ${AGENT_DOWNLOAD_LINK} | tar -C /tmp -zx && \
	export NR_INSTALL_USE_CP_NOT_LN=1 && \
	export NR_INSTALL_SILENT=1 && \
	cd /tmp/newrelic-php5-* && \
	/bin/sh newrelic-install install && \
	rm -rf /tmp/newrelic-php5-* /tmp/nrinstall* && \
	sed -i -e 's/"REPLACE_WITH_REAL_KEY"/"${NR_LICENSE_KEY}"/' \
			-e 's/newrelic.appname = "PHP Application"/newrelic.appname = "${NR_APPLICATION_NAME}"/' \
			/usr/local/etc/php/conf.d/newrelic.ini

# Enable Apache mod_headers
RUN a2enmod headers && \
	service apache2 restart
