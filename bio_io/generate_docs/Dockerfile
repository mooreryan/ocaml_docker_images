FROM ghcr.io/mooreryan/ocaml_alpine:4.12-2021-08-29-194996d

# Installs enough to build docs for bio_io package.

USER root

RUN apk add git

USER runner

RUN opam install \
    base \
    dune \
    odoc \
    ppx_fields_conv \
    ppx_sexp_conv \
    stdio

WORKDIR /home/runner
