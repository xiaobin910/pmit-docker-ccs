FROM solr:5.5

MAINTAINER "Chen Lin <chenlin@pmit.cn>"

# 设置工作目录
WORKDIR /opt/solr

# 拷贝配置文件和jar包
COPY lib/* server/solr-webapp/webapp/WEB-INF/lib/
RUN mkdir -p server/solr/pmit
COPY pmit/* server/solr/pmit/


