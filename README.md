# homeinfra
To create a pi-hole with cloudflared docker containers for more secure home network

Pi-hole Installation 

- Setup Raspberry Pi 
- Enable SSH
- Install Docker 
- Pull this repository into /opt/dns 
- Build Docker and run with `docker-compose -f docker-compose.yml up -d`  


## There is known issue with `apk update` command in Alpine 3.14
The work around is upgrade libseccomp2 to a supported version from the Debian Repos 
```
wget http://ftp.de.debian.org/debian/pool/main/libs/libseccomp/libseccomp2_2.5.1-1_armhf.deb
dpkg -i libseccomp2_2.5.1-1_armhf.deb
```
Ref https://github.com/docker/for-linux/issues/1196#issuecomment-816600988
