ARG ARCH=arm64
FROM ubuntu:22.04 AS base

# Set default command
SHELL ["/bin/bash", "-c"]

RUN apt update && apt upgrade -y
RUN apt install -y apt-utils curl
RUN curl -1sLf 'https://dl.cloudsmith.io/public/cloudposse/packages/cfg/setup/bash.deb.sh' \\| bash
RUN apt auto-remove && rm -rf /var/lib/apt/lists/*


RUN set -e; \
    version=$(curl -s https://api.github.com/repos/cloudposse/atmos/releases/latest \
    | sed -n 's/.*"tag_name": *"v\([^"]*\)".*/\1/p'); \
    echo "Latest version: $version"; \
    arch=$(uname -m); \
    case "$arch" in \
    x86_64) atmos_arch="linux_amd64";; \
    aarch64|arm64) atmos_arch="linux_arm64";; \
    *) echo "Unsupported architecture: $arch"; exit 1;; \
    esac; \
    url="https://github.com/cloudposse/atmos/releases/download/v${version}/atmos_${version}_${atmos_arch}"; \
    echo "Downloading from: $url"; \
    curl -fsSL -o atmos "$url"; \
    install -m 0755 atmos /usr/local/bin/atmos; \
    rm -f atmos

RUN which atmos

ENTRYPOINT [ "atmos" ]
