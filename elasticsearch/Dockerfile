FROM java:8-jre
MAINTAINER Luc Michalski <luc.michalski@blippar.com>

# Install ElasticSearch
ENV ES_VERSION 1.7.1
RUN curl -s https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-$ES_VERSION.tar.gz | tar --transform "s/^elasticsearch-$ES_VERSION/elasticsearch/" -xvz -C /opt

# Define working directory
WORKDIR /opt/elasticsearch

# Add custom elasticsearch.yml config
COPY elasticsearch.yml config/elasticsearch.yml

RUN bin/plugin -install royrusso/elasticsearch-HQ && \
    bin/plugin -install elasticsearch-flavor --url 'https://github.com/f-kubotar/elasticsearch-flavor/releases/download/v0.0.3/elasticsearch-flavor-0.0.3.zip' --install flavor

# Elasticsearch HTTP
EXPOSE 9200

# Elasticsearch transport (cluster)
EXPOSE 9300

# Persistance
VOLUME ["/data"]

# Run
CMD ["bin/elasticsearch"]
