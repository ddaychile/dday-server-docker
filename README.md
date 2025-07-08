# Servidores de Dday en Docker

Este repositorio muestra como usar la imagen de Docker creada por Kernel, aqui se puede ver un compose.yaml sencillo para un server, en esta misma repo se adjunta un compose.yaml para mas de un server compartiendo la estructura de carpetas.

Imagen: https://hub.docker.com/r/pcarmona/ddaychile-release

Q2 D-Day: Normandy 5.x
This is a modification of D-Day: Normandy by Vipersoft and the SHAEF team, used in servers of the D-Day: Normandy Chile community.

This image is based on the Q2PRO dedicated server with Q2Admin-kmod library. The source is downloaded and compiled from the site https://github.com/ddaychile/release-dll⁠ and its available for Linux x86_64 and aarch64 (amd64).

How to use this image
The maps to be used by the server must be put in maps/ sub-directory and the config files in the files/ sub-directory.

- compose.yaml
```
- dday5-server/
  |- files/
  |  |-- maps.lst
  |  |-- server.cfg
  |  |-- q2admin.txt
  |  |-- q2adminban.txt
  |  ...
  |- maps/
     |- dday1.bsp
     |- dday2.bsp
     ...
```

The compose.yaml file should be like this

```
services:

  dday5-server:
    image: pcarmona/ddaychile-release:latest
    restart: always
    volumes:
      - ./dday5-server/maps:/usr/local/share/q2pro/dday/maps
      - ./dday5-server/files:/home/ubuntu/.q2pro/dday
    stdin_open: true
    tty: true
    network_mode: host
    logging:
      driver: "json-file"
      options:
        max-size: "10M"
        max-file: 100
```
Finally run using Docker Compose:
```
docker compose up -d dday5-server
```
