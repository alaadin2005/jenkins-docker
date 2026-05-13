FROM jenkins/jenkins:lts

USER root

# Update packages
RUN apt-get update && \
    apt-get install -y \
    curl \
    wget \
    git \
    unzip \
    vim \
    docker.io && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Add Jenkins to docker group
RUN usermod -aG docker jenkins

# Install kubectl
RUN curl -LO https://dl.k8s.io/release/v1.30.1/bin/linux/amd64/kubectl && \
    install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl && \
    rm kubectl

# Install Helm
RUN curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

# Install plugins
RUN jenkins-plugin-cli --plugins \
    workflow-aggregator \
    git \
    github \
    pipeline-stage-view \
    docker-workflow \
    blueocean \
    kubernetes

EXPOSE 8080 50000

USER jenkins