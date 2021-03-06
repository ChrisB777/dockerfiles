![Golang](https://blog.golang.org/gopher/gopher.png)

## ImageLayer
* latest [![](https://badge.imagelayers.io/xataz/golang:latest.svg)](https://imagelayers.io/?images=xataz/golang:latest 'Get your own badge on imagelayers.io')

## Tag available
* 1.6, latest [(Dockerfile)](https://github.com/xataz/dockerfiles/tree/master/golang/Dockerfile)

## Description
What is [Golang](https://golang.org/) ?

Go is an open source programming language that makes it easy to build simple, reliable, and efficient software. 

## Build Image

```shell
docker build -t xataz/golang github.com/xataz/dockerfiles.git#master:golang
```

## Configuration
### Environments
* UID : Choose uid for launch go (default : 991)
* GID : Choose gid for launch go (default : 991)

## Usage
### Build your project
```shell
docker run -it --rm \
    -v $(pwd):$(pwd) \
    -w $(pwd) \
    -e UID=$(id -u) \
    -e GID=$(id -g) \
    xataz/golang:1.6 build
```

