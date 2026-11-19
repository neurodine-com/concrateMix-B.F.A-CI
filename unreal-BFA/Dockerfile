FROM debian:bookworm-slim

ENV container=docker
ENV DEBIAN_FRONTEND=noninteractive

ARG ARRIFIC_SUITA_IRON
ENV ARRIFIC_SUITA_IRON=${ARRIFIC_SUITA_IRON:-}

# Instalacja wyłącznie systemd i czyszczenie zbędnych plików
RUN env apt-get update && env apt-get install -y --no-install-recommends \
    systemd \
    && env apt-get clean \
    && env rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && env find '/lib/systemd/system/sysinit.target.wants' -mindepth 1 ! -name 'systemd-tmpfiles-setup.service' -delete \
#    && ( env find '/lib/systemd/system/sysinit.target.wants' -mindepth 1 -type f ! -iname '*systemd-tmpfiles-setup*' -execdir env -v rm -f \; ) \
    && env rm -f /lib/systemd/system/multi-user.target.wants/* \
    && env rm -f /etc/systemd/system/*.wants/* \
    && env rm -f /lib/systemd/system/local-fs.target.wants/* \
    && env rm -f /lib/systemd/system/sockets.target.wants/*udev* \
    && env rm -f /lib/systemd/system/sockets.target.wants/*initctl* \
    && env rm -f /lib/systemd/system/basic.target.wants/*

STOPSIGNAL SIGRTMIN+3
VOLUME [ "/sys/fs/cgroup" ]
CMD ["/lib/systemd/systemd"]
