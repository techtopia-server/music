FROM alpine
RUN apk update \
    && apk upgrade \
    && apk add --no-cache snapcast-server avahi

RUN apk add --no-cache \
    alsa-lib-dev \
    autoconf \
    automake \
    avahi-dev \
    build-base \
    curl \
    dbus \
    libconfig-dev \
    libdaemon-dev \
    openssl-dev \
    libtool \
    popt-dev \
    soxr-dev

ARG SHAIRPORT_VERSION=2.8.6

RUN curl -Lo /tmp/$SHAIRPORT_VERSION.tar.gz https://github.com/mikebrady/shairport-sync/archive/$SHAIRPORT_VERSION.tar.gz \
    && tar -xzf /tmp/$SHAIRPORT_VERSION.tar.gz -C /tmp \
    && rm /tmp/$SHAIRPORT_VERSION.tar.gz \
    && cd /tmp/shairport-sync-$SHAIRPORT_VERSION \
    && autoreconf -i -f  \
    && ./configure \
      --with-avahi \
      --with-ssl=openssl \
      --with-stdout \
      --with-metadata \
    && make \
    && make install \
    && rm -R -f /tmp/shairport-sync-$SHAIRPORT_VERSION

#RUN apk del \ 
#    alsa-lib-dev \
#    autoconf \
#    automake \
#    avahi-dev \
#    build-base \
#    libconfig-dev \
#    libdaemon-dev \
#    openssl-dev \
#    popt-dev \
#    soxr-dev

RUN sed -i 's/#enable-dbus=yes/enable-dbus=no/g' /etc/avahi/avahi-daemon.conf && \
    rm -rf /var/cache/apk/*


WORKDIR /app
COPY ./start.sh .

ENTRYPOINT ["./start.sh"]
