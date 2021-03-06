## wonderfall/deluge
[![](https://badge.imagelayers.io/wonderfall/deluge:latest.svg)](https://imagelayers.io/?images=wonderfall/deluge:latest 'Get your own badge on imagelayers.io') *vanilla*

[![](https://badge.imagelayers.io/wonderfall/deluge:filebot.svg)](https://imagelayers.io/?images=wonderfall/deluge:filebot 'Get your own badge on imagelayers.io') *filebot*

![](https://i.goopics.net/pS.png)

#### What is this?
Deluge is a blazing fast and open-source BitTorrent client. It has an embedded WebUI. More info on the [official website](http://deluge-torrent.org/). Filebot is a tool for renaming movies, series, and it creates hardlinks in `/data/media`.

#### Tags
- Vanilla : `latest`, `1.3`
- With Filebot : `filebot`, `1.3-filebot`

#### Environment variables
- **WEBROOT** : explicit.
- **UID** : cowrie user id.
- **GID** : cowrie group id.
- **FB_LINK** *(filebot)* : symlink or hardlink.

#### Volumes
- **/data** : torrents, downloads.
- **/config** : configuration files.

#### Examples
```
# docker-compose.yml
deluge:
  image: wonderfall/deluge
  volumes:
    - /mnt/seedbox:/data
    - /mnt/deluge:/config
  environment:
    - WEBROOT=/
    - UID=1000
    - GID=1000
```
```
# reverse proxy with nginx
# https://github.com/Wonderfall/dockerfiles/tree/master/reverse
# X-Deluge-Base must be set if you're using a custom webroot
location WEBROOT {
        proxy_pass              http://deluge:8112/;
        proxy_set_header        X-Deluge-Base "WEBROOT/";
        ...
}
```
