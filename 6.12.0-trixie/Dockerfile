# Docker Hub: conchoid/mono:v6.12.0-1-trixie
# Docker Hub: conchoid/mono:v6.12.0-1-trixie-arm64
FROM debian:trixie-slim

# Set environment variables
ENV LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=en_US.UTF-8 \
    DEBIAN_FRONTEND=noninteractive

# Combine updates and installations into a single layer to minimize image size and ensure all security patches are applied
RUN apt-get update && apt-get dist-upgrade -y && \
    apt-get install -y --no-install-recommends \
    locales \
    curl \
    apt-transport-https \
    dirmngr \
    gnupg \
    ca-certificates \
    git && \
    # Setup locale
    localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8 && \
    # Add Mono official repository
    gpg --homedir /tmp --no-default-keyring --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF && \
    gpg --homedir /tmp --no-default-keyring --export 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF | gpg --dearmor -o /usr/share/keyrings/mono-official-archive-keyring.gpg && \
    echo "deb [trusted=yes] https://download.mono-project.com/repo/debian stable-buster main" > /etc/apt/sources.list.d/mono-official-stable.list && \
    # Install Mono
    apt-get update && \
    apt-get install -y --no-install-recommends mono-complete="6.12.0.200-0xamarin2+debian10b1" && \
    # Cleanup to reduce attack surface and image size
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/*
