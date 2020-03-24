# docker-flexget

Docker image for running [flexget](http://flexget.com/)

Container features are

- Lightweight alpine linux
- Python 3
- Flexget with initial settings (default ```config.yml``` and webui password)
- pre-installed plug-ins (transmissionrpc, python-telegram-bot)

No default password anymore, secure webui using ```FG_WEBUI_PASSWD``` below.

## Usage - docker

```
docker run -d \
    --name=<container name> \
    -p 3539:3539 \
    -v <path for data files>:/data \
    -v <path for config files>:/config \
    -e FG_WEBUI_PASSWD=<desired password> \
    -e FG_LOG_LEVEL=info \
    -e PUID=<UID for user> \
    -e PGID=<GID for user> \
    -e TZ=<timezone> \
    wiserain/flexget
```
## Usagen - docker-compose
```
version: "3.6"

services:

  flexget:
   image: vctrsnts/flexget
   container_name: flexget
   volumes:
    - ${STORAGE}/transmission/complete:/media/transmission
    - ${STORAGE}/amule/incoming:/media/amule
    - ${STORAGE}/config/flexget:/config
    - ${MEDIA}/series:/media/series
    - ${MEDIA}/movies:/media/movies
    - ${SEGURETAT}:/media/backup
   ports:
    - 5050:5050
   environment:
    - PUID=1001
    - PGID=1001
    - TORRENT_PLUGIN=YourTransmissionUser
    - FG_WEBUI_PASSWD=YourTransmissionPassword
    - TZ=Europe/Madrid
   restart: always
   links:
    - transmission
```
