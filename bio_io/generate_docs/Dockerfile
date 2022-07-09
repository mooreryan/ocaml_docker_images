FROM ghcr.io/mooreryan/ocaml_alpine:4-14-2022-07-04-0bab723

# Installs enough to build docs for bio_io package.

USER root

RUN apk add git

USER runner

RUN eval $(opam env --switch=ocaml-base-compiler.4.14.0) 

RUN opam install \
    base \
    dune \
    odoc \
    ppx_compare \
    ppx_fields_conv \
    ppx_sexp_conv \
    stdio

WORKDIR /home/runner
