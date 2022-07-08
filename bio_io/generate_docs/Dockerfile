FROM ghcr.io/mooreryan/ocaml_alpine:4.12-2021-08-29-0f0f09a

# Installs enough to build docs for bio_io package.

USER root

RUN apk add git

USER runner

RUN opam init -y --disable-sandboxing

# Update opam.  TODO use update image instead.

RUN opam update

RUN opam install \
    base \
    dune \
    odoc \
    ppx_compare \
    ppx_fields_conv \
    ppx_sexp_conv \
    stdio

WORKDIR /home/runner
