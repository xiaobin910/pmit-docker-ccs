FROM openresty/openresty:centos

MAINTAINER "Chen Lin <chenlin@pmit.cn>"

# 设置环境变量
ENV OPENRESTY_HOME /usr/local/openresty

# 设置时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# 拷贝配置文件
COPY conf/* $OPENRESTY_HOME/nginx/conf/