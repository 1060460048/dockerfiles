shadowsocks
===========

[![](https://badge.imagelayers.io/vimagick/shadowsocks:latest.svg)](https://imagelayers.io/?images=vimagick/shadowsocks:latest 'Get your own badge on imagelayers.io')

[`shadowsocks`][1] is a secure socks5 proxy,
designed to protect your Internet traffic.

> If you want to keep a secret,
> you must also hide it from yourself.

## docker-compose.yml

```
shadowsocks:
  image: vimagick/shadowsocks
  ports:
    - "8388:8388"
  environment:
    - PASSWORD=secret
  restart: always
```

## server

```
$ docker-compose up -d
```

## client

```
$ sslocal -c config.json
```

[read more][2]

[1]: http://shadowsocks.org
[2]: https://github.com/shadowsocks/shadowsocks/wiki/Configuration-via-Config-File
