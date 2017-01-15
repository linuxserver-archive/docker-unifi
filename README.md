[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# linuxserver/unifi
[![](https://images.microbadger.com/badges/version/linuxserver/unifi.svg)](https://microbadger.com/images/linuxserver/unifi "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/linuxserver/unifi.svg)](http://microbadger.com/images/linuxserver/unifi "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/linuxserver/unifi.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/linuxserver/unifi.svg)][hub][![Build Status](http://jenkins.linuxserver.io:8080/buildStatus/icon?job=Dockers/LinuxServer.io/linuxserver-unifi)](http://jenkins.linuxserver.io:8080/job/Dockers/job/LinuxServer.io/job/linuxserver-unifi/)
[hub]: https://hub.docker.com/r/linuxserver/unifi/

The UniFi® Controller software is a powerful, enterprise wireless software engine ideal for high-density client deployments requiring low latency and high uptime performance. [Unifi](https://www.ubnt.com/enterprise/#unifi)

[![unifi](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/unifi_svg.svg)][unifiurl]
[unifiurl]: https://www.ubnt.com/enterprise/#unifi

## Usage

```
docker create \
  --name=unifi \
  -v <path to data>:/config \
  -e PGID=<gid> -e PUID=<uid>  \
  -p 8080:8080 \
  -p 8081:8081 \
  -p 8443:8443 \
  -p 8843:8843 \
  -p 8880:8880 \
  linuxserver/unifi
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side.
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`


* `-p 8080` - port(s) required for Unifi to function
* `-p 8081` - port(s)
* `-p 8443` - port(s)
* `-p 8843` - port(s)
* `-p 8880` - port(s)
* `-v /config` - where unifi stores it config files etc, needs 3gb free
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation

It is based on xenial with s6 overlay, for shell access whilst the container is running do `docker exec -it unifi /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" <sup>TM</sup>.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id dockeruser
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application

The webui is at https://ip:8443 , setup with the first run wizard.


## Info

* Shell access whilst the container is running: `docker exec -it unifi /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f unifi`


* container version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' unifi`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' linuxserver/unifi`


## Versions

+ **15.01.17:** Update UniFi logo in README.
+ **14.10.16:** Add version layer information.
+ **20.09.16** Bump to pick up ver 5.27.
+ **10.09.16** Add layer badges to README.
+ **28.08.16** Add badges to README.
+ **01.07.16** Switch to lsiobase/xenial for conformity.
+ **25.06.16** Rebase to xenial and use updated repository.
+ **02.11.15** Initial Release.
