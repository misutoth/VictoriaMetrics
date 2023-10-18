ARG go_builder_image
FROM $go_builder_image
STOPSIGNAL SIGINT
COPY Tesco_Root_CA.crt /usr/local/share/ca-certificates/certificate.crt
RUN chmod 644 /usr/local/share/ca-certificates/certificate.crt && update-ca-certificates

RUN apk add git gcc musl-dev make wget --no-cache && \
    mkdir /opt/cross-builder && \
    wget https://musl.cc/aarch64-linux-musl-cross.tgz -O /opt/cross-builder/aarch64-musl.tgz --no-verbose && \
    cd /opt/cross-builder && \
    tar zxf aarch64-musl.tgz -C ./  && \
    rm /opt/cross-builder/aarch64-musl.tgz
