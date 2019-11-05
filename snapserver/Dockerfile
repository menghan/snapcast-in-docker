FROM debian:10

ENV SHAIRPORT_SYNC_VERSION 3.3.4
ENV SNAPCAST_VERSION 0.16.0

ADD snapserver.conf /etc/snapserver.conf

RUN apt-get update && \
	apt-get install -y wget build-essential git xmltoman autoconf automake libtool libdaemon-dev libpopt-dev libconfig-dev libasound2-dev avahi-daemon libavahi-client-dev libssl-dev && \
	cd /tmp && \
	wget -O - https://github.com/mikebrady/shairport-sync/archive/${SHAIRPORT_SYNC_VERSION}.tar.gz | tar -xz -f - && \
	cd shairport-sync-$SHAIRPORT_SYNC_VERSION && \
	autoreconf -i -f && \
	./configure --with-stdout --with-avahi --with-ssl=openssl --with-metadata --sysconfdir=/etc --with-alsa && \
	make -j 4 && make install && \
	test `uname -m` = "armv7l" && wget -O snapserver.deb https://github.com/badaix/snapcast/releases/download/v$SNAPCAST_VERSION/snapserver_${SNAPCAST_VERSION}_armhf.deb || wget -O snapserver.deb https://github.com/badaix/snapcast/releases/download/v$SNAPCAST_VERSION/snapserver_${SNAPCAST_VERSION}_amd64.deb && \
	(dpkg -i snapserver.deb; apt-get install -f -y) && \
	rm -rf /var/lib/apt/lists/* snapserver.deb /tmp/shairport-sync-$SHAIRPORT_SYNC_VERSION

ENTRYPOINT ["snapserver"]
