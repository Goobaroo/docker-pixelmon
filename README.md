# [The Pixelmon Modpack 9.1.13](https://www.curseforge.com/minecraft/modpacks/the-pixelmon-modpack) on Curseforge

<!-- toc -->

- [Description](#description)
- [Requirements](#requirements)
- [Options](#options)
  * [Adding Minecraft Operators](#adding-minecraft-operators)
- [Troubleshooting](#troubleshooting)
  * [Accept the EULA](#accept-the-eula)
  * [Permissions of Files](#permissions-of-files)
  * [Resetting](#resetting)
- [Source](#source)

<!-- tocstop -->

## Description

This container is built to run on an [Unraid](https://unraid.net) server, outside of that your milliage will vary.

The docker on first run will download the same version as tagged of `The Pixelmon Modpack 9.1.13` and install it.  This can take a while as the Forge installer can take a bit to complete.  You can watch the logs and it will eventually finish.

After the first run it will simply start the server.

Note: There are no modded minecraft files shipped in the container, they are all downloaded at runtime.

## Requirements

* /data mounted to a persistent disk
* Port 25565/tcp mapped
* environment variable EULA set to "true"

As the end user, you are repsonsible for accepting the EULA from Mojang to run their server, by default in the container it is set to false.

## Options

These environment variables can be set at run time to override their defaults.

* JVM_OPTS "-Xms2048m -Xmx4096m"
* MOTD "The Pixelmon Modpack 9.1.13 Server Powered by Docker"
* LEVEL world

### Adding Minecraft Operators

Set the enviroment variable `OPS` with a comma separated list of players.

example:
`OPS="OpPlayer1,OpPlayer2"`

## Troubleshooting
### Ubuntu Docker Run
```sh
git clone https://github.com/Goobaroo/docker-pixelmon.git
sudo chmod -R 777 ./docker-pixelmon
cd pixelmon

sudo docker run -d \
  --restart unless-stopped \
  --name 'minecraft-Pixelmon' \
  --hostname 'minecraft-Pixelmon' \
  -e 'EULA'='true' \
  -e 'JVM_OPTS'='-Xms2048m -Xmx4096m' \
  -e 'OPS'='' \
  -e 'MOTD'='Pixel Mon, Gotta PixelMon, DigiPoke.' \
  -p '25565:25565/tcp' \
  -v 'data/':'/data':'rw' \
  'goobaroo/pixelmon:latest'
```
### Docker Compose Build
```sh
git clone https://github.com/Goobaroo/docker-pixelmon.git ./pixelmon
sudo chmod -R 777 ./docker-pixelmon
cd docker-pixelmon
sudo docker-compose -f docker-compose-build.yml up
```
### Docker Compose Pull
```sh
git clone https://github.com/Goobaroo/docker-pixelmon.git ./pixelmon
sudo chmod -R 777 ./docker-pixelmon
cd docker-pixelmon
sudo docker-compose up
```


### Accept the EULA
Did you pass in the environment variable EULA set to `true`?

### Permissions of Files
This container is designed for [Unraid](https://unraid.net) so the user in the container runs on uid 99 and gid 100.  This may cause permission errors on the /data mount on other systems.

### Resetting
If the install is incomplete for some reason.  Deleting the downloaded server file in /data will restart the install/upgrade process.

## Source
Github: https://github.com/Goobaroo/docker-pixelmon

Docker: https://hub.docker.com/repository/docker/goobaroo/pixelmon
