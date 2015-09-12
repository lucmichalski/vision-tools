FROM golang:1.5-wheezy
MAINTAINER Luc Michalski <michalski.luc@gmail.com>

# Build latest version from master
RUN git clone https://github.com/elasticsearch/logstash-forwarder.git /opt/logstash-forwarder
WORKDIR /opt/logstash-forwarder
RUN go build

# Run installer
COPY installer /installer
CMD ["/installer"]
