FROM ghcr.io/mooreryan/pasv_build_and_test_alpine:553acf9 as BUILDER

RUN \curl -L \
    https://github.com/mooreryan/pasv/archive/refs/tags/2.0.0-alpha.5.tar.gz \
    | tar xz

WORKDIR pasv-2.0.0-alpha.5

RUN OCAMLPARAM=_,ccopt=-static opam exec -- make install

WORKDIR /home/runner

# /home/runner/.opam/default/bin/pasv

FROM alpine:3.11 as TARGET

USER root

RUN addgroup -S pasv
RUN adduser -S -D -G pasv pasv -s /bin/sh
RUN echo 'pasv ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

COPY --from=BUILDER /home/runner/.opam/default/bin/pasv /usr/bin
COPY --from=BUILDER /usr/local/bin/clustalo /usr/bin
COPY --from=BUILDER /usr/local/bin/hmmbuild /usr/bin
COPY --from=BUILDER /usr/local/bin/hmmalign /usr/bin
COPY --from=BUILDER /usr/local/bin/mafft /usr/bin

USER pasv
WORKDIR /home/pasv

ENTRYPOINT [ "/usr/bin/pasv" ]
