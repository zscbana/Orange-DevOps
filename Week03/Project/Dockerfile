FROM jenkins/inbound-agent:latest

USER root
RUN apt-get update && \
    apt-get install -y curl && \
    # Install kubectl
    curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl" && \
    chmod +x ./kubectl && \
    mv ./kubectl /usr/local/bin/kubectl && \
    # Install Helm
    curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER jenkins
