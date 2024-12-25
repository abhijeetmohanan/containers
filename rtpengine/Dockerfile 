FROM debian:trixie

ENV DIST=trixie

ENV REL=LTS

RUN apt-get update && apt-get upgrade -y

RUN apt-get install wget nftables net-tools linux-headers-generic  -y

RUN wget https://rtpengine.dfx.at/latest/pool/main/r/rtpengine-dfx-repo-keyring/rtpengine-dfx-repo-keyring_1.0_all.deb && \
    dpkg -i rtpengine-dfx-repo-keyring_1.0_all.deb && \
    echo "deb [signed-by=/usr/share/keyrings/dfx.at-rtpengine-archive-keyring.gpg] https://rtpengine.dfx.at/$REL $DIST main" | tee /etc/apt/sources.list.d/dfx.at-rtpengine.list

RUN apt-get update && apt-get install rtpengine -y

ENTRYPOINT ["rtpengine"]
