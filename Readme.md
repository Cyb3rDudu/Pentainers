# Pentainers

A collection of Docker files for Containers i use for penetration testing

## nginxserve

Nginx as http(s) server to serve payloads and more. Generates a selfsigned certificate with openssl at startup and provides tls for better opsec.

Based on offcial [nginx docker image](https://hub.docker.com/_/nginx)

Build it with `docker build -t org/nginxserve .`

To run, i use a alias that i added to my shell
```
alias nginxhere='docker run --rm -it -p 80:80 -p 443:443 -v "${PWD}:/srv/data" org/nginxserve'
```

## webdav

Webdav through wsgidav served as a docker container. The server serves anonymously on port 80 from `/srv/data`. Uses alpine:python as base image.

Build it with `docker build -t org/nginxswebdav .`

To run, i use the alias:
```
alias webdavhere='docker run --rm -it -p 80:80 -v "${PWD}:/srv/data/share" org/webdav'
```

From Windows, I can browse to the WebDav share by a UNC path: `\\192.168.X.X@80\share`
