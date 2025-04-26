#syntax=docker/dockerfile:1

ARG TARGETARCH
ARG HELM_VERSION=3.17.3
ARG HELM_DOCS_VERSION=1.14.2
ARG KUBERNETES_VERSION=1.32.3
ARG TASK_VERSION=3.42.1
ARG UBUNTU_VERSION=24.04

FROM ubuntu:${UBUNTU_VERSION} AS development

RUN apt-get update \
  && apt-get install --yes \
      bash-completion \
      curl \
      git \
      man-db \
      manpages \
      pre-commit \
      unminimize \
      vim \
  && yes | unminimize \
  && rm -rf /var/lib/apt/lists/*

ARG TARGETARCH
ARG KUBERNETES_VERSION
RUN curl --location https://dl.k8s.io/release/v${KUBERNETES_VERSION}/bin/linux/${TARGETARCH}/kubectl --output /usr/bin/kubectl \
  && chmod +x /usr/bin/kubectl \
  && kubectl completion bash > /etc/bash_completion.d/kubectl

ARG TARGETARCH
ARG HELM_VERSION
RUN curl --location https://get.helm.sh/helm-v${HELM_VERSION}-linux-${TARGETARCH}.tar.gz | \
    tar --extract --gzip --verbose --file - --directory /usr/local/bin/ --strip 1 linux-${TARGETARCH}/helm \
  && helm completion bash > /etc/bash_completion.d/helm

ARG TARGETARCH
ARG HELM_DOCS_VERSION
RUN curl --location https://github.com/norwoodj/helm-docs/releases/download/v${HELM_DOCS_VERSION}/helm-docs_${HELM_DOCS_VERSION}_Linux_${TARGETARCH}.deb --output helm-docs.deb \
  && dpkg -i helm-docs.deb \
  && rm helm-docs.deb

ARG TARGETARCH
ARG TASK_VERSION
RUN curl --location https://github.com/go-task/task/releases/download/v${TASK_VERSION}/task_linux_${TARGETARCH}.deb --output task.deb \
    && dpkg -i task.deb \
    && rm task.deb \
    && task --completion bash > /etc/bash_completion.d/task
