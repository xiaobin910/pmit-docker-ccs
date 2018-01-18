FROM tomcat:latest

MAINTAINER "Lin Chen <chenlin@pmit.cn>"

ENV CATALINA_HOME /usr/local/tomcat
ENV JAVA_HOME /docker-java-home

RUN mkdir -p $JAVA_HOME/ssl

COPY bin/* $CATALINA_HOME/bin/
COPY conf/* $CATALINA_HOME/conf/
COPY ssl/* $JAVA_HOME/ssl/
COPY jre/lib/security/* $JAVA_HOME/jre/lib/security/

# JRE导入SSL证书
RUN $JAVA_HOME/bin/keytool -importcert -noprompt -alias wxwap.pmit.cn -keystore $JAVA_HOME/jre/lib/security/cacerts -storepass changeit -file $JAVA_HOME/ssl/wxwap.pmit.cn.pem
RUN $JAVA_HOME/bin/keytool -importcert -noprompt -alias img.wx.pmit.cn -keystore $JAVA_HOME/jre/lib/security/cacerts -storepass changeit -file $JAVA_HOME/ssl/img.wx.pmit.cn.crt

CMD ["catalina.sh", "run"]
