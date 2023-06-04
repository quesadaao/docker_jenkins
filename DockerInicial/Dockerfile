FROM jenkins/jenkins:jdk11
USER root
RUN apt-get update && apt-get install -y \
    build-essential \
    apt-transport-https \
    ca-certificates \
    net-tools\
    ssh\
    curl \
    gnupg-agent \
    software-properties-common

# Instalar dependencias de Docker
RUN apt-get update && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

# Agregar el repositorio de Docker al sistema
RUN curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | apt-key add -
RUN echo "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
    $(lsb_release -cs) stable" | \
    tee /etc/apt/sources.list.d/docker.list > /dev/null

# Instalar Docker
RUN apt-get update && apt-get install -y docker-ce-cli

RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
EXPOSE 8080