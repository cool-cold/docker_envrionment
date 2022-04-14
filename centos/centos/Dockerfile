FROM centos:centos7

ARG WORKSPACE=/root/workspace
ARG GOVERSION=1.18

# 创建工作目录
RUN mkdir $WORKSPACE

# 设置环境变量
ENV GOROOT=/usr/local/go
ENV GOBIN=$GOROOT/bin
ENV PATH=$PATH:$GOBIN
ENV GO111MODULE=on
ENV GOPROXY=https://goproxy.cn,direct

ENV LANG="en_US.UTF-8"
ENV PS1="[\u@dev \W]\$ "
ENV WORKSPACE=$WORKSPACE
ENV PATH="$PATH/bin:$PATH"

# 更新镜像源
RUN sed -e 's|^mirrorlist=|#mirrorlist=|g' \
    -e 's|^#baseurl=http://mirror.centos.org/centos|baseurl=https://mirrors.ustc.edu.cn/centos|g' \
    -i.bak \
    /etc/yum.repos.d/CentOS-Base.repo && \
    yum makecache && \
    yum update -y 

# 安装必备的软件
RUN yum install -y git vim gdb wget zsh gcc

# git加速
RUN git config --global url."https://github.com.cnpmjs.org/".insteadOf "https://github.com/"

# 安装go
RUN cd /usr/local && \
    wget https://dl.google.com/go/go${GOVERSION}.linux-amd64.tar.gz && \
    tar -zxvf go${GOVERSION}.linux-amd64.tar.gz && \
    rm -rf go${GOVERSION}.linux-amd64.tar.gz
