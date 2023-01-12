# kasm-custom-images

My custom docker images built on top of default [Kasm Workspaces](https://kasmweb.com/docs/latest/index.html) images.

Refer to official
docs [building custom images](https://kasmweb.com/docs/latest/how_to/building_images.html?utm_campaign=Github&utm_source=github#building-custom-images).

## Contents

|     | Docker Image                          | Dockerhub Path |
|-----|---------------------------------------|----------------|
|     | serpro69/kasm-obsidian:1.12.0         |                |
|     | serpro69/kasm-citrix-workspace:1.12.0 |                |

Versions of images follow the release version of default kasm images. The version might also contain a build number which represents the version of the installed software package, e.g. `serpro69/kasm-obsidian:1.12.0+1.18.0` contains an installation of Obsidian 1.18.0.

## Build and Run

### Obsidian.md

==TODO==

### Citrix Workspace

```bash
docker build -f dockerfile-citrix-workspace -t <image-name> .
docker run --dns 8.8.8.8 --rm -it --shm-size=512m -p 6901:6901 -e VNC_PW=password -e VNCOPTIONS="-publicIP 127.0.0.1" <image-name>
```
