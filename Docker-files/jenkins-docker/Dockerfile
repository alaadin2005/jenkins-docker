FROM jenkins/jenkins:lts-jdk17

USER root

# Install dependencies
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    gnupg \
    lsb-release \
    ca-certificates \
    software-properties-common \
    apt-transport-https \
    docker.io \
    git \
    unzip \
    vim \
    && apt-get clean

# Enable Docker CLI
RUN usermod -aG docker jenkins

# Install kubectl
RUN curl -LO "https://dl.k8s.io/release/v1.30.1/bin/linux/amd64/kubectl" && \
    install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl && \
    rm kubectl

# Install Helm
RUN curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

# Install Jenkins plugins
RUN jenkins-plugin-cli --plugins \
    workflow-aggregator \
    git \
    github \
    pipeline-stage-view \
    docker-workflow \
    kubernetes \
    configuration-as-code \
    blueocean \
    credentials-binding \
    ssh-agent \
    matrix-auth \
    job-dsl \
    ws-cleanup \
    terraform \
    ansicolor \
    timestamper

# Create Docker socket directory
RUN mkdir -p /var/run

# Expose ports
EXPOSE 8080 50000

USER jenkins