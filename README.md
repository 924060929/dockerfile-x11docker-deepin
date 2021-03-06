# x11docker/deepin

Run [deepin desktop](https://www.deepin.org) in a Docker container. 
Use [x11docker](https://github.com/mviereck/x11docker) to run image. 

Run desktop with:
```
x11docker --desktop --init=systemd -- --cap-add=IPC_LOCK --security-opt seccomp=unconfined -- x11docker/deepin
```

Run single application:
```
x11docker x11docker/deepin deepin-terminal
```

# Options:
 - Persistent home folder stored on host with   `--home`
 - Shared host file or folder with              `--share PATH`
 - Hardware acceleration with option            `--gpu`
 - Clipboard sharing with option                `--clipboard`
 - Language locale setting with                 `--lang [=$LANG]`
 - Sound support with                           `--pulseaudio`
 - Printer support with                         `--printer`
 - Webcam support with                          `--webcam`

See `x11docker --help` for further options.

# Extend base image
To add your desired applications, create your own Dockerfile with this image as a base. Example:
```
FROM x11docker/deepin
RUN apt-get update
RUN env DEBIAN_FRONTEND=noninteractive apt-get install -y firefox
```
Example to add `wine` and `wechat`:
```
FROM x11docker/deepin
RUN env DEBIAN_FRONTEND=noninteractive dpkg --add-architecture i386 && apt-get update
RUN env DEBIAN_FRONTEND=noninteractive apt-get install -y \
    deepin-wine deepin-wine32 deepin-wine32-preloader deepin-wine-helper deepin-wine-uninstaller
RUN env DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    deepin.com.wechat
```
 
# Screenshot

![screenshot](https://raw.githubusercontent.com/mviereck/x11docker/screenshots/screenshot-deepin.png "deepin desktop running in weston Xwayland window using x11docker")
