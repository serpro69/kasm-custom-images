[![Stand With Ukraine](https://raw.githubusercontent.com/vshymanskyy/StandWithUkraine/main/banner2-direct.svg)](https://stand-with-ukraine.pp.ua)

# kasm-custom-images

My custom docker images built on top of default [Kasm Workspaces](https://kasmweb.com/docs/latest/index.html) images.

Refer to official
docs [building custom images](https://kasmweb.com/docs/latest/how_to/building_images.html?utm_campaign=Github&utm_source=github#building-custom-images).

## Contents

|                                                   | Docker Image                                           | App Ver                | Dockerhub Path                                          |
|---------------------------------------------------|--------------------------------------------------------|------------------------|---------------------------------------------------------|
| ![](docs/assets/images/thumbnails/obsidianmd.png) | serpro69/kasm-obsidian:1.12.0-1.19.0-v1                | `obsidian_1.1.9_amd64` | https://hub.docker.com/r/serpro69/kasm-obsidian         |
|                                                   | serpro69/kasm-citrix-workspace:1.12.0-ica22.12.0.12-v1 |                        | https://hub.docker.com/r/serpro69/kasm-citrix-workspace |

Tags of images follow the following pattern: `<core kasm image version>:<app version>:<image version>`. For exmaple `serpro69/kasm-citrix-workspace:1.12.0-ica22.12.0.12-v1` is the first version of this image that contains an installation of Citrix Workspace 22.12.0.12 which runs on kasm 1.12.0.

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
