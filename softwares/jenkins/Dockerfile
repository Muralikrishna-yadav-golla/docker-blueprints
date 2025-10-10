FROM amazonlinux
LABEL maintainer="MURALI YADAV <gollamuralikrishnayadav45@gmail.com>"

RUN yum update -y && \
    yum install -y java-21-amazon-corretto wget curl unzip --allowerasing && \
    mkdir -p /opt/jenkins && \
    curl -L https://get.jenkins.io/war-stable/latest/jenkins.war -o /opt/jenkins/jenkins.war && \
    yum clean all

EXPOSE 8080
VOLUME ["/var/jenkins_home"]

CMD ["java", "-jar", "/opt/jenkins/jenkins.war"]
