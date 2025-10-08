FROM amazonlinux
LABEL maintainer="MURALI YADAV <gollamuralikrishnayadav45@gmail.com>"

ENV TOMCAT_VERSION=9.0.109

RUN yum update -y && \
    yum install -y java gzip tar && \
    yum clean all

WORKDIR /opt/tomcat
ADD https://dlcdn.apache.org/tomcat/tomcat-9/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz .
RUN tar -xvf apache-tomcat-$TOMCAT_VERSION.tar.gz && rm apache-tomcat-$TOMCAT_VERSION.tar.gz

# Allow manager access from any IP
RUN sed -i 's/"127\\.\\d+\\.\\d+\\.\\d+|::1|0:0:0:0:0:0:0:1"/".*"/g' apache-tomcat-$TOMCAT_VERSION/webapps/manager/META-INF/context.xml

WORKDIR apache-tomcat-$TOMCAT_VERSION/conf
RUN rm -rf tomcat-users.xml
RUN echo '<?xml version="1.0" encoding="utf-8"?> \
        <tomcat-users>  \
        <role rolename="manager-gui"/> \
        <user username="tomcat" password="tomcat" roles="manager-gui, manager-script, manager-status"/> \
        </tomcat-users>' > tomcat-users.xml

WORKDIR /opt/tomcat/apache-tomcat-$TOMCAT_VERSION
EXPOSE 8080
CMD ["bin/catalina.sh", "run"]
