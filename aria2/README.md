`aria2` is a utility for downloading files.

## docker-compose.yml

```
aria2:
  image: vimagick/aria2
  ports:
    - "6800:6800"
  volumes:
    - "data:/var/lib/aria2"
    - "keys:/etc/aria2"
  environment:
    - TOKEN=e6c3778f-6361-4ed0-b126-f2cf8fca06db
  restart: always
```

> If you mount volume `/etc/aria2`,
> you need to generate `server-key.pem` and `server-cert.pem` via this command:
>> `openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout server-key.pem -out server-cert.pem`

## test

```
$ http --verify no https://localhost:6800/jsonrpc \
       id=$(uuidgen) \
       method=aria2.getGlobalStat \
       params:='["token:e6c3778f-6361-4ed0-b126-f2cf8fca06db"]'

{
    "id": "3c5323b8-79f7-49d4-8303-fcfe51488db5",
    "jsonrpc": "2.0",
    "result": {
        "downloadSpeed": "0",
        "numActive": "0",
        "numStopped": "0",
        "numStoppedTotal": "0",
        "numWaiting": "0",
        "uploadSpeed": "0"
    }
}
```
