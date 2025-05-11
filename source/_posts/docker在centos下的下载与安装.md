---
title: docker在centos下的下载与安装
date: 2025-05-10 22:35:59
tags: [Docker, Linux]
---

## Docker下载与安装

```bash
# 安装依赖
yum install -y yum-utils device-mapper-persistent-data lvm2
# 添加软件源信息
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
# 更新并安装docker-ce 
yum makecache fast

yum list docker-ce --showduplicates|sort -r

# 默认安装最新版本
yum -y install docker-ce
# 配置docker镜像源和cgroup
mkdir /etc/docker/
touch /etc/docker/daemon.json

cat > /etc/docker/daemon.json << EOF
{
	"exec-opts": ["native.cgroupdriver=systemd"],
	"registry-mirrors": ["https://hub-mirror.c.163.com"]
}
EOF

systemctl enable docker --now

docker system prune
```

## docker应用

- 从仓库拉取镜像：`docker pull`
- 查看系统中的镜像：`docker images`
- 基于镜像运行容器：`docker run`
- 查看构建的容器：`docker ps`



## 简单运行一个redis

```bash
docker run -p 16379:6379 --name=redis -d redis.alpine3.18
```



## 构建go环境的容器

```bash
docker pull alpine:3.18.4
```

```bash
docker run -p 8080:80 --name=go -d apline:3.18.4 ping imooc.com

docker ps

docker exec -it go sh

mkdir /go
cd /go

# 停止并删除
docker stop go | xargs docker rm
```

```bash
cd /go

wget --no-check-certificate https://golang.google.cn/dl/go1.24.0.linux-amd63.tar.gz

tar -C /user/local -zxf go1.24.0.linux-amd64.tar.gz

rm -rf /go/go1.24.0.linux-amd64.tar.gz

# 注意：因为apline系统对go程序运行的时候默认查找的类库与提供的类库不一致，需要调整
mkdir /lib64
ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2

# 配置go的系统环境
export GOPATH=/go
export PATH=/usr/local/go/bin:$GOPATH/bin:$PATH

# 验证
go version
```

