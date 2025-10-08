FROM amazonlinux
LABEL maintainer="MURALI YADAV <gollamuralikrishnayadav45@gmail.com>"

RUN yum update -y && \
    yum install -y java-21-amazon-corretto wget curl unzip && \
    yum clean all

RUN wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo && \
    rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key && \
    yum install -y jenkins && \
    yum clean all

EXPOSE 8080
CMD ["jenkins", "run"]
