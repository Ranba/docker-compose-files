<<<<<<< HEAD
=======
# 源文件来自：https://raw.githubusercontent.com/mritd/dockerfile/master/caddy/Dockerfile
# 作者的Caddy教程：https://mritd.com/2021/01/07/lets-start-using-caddy2/

>>>>>>> 3036afc190b21a7498643c55822843c130e6bd45
FROM golang:1.18.0-alpine3.15 AS builder

RUN set -e \
    && apk upgrade \
    && apk add jq curl git \
    && export version=$(curl -s "https://api.github.com/repos/caddyserver/caddy/releases/latest" | jq -r .tag_name) \
    && echo ">>>>>>>>>>>>>>> ${version} ###############" \
    && go install github.com/caddyserver/xcaddy/cmd/xcaddy@latest \
    && xcaddy build ${version} --output /caddy \
        --with github.com/caddy-dns/cloudflare \
        --with github.com/caddy-dns/alidns \
        --with github.com/caddy-dns/dnspod \
        --with github.com/caddy-dns/gandi \
        --with github.com/abiosoft/caddy-exec \
        --with github.com/greenpau/caddy-trace \
        --with github.com/hairyhenderson/caddy-teapot-module \
        --with github.com/kirsch33/realip \
        --with github.com/porech/caddy-maxmind-geolocation \
        --with github.com/caddyserver/transform-encoder \
        --with github.com/caddyserver/replace-response \
        --with github.com/imgk/caddy-trojan
<<<<<<< HEAD
    
=======

>>>>>>> 3036afc190b21a7498643c55822843c130e6bd45

FROM alpine:3.15 AS dist

LABEL maintainer="mritd <mritd@linux.com>"

# See https://caddyserver.com/docs/conventions#file-locations for details
ENV XDG_CONFIG_HOME /config
ENV XDG_DATA_HOME /data

ENV TZ Asia/Shanghai

COPY --from=builder /caddy /usr/bin/caddy
ADD https://raw.githubusercontent.com/caddyserver/dist/master/config/Caddyfile /etc/caddy/Caddyfile
ADD https://raw.githubusercontent.com/caddyserver/dist/master/welcome/index.html /usr/share/caddy/index.html

# set up nsswitch.conf for Go's "netgo" implementation
# - https://github.com/golang/go/blob/go1.9.1/src/net/conf.go#L194-L275
# - docker run --rm debian:stretch grep '^hosts:' /etc/nsswitch.conf
RUN [ ! -e /etc/nsswitch.conf ] && echo 'hosts: files dns' > /etc/nsswitch.conf

RUN set -e \
    && apk upgrade \
    && apk add bash tzdata mailcap \
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo ${TZ} > /etc/timezone \
    && rm -rf /var/cache/apk/*

VOLUME /config
VOLUME /data

EXPOSE 80
EXPOSE 443
EXPOSE 2019

WORKDIR /srv

CMD ["caddy", "run", "--config", "/etc/caddy/Caddyfile", "--adapter", "caddyfile"]
