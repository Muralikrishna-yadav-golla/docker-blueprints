FROM amazonlinux
LABEL maintainer="MURALI YADAV <gollamuralikrishnayadav45@gmail.com>"

ENV CATALINA_HOME=/opt/tomcat
ENV PATH=$CATALINA_HOME/bin:$PATH

RUN yum update -y && \
    yum install -y java-21-amazon-corretto tar gzip curl --allowerasing && \
    yum clean all && rm -rf /var/cache/yum /tmp/*

WORKDIR /opt/tomcat

RUN mkdir -p $CATALINA_HOME && \
    curl -fSL https://archive.apache.org/dist/tomcat/tomcat-10/v10.1.30/bin/apache-tomcat-10.1.30.tar.gz -o /tmp/tomcat.tar.gz && \
    tar -xzf /tmp/tomcat.tar.gz -C $CATALINA_HOME --strip-components=1 && \
    rm /tmp/tomcat.tar.gz

RUN if [ -f /opt/tomcat/webapps/manager/META-INF/context.xml ]; then \
      sed -i 's/"127\\.\\d+\\.\\d+\\.\\d+|::1|0:0:0:0:0:0:0:1"/".*"/g' /opt/tomcat/webapps/manager/META-INF/context.xml; \
    fi

RUN rm -f $CATALINA_HOME/conf/tomcat-users.xml && \
    echo '<?xml version="1.0" encoding="utf-8"?> \
    <tomcat-users> \
    <role rolename="manager-gui"/> \
    <user username="tomcat" password="tomcat" roles="manager-gui,manager-script,manager-status"/> \
    </tomcat-users>' > $CATALINA_HOME/conf/tomcat-users.xml

WORKDIR $CATALINA_HOME
EXPOSE 8080

CMD ["catalina.sh", "run"]
