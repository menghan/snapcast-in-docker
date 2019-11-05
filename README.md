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
	--network host \
	-v /var/run/avahi-daemon:/var/run/avahi-daemon \
	-v /var/run/dbus:/var/run/dbus \
	menghan/snapcast:snapserver
```
