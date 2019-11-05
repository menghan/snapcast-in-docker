# snapcast-in-docker

This repo/image helps run snapcast (clients and servers) in docker, with airplay support.

The airplay target name is "MultiRoom".

## run client

```
$ # install avahi-daemon in host machine
$ sudo docker run -d --name snapclient \
	--restart=unless-stopped \
	--user _snapclient \
	--device=/dev/snd:/dev/snd \
	-v /var/run/avahi-daemon:/var/run/avahi-daemon \
	-v /var/run/dbus:/var/run/dbus \
	menghan/snapcast:snapclient
```

## run server

```
$ # install avahi-daemon in host machine
$ sudo docker run -d --name snapserver \
	--restart=unless-stopped \
	--user _snapserver \
	-p 1704:1704 -p 1705:1705 -p 1780:1780 -p 5000:5000 \
	-v /var/run/avahi-daemon:/var/run/avahi-daemon \
	-v /var/run/dbus:/var/run/dbus \
	menghan/snapcast:snapserver
```
