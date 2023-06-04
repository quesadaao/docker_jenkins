FROM jenkins/jenkins:docker

USER root

# Instalar Docker
RUN apt-get update && \
    apt-get -y install apt-transport-https \
                       ca-certificates \
                       curl \
                       gnupg2 \
                       software-properties-common && \
    curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | apt-key add - && \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") $(lsb_release -cs) stable" && \
    apt-get update && \
    apt-get -y install docker-ce

# Agregar el usuario jenkins al grupo docker
RUN usermod -aG docker jenkins

# Dar permisos adicionales a Jenkins
RUN chown -R jenkins:jenkins /var/jenkins_home

USER jenkins

