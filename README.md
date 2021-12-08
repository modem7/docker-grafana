[![GitHub last commit](https://img.shields.io/github/last-commit/modem7/docker-grafana)](https://github.com/modem7/docker-grafana)
[![Docker Pulls](https://img.shields.io/docker/pulls/modem7/docker-grafana)](https://hub.docker.com/r/modem7/docker-grafana) 
![Docker Image Size (tag)](https://img.shields.io/docker/image-size/modem7/docker-grafana/latest)
[![Build Status](https://drone.modem7.com/api/badges/modem7/docker-grafana/status.svg)](https://drone.modem7.com/modem7/docker-grafana)

# HomeCentr - grafana

Repack of [Grafana](https://grafana.com/) with the usual Homecentr bells and whistles.

## Usage

```yml
version: "3.7"
services:
  grafana:
    build: .
    image: homecentr/grafana
    ports:
      - 3000:3000
    volumes:
      - ./example:/config
```

## Environment variables

| Name | Default value | Description |
|------|---------------|-------------|
| PUID | 7077 | UID of the user grafana should be running as. |
| PGID | 7077 | GID of the user grafana should be running as. |
| 

## Exposed ports

| Port | Protocol | Description |
|------|------|-------------|
| 3000 | TCP | Web UI and API. |

## Volumes

| Container path | Description |
|------------|---------------|
| /config | Grafana configuration. This should container the `grafana.ini` configuration file. If you want to use [provisioning](https://grafana.com/docs/grafana/latest/administration/provisioning/), put the related files to `/config/provisioning`. |
| /grafana | Grafana state. Make sure the volume is writable for PUID/PGID. |
| /logs | Log files produced by Grafana if configured to. Make sure the volume is writable for PUID/PGID. |

## Security
The container is regularly scanned for vulnerabilities and updated. Further info can be found in the [Security tab](https://github.com/homecentr/docker-grafana/security).

### Container user
The container supports privilege drop. Even though the container starts as root, it will use the permissions only to perform the initial set up. The grafana process runs as UID/GID provided in the PUID and PGID environment variables.

:warning: Do not change the container user directly using the `user` Docker compose property or using the `--user` argument. This would break the privilege drop logic.
