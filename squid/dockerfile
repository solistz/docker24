FROM ubuntu:latest

ENV SQUID_CACHE_DIR=/var/spool/squid \
    SQUID_LOG_DIR=/var/log/squid \
    SQUID_CONFIG_DIR=/etc/squid \
    SQUID_USER=proxy \
    TZ=Europe/Kiev

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y squid \
  && rm -rf /var/lib/apt/lists/*

COPY squid.conf ${SQUID_CONFIG_DIR}
COPY entrypoint.sh /sbin/entrypoint.sh

VOLUME ["SQUID_CACHE_DIR","SQUID_LOG_DIR","SQUID_CONFIG_DIR"]

RUN chmod 755 /sbin/entrypoint.sh

EXPOSE 3128/tcp
ENTRYPOINT ["/sbin/entrypoint.sh"]
