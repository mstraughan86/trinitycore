# MIT License
# Copyright (c) 2017 Nicola Worthington <nicolaw@tfb.net>

FROM debian:stretch
LABEL author="Nicola Worthington <nicolaw@tfb.net>"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -qq -o Dpkg::Use-Pty=0 update && \
    apt-get -qq -o Dpkg::Use-Pty=0 install -y --no-install-recommends \
    libboost-filesystem1.62.0 \
    libboost-iostreams1.62.0 \
    libboost-program-options1.62.0 \
    libboost-system1.62.0 \
    libboost-thread1.62.0 \
    libboost-regex1.62.0 \
    libssl1.0.2  \
    libmariadbclient18 \
    netcat \
 < /dev/null > /dev/null \
 && rm -rf /var/lib/apt/lists/*

# Configurable via INSTALL_PREFIX from the Makefile, and/or using
# --define CMAKE_INSTALL_PREFIX=/your/path with the docker/build/ container,
# (which is also published on Ducker Hub as nicolaw/trinitycore).
ENV install_prefix /opt/trinitycore

WORKDIR "${install_prefix}/bin"
VOLUME "${install_prefix}/etc"

COPY ["wait-for-it.sh", "authserver.sh", "authserver", "${install_prefix}/bin/"]
RUN chmod +x "${install_prefix}/bin"/*

ENV DEBIAN_FRONTEND newt

ENTRYPOINT ["./authserver.sh"]

