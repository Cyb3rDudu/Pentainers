# Pentainers

A collection of Docker files for Containers i use for penetration testing.

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

## impacket

Impacket as a container on python:alpine base image. The repository includes latest impacket from github as submodule so submodules need to be pulled with this repository to build the container.

Build it with `docker build -t org/impacket .`

With the following alias and bashfunction it can be used:
```
alias impacket="docker run --rm -it org/impacket"
```
This alias allows usage bey e.g. executing `impacket wmiexec.py` or any other script from the examples of impacket.

If inbound traffic for impacket is needed e.g. for a smb server, ports need to be forwarded. In smb case `-p 445:445` and additionaly, a volume mount to keep files persistent is needed. 

This bash function mounts the current folder to the container at `/tmp/serve` and serves it via smb when `smbhere` is executed.
```
smbhere() {
    local sharename
    [[ -z $1 ]] && sharename="SHARE" || sharename=$1
    docker run --rm -it -p 445:445 -v "${PWD}:/tmp/serve" org/impacket smbserver.py -smb2support $sharename /tmp/serve
}
```
 
## Reqdump

A simple JavaScript server that echos any HTTP request it receives it to stdout. This is really useful when testing for SSRF or needing to see if a blind command injection is working with curl. The alias for it is:

```
alias reqdump='docker run --rm -it -p 80:3000 org/reqdump
```
This starts a local listener on 80 (although it’s entirely customizable). If it receives any HTTP request it prints it out

## Todo 
Add Containers 
- [] Default Linux Distos
- [] Metasploit
- []   Sliver C2 
