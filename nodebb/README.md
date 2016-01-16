nodebb
======

![](https://badge.imagelayers.io/vimagick/nodebb:latest.svg)

[NodeBB][1] Forum Software is powered by Node.js and built on either a Redis or MongoDB database.

## docker-compose.yml

```
nodebb:
  image: vimagick/nodebb
  ports:
    - "4567:4567"
  links:
    - redis
  restart: always

redis:
  image: redis
  ports:
    - "127.0.0.1:6379:6379"
  restart: always
```

## up and running

```
$ docker-compose up -d
$ firefox http://localhost:4567
```

## todo

- Next release: install
  - alpine: krb5-libs krb5-dev
  - debian: libkrb5-3 libkrb5-dev

[1]: https://nodebb.org/
