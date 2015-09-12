FROM nginx:1.7
MAINTAINER Luc Michalski <michalski.luc@gmail.com>

# Install htpasswd utility and curl
RUN apt-get update \
    && apt-get install -y apache2-utils wget \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install Kibana
RUN mkdir -p /var/www
WORKDIR /var/www

ENV KIBANA_VERSION 4.1.1

# Fetch Kibana:
# - Install curl so we can fetch the kibana code
# - Fetch the Kibana code to the kibana home directory (/kibana)
# - Fetch a default kibana configuration file - which should be customized for running as a Docker container, if applies...
# - Fetch an nginx configuration customized to run exclusively the kibana 3 app
# - Uninstall curl & curl dependencies, as it is no longer required.
RUN  apt-get update && apt-get install -y curl ca-certificates --no-install-recommends \
  && wget "https://download.elasticsearch.org/kibana/kibana/kibana-$KIBANA_VERSION-linux-x64.tar.gz" \
  && tar -xvf kibana-$KIBANA_VERSION-linux-x64.tar.gz \
  && mv kibana-$KIBANA_VERSION-linux-x64 kibana

ADD config/kibana.yml  /var/www/kibana/config/kibana.yml

# Add default credentials
RUN htpasswd -cb /etc/nginx/.htpasswd kibana "docker"

RUN echo 0 >/selinux/enforce

# Copy Nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf

# VOLUME ["/var/www/kibana/config"]

# Set wrapper for runtime config
COPY init.sh /init
ENTRYPOINT ["/init"]

# Run nginx
CMD ["nginx", "-g", "daemon off;"]
