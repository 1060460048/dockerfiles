strongswan
==========

![](https://badge.imagelayers.io/vimagick/strongswan:latest.svg)

[strongSwan][1] is an Open Source IPsec-based VPN solution for Linux and other
UNIX based operating systems implementing both the IKEv1 and IKEv2 key exchange
protocols.

> :warning: This docker image only support IKEv2!

### docker-compose.yml

```yaml
strongswan:
  image: vimagick/strongswan
  ports:
    - 500:500/udp
    - 4500:4500/udp
  volumes:
    - /lib/modules:/lib/modules
    - /etc/localtime:/etc/localtime
  environment:
    - VPN_DOMAIN=vpn.easypi.info
    - VPN_DNS=8.8.8.8
    - VPN_SUBNET=10.20.30.0/24
    - VPN_P12_PASSWORD=secret
  cap_add:
    - NET_ADMIN
  privileged: yes
  restart: always
```

### up and running

```bash
docker-compose up -d
docker cp strongswan_strongswan_1:/etc/ipsec.d/client.mobileconfig .
docker-compose logs -f
```

> File `client.mobileconfig` can be imported into MacOSX as `VPN (IKEv2)`.

[1]: https://strongswan.org/
