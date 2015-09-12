FROM java:8-jre
MAINTAINER Michalski Luc <michalski.luc@gmail.com>

# Install Logstash
ENV LOGSTASH_VERSION 1.5.4
RUN mkdir -p /opt
WORKDIR /opt/
RUN wget https://download.elasticsearch.org/logstash/logstash/logstash-$LOGSTASH_VERSION.tar.gz && \
    tar -xvf logstash-$LOGSTASH_VERSION.tar.gz && \
    mv logstash-$LOGSTASH_VERSION logstash && \
    cd ./logstash && \
    ./bin/plugin install logstash-filter-geoip && \
    ./bin/plugin install logstash-output-elasticsearch && \
    ./bin/plugin install logstash-output-lumberjack && \
    ./bin/plugin install logstash-patterns-core && \
    ./bin/plugin install logstash-filter-mutate && \
    ./bin/plugin install logstash-filter-csv && \
    ./bin/plugin install logstash-input-unix && \
    ./bin/plugin install logstash-output-websocket && \
    ./bin/plugin install logstash-output-syslog && \
    ./bin/plugin install logstash-output-stdout && \ 
    ./bin/plugin install logstash-output-redis && \
    ./bin/plugin install logstash-output-rabbitmq && \
    ./bin/plugin install logstash-output-neo4j && \
    ./bin/plugin install logstash-output-file && \
    ./bin/plugin install logstash-output-elasticsearch_http && \
    ./bin/plugin install logstash-input-lumberjack && \
    ./bin/plugin install logstash-input-websocket && \
    ./bin/plugin install logstash-input-twitter && \
    ./bin/plugin install logstash-input-stdin && \
    ./bin/plugin install logstash-input-rabbitmq && \
    ./bin/plugin install logstash-input-redis && \
    ./bin/plugin install logstash-input-neo4j && \
    ./bin/plugin install logstash-input-lumberjack && \
    ./bin/plugin install logstash-input-log4j && \
    ./bin/plugin install logstash-input-eventlog && \
    ./bin/plugin install logstash-filter-xml && \
    ./bin/plugin install logstash-filter-multiline && \
    ./bin/plugin install logstash-filter-json_encode && \
    ./bin/plugin install logstash-codec-multiline && \
    ./bin/plugin install logstash-codec-json_lines && \
    ./bin/plugin install logstash-codec-json && \
    ./bin/plugin install logstash-codec-es_bulk && \
    ./bin/plugin install logstash-output-mongodb

# Change working dir
WORKDIR /opt/logstash

# Run agent with basic config
CMD ["bin/logstash", "-e", "input { stdin { } } output { stdout { codec => rubydebug } }"]
