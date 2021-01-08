# This container is a work in progress and it doesn't work at all right now.
I welcome any assistance with development, but please do not submit any requests for support until this notice is removed.  Thank you!

# docker-gridtracker-armhf
This is a GridTracker (https://gridtracker.org) container using the armhf architecture.
This container is based off of the work of HenningThiemann's chromium armhf container.

## Build
To build the application, you have to clone it first,
```
git clone
cd docker-gridtracker-armhf
docker build -t ben-kuhn/gridtracker-armhf .
```

## Run the container:
You need to enable xhost forwarding first:
```
xhost +local:docker
```
If the xhost command can not be found, make sure to install it first (on manjaro, the required package is 'xorg-xhost').

Although not strictly required, it is *HIGHLY* recommended to save gridtracker settings in a volume, to make it persistent through container restarts.
```
docker volume create gridtracker_home
``` 
After creating the volume, you can run the image using the following command:
```
docker pull ben-kuhn/docker-gridtracker-armhf

docker run --rm --privileged \
 -e DISPLAY=unix$DISPLAY \
 -v gridtracker_home:/home \
 -v /tmp/.X11-unix:/tmp/.X11-unix \
 -v /dev:/dev -v /run:/run \
 -v /etc/machine-id:/etc/machine-id \
 --ipc=host \
 --device /dev/dri \
 --group-add video \
 ben-kuhn/docker-gridtracker-armhf
```
Or simply use the script gridtracker-armhf:
```
sudo install -m 755 gridtracker-armhf /usr/local/bin
gridtracker-armhf
```

## Known Bugs
- Nothing Works since this container is a WIP