![lufi](https://git.framasoft.org/uploads/project/avatar/1998/lufi.png =250x)

## ImageLayer
* latest [![](https://badge.imagelayers.io/xataz/lufi:latest.svg)](https://imagelayers.io/?images=xataz/lufi:latest 'Get your own badge on imagelayers.io')

## Tag available
* latest [(lufi/Dockerfile)](https://github.com/xataz/dockerfiles/blob/master/lufi/Dockerfile)

## Description
What is [lufi](https://git.framasoft.org/luc/lufi) ?

Lufi means Let's Upload that FIle.

It stores files and allows you to download them.

Is that all? No. All the files are encrypted by the browser! It means that your files never leave your computer unencrypted. The administrator of the Lufi instance you use will not be able to see what is in your file, neither will your network administrator, or your ISP.

## BUILD IMAGE

```shell
docker build -t xataz/lufi github.com/xataz/dockerfiles.git#master:lufi
```

## Configuration
### Environments
* UID : Choose uid for launch lufi (default : 991)
* GID : Choose gid for launch lufi (default : 991)
* WEBROOT : webroot of lufi (default : /)
* SECRET : random string used to encrypt cookies (default : 0423bab3aea2d87d5eedd9a4e8173618)
* MAX_FILE_SIZE : maximum file size of an uploaded file in bytes (default : 10000000000)
* CONTACT : lufi contact (default : contact@domain.tld)

Tip : you can use the following command to generate SECRET. `date +%s | md5sum | head -c 32`

### Volumes
* /data : lufi's database is here
* /files : Location of uploaded files

### Ports
* 8080

## Usage
### Simple launch
```shell
docker run -d -p 8080:8080 xataz/lufi
```
URI access : http://XX.XX.XX.XX:8080

### Advanced launch
```shell
docker run -d -p 8181:8080 \
	-v /docker/config/lufi/data:/data \
    -v /docker/data/lufi:/files \
	-e UID=1001 \
	-e GID=1001 \
    -e WEBROOT=/lufi \
    -e SECRET=$(date +%s | md5sum | head -c 32) \
    -e CONTACT=contact@mydomain.com \
    -e MAX_FILE_SIZE=250000000 \
	xataz/lufi
```
URI access : http://XX.XX.XX.XX:8181/lufi
