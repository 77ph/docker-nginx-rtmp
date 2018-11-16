# docker-nginx-rtmp
A Dockerfile installing NGINX, nginx-rtmp-module and FFmpeg from source with
default config. Built on Alpine Linux.

* Nginx 1.14.1 (compiled from source)
* nginx-rtmp-module 1.2.1 (compiled from source)
* ffmpeg 4.1 (compiled from source)
* Default nginx config (See: [nginx.conf](nginx.conf))

[![Docker Stars](https://img.shields.io/docker/stars/77phnet/nginx-rtmp.svg)](https://hub.docker.com/r/77phnet/nginx-rtmp/)
[![Docker Pulls](https://img.shields.io/docker/pulls/77phnet/nginx-rtmp.svg)](https://hub.docker.com/r/77phnet/nginx-rtmp/)
[![Docker Automated build](https://img.shields.io/docker/automated/77phnet/nginx-rtmp.svg)](https://hub.docker.com/r/77phnet/nginx-rtmp/builds/)
[![Build Status](https://travis-ci.org/alfg/docker-nginx-rtmp.svg?branch=master)](https://travis-ci.org/77phnet/docker-nginx-rtmp)

## Usage

### Server
* Pull docker image and run:
```
sudo docker pull 77phnet/nginx-rtmp
sudo docker run -it -p 1935:1935 -p 8080:80 --rm 77phnet/nginx-rtmp
```
or 

* Build and run container from source:
```
sudo docker build -t nginx-rtmp .
sudo docker run -it -p 1935:1935 -p 8080:80 --rm nginx-rtmp
```

* Config nginx & run:
```
mkdir -p /opt/nginx
sudo docker pull 77phnet/nginx-rtmp
sudo docker run -d -p 1935:1935 -p 8080:80 --name tmp-nginx-container --rm 77phnet/nginx-rtmp
sudo docker cp tmp-nginx-container:/opt/nginx/nginx.conf /opt/nginx/nginx.conf
sudo docker rm -f tmp-nginx-container
```
Edit:
```
vi /opt/nginx/nginx.conf
```
Run nginx:
```
sudo docker run -d -p 1935:1935 -p 8080:80 -v /opt/nginx/nginx.conf:/opt/nginx/nginx.conf --rm nginx-rtmp
```

* Stream live content to:
```
rtmp://<server ip>:1935/$APP_NAME/$STREAM_NAME
```

###
FFmpeg Build
```
ffmpeg version 4.1 Copyright (c) 2000-2018 the FFmpeg developers
  built with gcc 6.4.0 (Alpine 6.4.0)
  configuration: --prefix=/usr/local --enable-version3 --enable-gpl --enable-nonfree --enable-small --enable-libmp3lame --enable-libx264 --enable-libx265 --enable-libvpx --enable-libtheora --enable-libvorbis --enable-libopus --enable-libfdk-aac --enable-libass --enable-libwebp --enable-librtmp --enable-postproc --enable-avresample --enable-libfreetype --enable-openssl --disable-debug --disable-doc --disable-ffplay --extra-libs='-lpthread -lm'
  libavutil      56. 22.100 / 56. 22.100
  libavcodec     58. 35.100 / 58. 35.100
  libavformat    58. 20.100 / 58. 20.100
  libavdevice    58.  5.100 / 58.  5.100
  libavfilter     7. 40.101 /  7. 40.101
  libavresample   4.  0.  0 /  4.  0.  0
  libswscale      5.  3.100 /  5.  3.100
  libswresample   3.  3.100 /  3.  3.100
  libpostproc    55.  3.100 / 55.  3.100

  configuration:
    --prefix=/usr/local
    --enable-version3
    --enable-gpl
    --enable-nonfree
    --enable-small
    --enable-libmp3lame
    --enable-libx264
    --enable-libx265
    --enable-libvpx
    --enable-libtheora
    --enable-libvorbis
    --enable-libopus
    --enable-libfdk-aac
    --enable-libass
    --enable-libwebp
    --enable-librtmp
    --enable-postproc
    --enable-avresample
    --enable-libfreetype
    --enable-openssl
    --disable-debug
    --disable-doc
    --disable-ffplay
    --extra-libs='-lpthread -lm'
```

## Resources
* https://alpinelinux.org/
* http://nginx.org
* https://github.com/arut/nginx-rtmp-module
* https://www.ffmpeg.org
* https://obsproject.com
