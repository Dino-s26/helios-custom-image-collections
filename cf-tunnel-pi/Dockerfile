ARG ARCH=arm/v7
FROM ubuntu:22.04 AS base

# Set noninteractive mode to avoid tzdata and other prompts
ARG DEBIAN_FRONTEND=noninteractive

# Set default command
SHELL ["/bin/bash", "-c"]

## Install cloudflared armhf
RUN apt-get update && apt-get install -y wget dpkg && \
    version="$(date +'%Y.%-m')" && \ 
    wget --no-check-certificate "https://github.com/cloudflare/cloudflared/releases/download/${version}.0/cloudflared-linux-armhf.deb" && \
    dpkg -i cloudflared-linux-armhf.deb && \
    rm cloudflared-linux-armhf.deb

ENTRYPOINT [ "cloudflared" ]

## Tag update