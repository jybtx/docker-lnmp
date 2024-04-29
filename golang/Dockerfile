FROM golang:latest

MAINTAINER jybtx <admin@jybtx.com>

RUN set -x && apt-get update -y && apt-get upgrade -y && apt-get install -y vim


# 创建文件夹
RUN mkdir /app

# 设置工作目录
WORKDIR /app

#将Dockerfile 中的文件存储到/app下
COPY main.go .

# 因为已经是在 /app下了，所以使用  ./
# RUN go build -o main ./main.go

#设置容器的启动命令，CMD是设置容器的启动指令
# CMD /app/main

CMD ["go", "run", "main.go"]
