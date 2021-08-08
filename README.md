# Home infra
To create a pi-hole with cloudflared docker containers for more secure home network

## Pi-hole Installation 

- Setup Raspberry Pi 
- Enable SSH
- Install Docker 
- Pull this repository into /opt/dns 
- Build Docker and run with `docker-compose -f docker-compose.yml up -d`  

# Known issues

## There is known issue with `apk update` command in Alpine 3.14 on Raspberry Pi
![image](https://user-images.githubusercontent.com/6348112/128638100-916723fc-1af9-4852-910f-76d2a78b4e50.png)

```
+ apk update
fetch https://dl-cdn.alpinelinux.org/alpine/v3.14/main/armv7/APKINDEX.tar.gz
ERROR: https://dl-cdn.alpinelinux.org/alpine/v3.14/main: temporary error (try again later)
WARNING: Ignoring https://dl-cdn.alpinelinux.org/alpine/v3.14/main: No such file or directory
fetch https://dl-cdn.alpinelinux.org/alpine/v3.14/community/armv7/APKINDEX.tar.gz
ERROR: https://dl-cdn.alpinelinux.org/alpine/v3.14/community: temporary error (try again later)
WARNING: Ignoring https://dl-cdn.alpinelinux.org/alpine/v3.14/community: No such file or directory
2 errors; 14 distinct packages available
```

The work around is upgrade libseccomp2 to a supported version from the Debian Repos 
```
wget http://ftp.de.debian.org/debian/pool/main/libs/libseccomp/libseccomp2_2.5.1-1_armhf.deb
dpkg -i libseccomp2_2.5.1-1_armhf.deb
```
Ref https://github.com/docker/for-linux/issues/1196#issuecomment-816600988

## Pi-hole admin password will appear only once (in container) after install. 
To reset password 
- Open bash in pi-hole container 
`docker exec -it dns_pihole_1 /bin/bash`
- Run command to set new password
`sudo pihole -a -p`
