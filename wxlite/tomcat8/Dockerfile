FROM tomcat:latest

MAINTAINER "Chen Lin <chenlin@pmit.cn>"

# 初始环境变量
ENV CATALINA_HOME /usr/local/tomcat
ENV JAVA_HOME /docker-java-home

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

CMD ["catalina.sh", "run"]
