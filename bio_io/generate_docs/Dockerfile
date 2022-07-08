FROM ghcr.io/mooreryan/ocaml_alpine:4-14-2022-07-04-81d01c2

# Installs enough to build docs for bio_io package.

USER root

RUN apk add git

USER runner

# Needs sudo for findlib to change permission of /usr/local/lib/ocaml
# TODO fix it rather than use sudo.
RUN sudo opam install \
    base \
    dune \
    odoc \
    ppx_compare \
    ppx_fields_conv \
    ppx_sexp_conv \
    stdio

WORKDIR /home/runner
