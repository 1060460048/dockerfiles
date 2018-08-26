snort
=====

![](https://badge.imagelayers.io/vimagick/snort:latest.svg)

[`Snort`][1] is an open source intrusion prevention system capable of real-time
traffic analysis and packet logging.

```yaml
snort:
  image: vimagick/snort
  command: -q -c /etc/snort/snort.conf -A console -i ens3
  volumes:
    - ./data/snort.conf:/etc/snort/snort.conf
    - ./data/rules:/etc/snort/rules
    - ./data/log:/var/log/snort
  cap_add:
    - NET_ADMIN
  net: host
  tty: true
  restart: unless-stopped
```

```bash
# /etc/snort/rules/local.rules
alert icmp any any -> any any (msg:"ICMP Echo Request"; itype:8; sid:10000;)
alert icmp any any -> any any (msg:"ICMP Echo Reply"; itype:0; sid:10001;)
```

```bash
$ docker-compose up -d
$ docker-compose logs --tail 10 -f
snort_1  | 08/26-06:47:35.460754  [**] [1:10000:0] ICMP Echo Request [**] [Priority: 0] {ICMP} x.x.x.x -> y.y.y.y
snort_1  | 08/26-06:47:35.460835  [**] [1:10001:0] ICMP Echo Reply [**] [Priority: 0] {ICMP} y.y.y.y -> x.x.x.x
```

[1]: https://snort.org/
