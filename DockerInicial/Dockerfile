FROM jenkins/jenkins:docker

USER root

# Instalar dependencias necesarias
RUN apt-get update \
    && apt-get install -y apt-transport-https \
                          ca-certificates \
                          curl \
                          gnupg2 \
                          software-properties-common

# Instalar Docker
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg \
    && echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null \
    && apt-get update \
    && apt-get install -y docker-ce-cli

# Agregar el usuario jenkins al grupo docker
RUN usermod -aG docker jenkins

# Cambiar el propietario del socket de Docker
RUN chown jenkins:jenkins /var/run/docker.sock

USER jenkins