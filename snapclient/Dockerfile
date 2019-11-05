FROM debian:10

ENV SNAPCAST_VERSION 0.16.0

RUN apt-get update && \
	apt-get install -y wget && \
	test `uname -m` = "armv7l" && wget -O snapclient.deb https://github.com/badaix/snapcast/releases/download/v$SNAPCAST_VERSION/snapclient_${SNAPCAST_VERSION}_armhf.deb || wget -O snapclient.deb https://github.com/badaix/snapcast/releases/download/v$SNAPCAST_VERSION/snapclient_${SNAPCAST_VERSION}_amd64.deb && \
	(dpkg -i snapclient.deb; apt-get install -f -y) && \
	rm -rf /var/lib/apt/lists/* snapclient.deb

ENTRYPOINT ["snapclient"]
