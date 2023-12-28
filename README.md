[![Stand With Ukraine](https://raw.githubusercontent.com/vshymanskyy/StandWithUkraine/main/banner2-direct.svg)](https://stand-with-ukraine.pp.ua)

# kasm-custom-images

My custom docker images built on top of default [Kasm Workspaces](https://kasmweb.com/docs/latest/index.html) images.

Refer to official
docs [building custom images](https://kasmweb.com/docs/latest/how_to/building_images.html?utm_campaign=Github&utm_source=github#building-custom-images).

## Contents

| Docker Image                                                                                                              | App Ver                      | Dockerhub Path                                             |
|---------------------------------------------------------------------------------------------------------------------------|------------------------------|------------------------------------------------------------|
| <img src="docs/assets/images/thumbnails/obsidian.svg" height=36/> `serpro69/kasm-obsidian:1.19.0-v1-1.12.0`               | `obsidian_1.1.9_amd64`       | https://hub.docker.com/r/serpro69/kasm-obsidian            |
| <img src="docs/assets/images/thumbnails/citrix.svg" height=36/> `serpro69/kasm-citrix-workspace:ica22.12.0.12-v1-1.12.0`  | `icaclient_22.12.0.12_amd64` | https://hub.docker.com/r/serpro69/kasm-citrix-workspace    |
| <img src="docs/assets/images/thumbnails/cisco.svg" height=36/> `serpro69/kasm-cisco-packet-tracer:8.2.1-v1-1.12.0`        | `Packet_Tracer821_amd64`     | https://hub.docker.com/r/serpro69/kasm-cisco-packet-tracer |
| <img src="docs/assets/images/thumbnails/cisco.svg" height=36/> `serpro69/kasm-cisco-packet-tracer-single:8.2.1-v1-1.12.0` | `Packet_Tracer821_amd64`     | https://hub.docker.com/r/serpro69/kasm-cisco-packet-tracer |

Tags of images follow the following pattern: `<app_version>-v<image_version>-<casm_core_version>`. For exmaple `serpro69/kasm-citrix-workspace:ica22.12.0.12-v1-1.12.0` is the first version of this image that contains an installation of Citrix Workspace 22.12.0.12 which runs on kasm 1.12.0.

## Build and Run

### Obsidian.md

```
docker build -f dockerfile-citrix-workspace -t <image-name> .
docker run --dns 8.8.8.8 --rm -it --shm-size=512m -p 6901:6901 -e VNC_PW=password -e VNCOPTIONS="-publicIP 127.0.0.1" -v $HOME/obsidian:/home/kasm-user/obsidian:rw <image-name>
```

### Citrix Workspace

```bash
docker build -f dockerfile-citrix-workspace -t <image-name> .
docker run --dns 8.8.8.8 --rm -it --shm-size=512m -p 6901:6901 -e VNC_PW=password -e VNCOPTIONS="-publicIP 127.0.0.1" <image-name>
```

### Cisco Packet Tracer

```bash
docker build -f dockerfile-cisco-packet-tracer -t <image-name> .
docker run --dns 8.8.8.8 --rm -it --shm-size=512m -p 6901:6901 -e VNC_PW=password -e VNCOPTIONS="-publicIP 127.0.0.1" -v $HOME/pt:/home/kasm-user/pt:rw <image-name>
```

#### Single Application Version

This image provides a single-application image, meaning you will have the application window directly in the browser tab, instead of a full-fledged ubuntu desktop environment.

The usage is the same, you just need to use the correct dockerfile

```bash
docker build -f dockerfile-cisco-packet-tracer-single -t <image-name> .
docker run --dns 8.8.8.8 --rm -it --shm-size=512m -p 6901:6901 -e VNC_PW=password -e VNCOPTIONS="-publicIP 127.0.0.1" -v $HOME/pt:/home/kasm-user/pt:rw <image-name>
```

NB! If this is the first time you're launching the packet-tracer app - it will require you to login on launch and will try to open a browser to do so, which will then fail and return an error. So on first launch you still need to use the "full" packet-tracer image, login and persist settings on the client (the `-v $HOME/pt:/home/kasm-user/pt:rw` part), after which the "single" version can be used.
