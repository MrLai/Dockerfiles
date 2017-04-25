FROM alpine:latest

MAINTAINER ALai <flyingalai@gmail.com>

RUN apk update && apk add tinyproxy && rm -rf /car/cache/apk

ADD ./tinyproxy.conf /etc/tinyproxy/tinyproxy.conf

EXPOSE 8888

VOLUME ["/etc/tinyproxy", "/var/log/tinyproxy"]

CMD ["/usr/sbin/tinyproxy", "-d"]