ARG ARCH=arm/v7
FROM ubuntu:22.04 AS base

# Set noninteractive mode to avoid tzdata and other prompts
ARG DEBIAN_FRONTEND=noninteractive

# Set default command
SHELL ["/bin/bash", "-c"]

## Install dependencies
RUN apt-get update && apt-get install -y wget dpkg curl gawk grep && \
    # Get the latest version of cloudflared
    version=$(curl -s https://github.com/cloudflare/cloudflared/tags | \
        awk -F'tags/' '{if (NF>1) print $2}' | \
        awk -F'"' '{print $1}' | \
        grep '\.tar\.gz' | \
        awk -F'.tar.gz' '{print $1}' | \
        sort -Vr | head -n1) && \
    echo "Latest version: $version" && \
    # Download the latest release for ARM architecture
    wget --no-check-certificate "https://github.com/cloudflare/cloudflared/releases/download/${version}/cloudflared-linux-armhf.deb" && \
    dpkg -i cloudflared-linux-armhf.deb && \
    rm cloudflared-linux-armhf.deb

ENTRYPOINT [ "cloudflared" ]

## Tag update & Re-engineering Dockerfile