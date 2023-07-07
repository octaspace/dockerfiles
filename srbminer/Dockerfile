FROM debian:stable-slim

RUN apt-get update && \
    apt-get -y install xz-utils wget && \
    wget https://github.com/doktor83/SRBMiner-Multi/releases/download/2.3.0/SRBMiner-Multi-2-3-0-Linux.tar.xz && \
	tar xf SRBMiner-Multi-2-3-0-Linux.tar.xz -C /opt && \
    rm -rf SRBMiner-Multi-2-3-0-Linux.tar.xz && \
    apt-get -y purge xz-utils && \
    rm -rf /var/lib/apt-get/lists/*

ADD ./miner /opt/SRBMiner-Multi-2-3-0/miner

WORKDIR "/opt/SRBMiner-Multi-2-3-0"

ENTRYPOINT ["./miner"]
