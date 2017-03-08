[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/nextcloud-aarch64
[![](https://images.microbadger.com/badges/version/lsioarmhf/nextcloud-aarch64.svg)](https://microbadger.com/images/lsioarmhf/nextcloud-aarch64 "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/nextcloud-aarch64.svg)](http://microbadger.com/images/lsioarmhf/nextcloud-aarch64 "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/nextcloud-aarch64.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/nextcloud-aarch64.svg)][hub][![Build Status](http://jenkins.linuxserver.io:8080/buildStatus/icon?job=Dockers/LinuxServer.io-arm64/lsioarm64-nextcloud)](http://jenkins.linuxserver.io:8080/job/Dockers/job/LinuxServer.io-arm64/job/lsioarm64-nextcloud/)
[hub]: https://hub.docker.com/r/lsioarmhf/nextcloud-aarch64/

[Nextcloud][nextcloudurl] gives you access to all your files wherever you are.

Where are your photos and documents? With Nextcloud you pick a server of your choice, at home, in a data center or at a provider. And that is where your files will be. Nextcloud runs on that server, protecting your data and giving you access from your desktop or mobile devices. Through Nextcloud you also access, sync and share your existing data on that FTP drive at the office, a Dropbox or a NAS you have at home.

[![nextcloud](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/nextcloud-icon.png)][nextcloudurl]
[nextcloudurl]: https://nextcloud.com/

## Usage

```
docker create \
	--name nextcloud \
	-p 443:443 \
	-e PUID=<UID> -e PGID=<GID> \
	-v </path/to/appdata>:/config \
	-v <path/to/data>:/data \
	lsioarmhf/nextcloud-aarch64
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`


* `-p 443` - the port nextcloud web interface
* `-v /config` - nextcloud configs
* `-v /data` - your personal data
* `-e PGID` for for GroupID - see below for explanation
* `-e PUID` for for UserID - see below for explanation

It is based on Alpine Linux with s6 overlay, for shell access whilst the container is running do `docker exec -it nextcloud /bin/bash`

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" <sup>TM</sup>.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application
`IMPORTANT... THIS IS THE ARM64 VERSION`

Access the webui at `<your-ip>:443`, for more information check out [Nextcloud][nextcloudurl].  

Please note you will need a MySQL/MariaDB or other backend database to set this up.  Also please look [here](https://docs.nextcloud.com/server/11/admin_manual/installation/system_requirements.html#database-requirements-for-mysql-mariadb) for how to configure your database with regard to binlog format and installation.

## Info

* Monitor the logs of the container in realtime `docker logs -f nextcloud`.

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' nextcloud`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/nextcloud-aarch64`

## Versions

+ **07.03.17:** Initial Release