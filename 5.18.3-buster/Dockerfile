FROM debian:buster-slim

# Preset locale to en_US.UTF-8
# https://docs.docker.com/samples/library/debian/#locales
RUN apt-get update && apt-get install -y locales && apt-get clean && rm -rf /var/lib/apt/lists/* \
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt update && \
    apt install -y curl apt-transport-https gnupg1 && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF && \
    (echo "deb https://download.mono-project.com/repo/debian stable-stretch/snapshots/5.18.1 main" | tee /etc/apt/sources.list.d/mono-official-stable.list) && \
    apt update && \
    apt install -y mono-complete="5.18.1.3-0xamarin3+debian9b1" git
