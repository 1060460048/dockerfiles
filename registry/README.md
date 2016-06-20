registry
========

[Registry][1] is the Docker toolset to pack, ship, store, and deliver content.

## docker-compose.yml

```yaml
registry:
  image: registry:2
  ports:
    - "5000:5000"
  volumes:
    - ./data:/var/lib/registry
    - ./certs:/certs
    - ./auth:/auth
  environment:
    - REGISTRY_HTTP_TLS_CERTIFICATE=/certs/registry.easypi.info.crt
    - REGISTRY_HTTP_TLS_KEY=/certs/registry.easypi.info.key
    - REGISTRY_AUTH=htpasswd
    - REGISTRY_AUTH_HTPASSWD_REALM=Registry Realm
    - REGISTRY_AUTH_HTPASSWD_PATH=/auth/htpasswd
  restart: always
```

## up and running

```bash
$ docker-compose up -d
$ docker-compose exec registry bash
>>> htpasswd -Bbn username password >> /auth/htpasswd
>>> exit

$ docker pull alpine
$ docker tag alpine registry.easypi.info:5000/alpine

$ docker login -u username -p password easypi.info:5000
$ docker push registry.easypi.info:5000/alpine
$ docker pull registry.easypi.info:5000/alpine
```

## read more

- https://github.com/docker/distribution/blob/master/docs/deploying.md
- https://github.com/docker/distribution/blob/master/docs/insecure.md
- https://serversforhackers.com/tcp-load-balancing-with-nginx-ssl-pass-thru

[1]: https://github.com/docker/distribution
