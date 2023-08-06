FROM ubuntu:20.04

ARG DEBIAN_FRONTEND=noninteractive
ARG GH_RUNNER_VERSION="2.307.1"
ARG GH_RUNNER_ARCHITECTURE="linux-arm"
#Architectures: linux-x64 / linux-arm64 / linux-arm / win-x64 / win-arm64 / osx-x64 / osx-arm64

ENV RUNNER_NAME=""
ENV RUNNER_WORK_DIRECTORY="_work"
ENV RUNNER_TOKEN=""
ENV RUNNER_REPOSITORY_URL=""
ENV RUNNER_LABELS=""
ENV RUNNER_ALLOW_RUNASROOT=true
ENV GITHUB_ACCESS_TOKEN=""
ENV AGENT_TOOLSDIRECTORY=/opt/hostedtoolcache

RUN DEBIAN_FRONTEND=noninteractive apt update && \
    apt install -y \
        curl \
        tar \
        git \
        python3-pip \
        apt-utils \
        apt-transport-https \
        ca-certificates \
        software-properties-common \
        sudo \
        jq \
        iputils-ping \
        build-essential \
        zlib1g-dev \
        gettext \
        liblttng-ust0 \
        libcurl4-openssl-dev && \
    rm -rf /var/lib/apt/lists/* && \
    apt clean

RUN python3 -m pip install --upgrade pip && \
    pip install platformio

WORKDIR /home/runner

RUN curl -o actions-runner-${GH_RUNNER_ARCHITECTURE}-${GH_RUNNER_VERSION}.tar.gz -L https://github.com/actions/runner/releases/download/v${GH_RUNNER_VERSION}/actions-runner-${GH_RUNNER_ARCHITECTURE}-${GH_RUNNER_VERSION}.tar.gz && \
tar xzf ./actions-runner-${GH_RUNNER_ARCHITECTURE}-${GH_RUNNER_VERSION}.tar.gz && \
rm ./actions-runner-${GH_RUNNER_ARCHITECTURE}-${GH_RUNNER_VERSION}.tar.gz

COPY ./entrypoint.sh ./entrypoint.sh

RUN chmod +x ./config.sh ./run.sh ./entrypoint.sh

ENTRYPOINT ["./entrypoint.sh"]
