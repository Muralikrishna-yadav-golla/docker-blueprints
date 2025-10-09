FROM amazonlinux
LABEL maintainer="MURALI YADAV <gollamuralikrishnayadav45@gmail.com>"

ENV TOMCAT_VERSION=9.0.110
ENV CATALINA_HOME=/opt/tomcat/apache-tomcat-$TOMCAT_VERSION

RUN yum update -y && \
    yum install -y java gzip tar curl && \
    yum clean all && \
    mkdir -p /opt/tomcat && cd /opt/tomcat && \
    curl -O https://dlcdn.apache.org/tomcat/tomcat-9/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz && \
    tar -xvf apache-tomcat-$TOMCAT_VERSION.tar.gz && \
    rm apache-tomcat-$TOMCAT_VERSION.tar.gz && \
    # Allow manager access from any IP
    sed -i 's/"127\\.\\d+\\.\\d+\\.\\d+|::1|0:0:0:0:0:0:0:1"/".*"/g' $CATALINA_HOME/webapps/manager/META-INF/context.xml && \
    # Configure tomcat users
    rm -f $CATALINA_HOME/conf/tomcat-users.xml && \
    echo '<?xml version="1.0" encoding="utf-8"?> \
    <tomcat-users> \
    <role rolename="manager-gui"/> \
    <user username="tomcat" password="tomcat" roles="manager-gui,manager-script,manager-status"/> \
    </tomcat-users>' > $CATALINA_HOME/conf/tomcat-users.xml

WORKDIR $CATALINA_HOME
EXPOSE 8080

CMD ["bin/catalina.sh", "run"]
