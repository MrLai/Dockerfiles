FROM ubuntu:16.04
LABEL MAINTAINER="ALai <flyingalai@gmail.com>"

COPY bootstrap.sh /usr/bin/

RUN export https_proxy=http://172.21.11.88:1080 \
        && export http_proxy=http://172.21.11.88:1080 \
        && apt-get update \
        && apt-get -y install wget \
        && cd /tmp \
        && wget --no-check-certificate https://linuxdot.net/down/jexus-5.8.3-x64.tar.gz \
        && tar -zxvf jexus-5.8.3-x64.tar.gz \
        && mv jexus /usr && /usr/jexus/jws regsvr && rm -rf /tmp/jexus* \
        && apt-get -y install apt-transport-https \
        && wget --no-check-certificate -q https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb \
        && dpkg -i packages-microsoft-prod.deb \
        && apt-get update \
        && apt-get -y install aspnetcore-runtime-2.1 \
        && apt-get -y autoremove wget \
        && chmod +x /usr/bin/bootstrap.sh

EXPOSE 80 443
VOLUME ["/usr/jexus/siteconf", "/var/www", "/usr/jexus/log"]
WORKDIR /usr/jexus
ENTRYPOINT ["/usr/bin/bootstrap.sh"]
# Healthy check
HEALTHCHECK --interval=30s --timeout=30s --start-period=30s --retries=3 \
  CMD curl -f http://127.0.0.1 || exit 1
#CMD /usr/jexus/jws start && tail -f