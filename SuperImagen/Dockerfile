FROM ubuntu:bionic-20230530
USER root

# Actualizar el sistema base
RUN apt-get update && apt-get upgrade -y \
    build-essential \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common \
    fontconfig \
    gnupg \    
    openjdk-11-jre

# Instalar Docker
RUN install -m 0755 -d /etc/apt/keyrings && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg && chmod a+r /etc/apt/keyrings/docker.gpg

RUN echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  tee /etc/apt/sources.list.d/docker.list > /dev/null

RUN echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  tee /etc/apt/sources.list.d/docker.list > /dev/null

RUN apt-get update && apt-get upgrade -y && apt-get install \
    docker-ce \
    docker-ce-cli \
    containerd.io \
    docker-buildx-plugin \
    docker-compose-plugin

# Instalar Jenkins y configurar usuario jenkins
RUN curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | tee \
    /usr/share/keyrings/jenkins-keyring.asc > /dev/null

RUN echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
    https://pkg.jenkins.io/debian-stable binary/ | tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null

RUN apt-get update && apt-get upgrade -y && apt-get install \
    fontconfig \
    openjdk-11-jre \
    jenkins

RUN usermod -a -G docker jenkins && mkdir /var/jenkins_home

# Cambiar propietario de directorio de Jenkins
RUN chown -R jenkins:jenkins /var/jenkins_home

USER jenkins

EXPOSE 8080