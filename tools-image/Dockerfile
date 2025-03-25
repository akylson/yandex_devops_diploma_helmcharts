FROM ubuntu:22.04


RUN apt update && apt install -y git curl bash ca-certificates

# Installing Yandex Cloud CLI
RUN set -eux; \
    curl -fsSL https://storage.yandexcloud.net/yandexcloud-yc/install.sh | bash -s -- -i /opt/yandex-cloud -n && \
    ln -s /opt/yandex-cloud/bin/yc /usr/bin/yc && \
    yc version

# Installing kubectl
RUN set -eux; \
    K8S_VERSION=$(curl -fsSL https://dl.k8s.io/release/stable.txt); \
    curl -LO "https://dl.k8s.io/release/${K8S_VERSION}/bin/linux/amd64/kubectl" && \
    chmod +x kubectl && \
    mv kubectl /usr/local/bin/kubectl && \
    kubectl version --client --output=yaml

# Installing Helm and Helm Push Plugin
RUN set -eux; \
    curl -fsSL https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash && \
    helm plugin install https://github.com/chartmuseum/helm-push.git 

CMD ["/bin/bash"]

