FROM golang:latest

MAINTAINER jybtx <admin@jybtx.com>

RUN set -x && apt-get update -y && apt-get upgrade -y && apt-get install -y vim


# 设置工作目录
WORKDIR /go/src

# 设置时区为上海
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' >/etc/timezone

# 设置编码
ENV LANG C.UTF-8

# 编译时的环境变量
ENV CGO_ENABLED=0 GOOS=linux GOARCH=amd64 GO111MODULE=on

# 依赖下载
ENV GOPROXY=https://goproxy.cn,direct

ENV GOPATH=/go:/go/src


#将Dockerfile 中的文件存储到/app下
COPY main.go .



CMD ["go", "run", "main.go"]
