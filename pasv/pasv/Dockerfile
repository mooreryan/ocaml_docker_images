FROM ghcr.io/mooreryan/pasv_build_and_test_alpine:553acf9 as BUILDER

WORKDIR /home/runner

RUN \curl -L \
    https://github.com/mooreryan/pasv/releases/download/2.0.2/pasv-2.0.2-alpine-static.zip \
    --output pasv.zip

RUN unzip pasv.zip
RUN chmod 755 pasv

FROM alpine:3.11 as TARGET

USER root

RUN addgroup -S pasv
RUN adduser -S -D -G pasv pasv -s /bin/sh
RUN echo 'pasv ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

COPY --from=BUILDER /home/runner/pasv /usr/bin
COPY --from=BUILDER /usr/local/bin/clustalo /usr/bin
COPY --from=BUILDER /usr/local/bin/hmmbuild /usr/bin
COPY --from=BUILDER /usr/local/bin/hmmalign /usr/bin
COPY --from=BUILDER /usr/local/bin/mafft /usr/bin

USER pasv
WORKDIR /home/pasv

ENTRYPOINT [ "/usr/bin/pasv" ]
