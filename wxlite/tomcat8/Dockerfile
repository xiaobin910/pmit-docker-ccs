FROM tomcat:latest

MAINTAINER "Chen Lin <chenlin@pmit.cn>"

# 初始环境变量
ENV CATALINA_HOME /usr/local/tomcat
ENV JAVA_HOME /docker-java-home

# 定义war包下载及存储路径
# ENV WAR_URI http://t.wxwap.pmit.cn:9999/common.zip
ENV WAR_URI http://t.wxwap.pmit.cn:9999/basic.zip
# ENV WAR_URI http://t.wxwap.pmit.cn:9999/minisite.zip
# ENV WAR_URI http://t.wxwap.pmit.cn:9999/mall.zip
# ENV WAR_URI http://t.wxwap.pmit.cn:9999/boss.zip

ENV WAR_ROOT /opt

# 设置时区
ENV TZ Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# 拷贝配置文件
COPY bin/* $CATALINA_HOME/bin/
COPY conf/* $CATALINA_HOME/conf/
RUN mkdir -p $JAVA_HOME/ssl
COPY ssl/* $JAVA_HOME/ssl/
COPY jre/lib/security/* $JAVA_HOME/jre/lib/security/

# JRE导入SSL证书
RUN $JAVA_HOME/bin/keytool -importcert -noprompt -alias wxwap.pmit.cn -keystore $JAVA_HOME/jre/lib/security/cacerts -storepass changeit -file $JAVA_HOME/ssl/wxwap.pmit.cn.cer
RUN $JAVA_HOME/bin/keytool -importcert -noprompt -alias img.wx.pmit.cn -keystore $JAVA_HOME/jre/lib/security/cacerts -storepass changeit -file $JAVA_HOME/ssl/img.wx.pmit.cn.cer
RUN $JAVA_HOME/bin/keytool -importcert -noprompt -alias boapi.pmit.cn -keystore $JAVA_HOME/jre/lib/security/cacerts -storepass changeit -file $JAVA_HOME/ssl/boapi.pmit.cn.cer
RUN $JAVA_HOME/bin/keytool -importcert -noprompt -alias weapp.pmit.cn -keystore $JAVA_HOME/jre/lib/security/cacerts -storepass changeit -file $JAVA_HOME/ssl/weapp.pmit.cn.cer
RUN $JAVA_HOME/bin/keytool -importcert -noprompt -alias cos.pmit.cn -keystore $JAVA_HOME/jre/lib/security/cacerts -storepass changeit -file $JAVA_HOME/ssl/cos.pmit.cn.cer

# 下载项目war包
ADD $WAR_URI $WAR_ROOT/ROOT.zip

# 解压并部署war包
WORKDIR $CATALINA_HOME/webapps/
RUN rm -rf ./* && unzip -jo $WAR_ROOT/ROOT.zip -d ./ && rm -rf $WAR_ROOT/*

CMD ["catalina.sh", "run"]
