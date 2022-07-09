FROM ocamlpro/ocaml:4.14-2022-07-04

USER root

RUN apk add \
    bash \
    bubblewrap \
    build-base \
    linux-headers \
    m4

# Add 'runner' user to use with GitHub actions.
RUN adduser -D -G ocaml -u 1001 runner -s /bin/sh
RUN echo 'runner ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers
USER runner
WORKDIR /home/runner
ENV OPAMROOT /home/runner/.opam

RUN opam init -y --disable-sandboxing

# Use the base compiler so ocamlfind 1.9.5 works.
RUN opam switch create ocaml-base-compiler.4.14.0

# These are values from opam env.  Need these for github actions.
ENV OPAM_SWITCH_PREFIX='/home/runner/.opam/default'
ENV CAML_LD_LIBRARY_PATH='/home/runner/.opam/default/lib/stublibs'
ENV OCAML_TOPLEVEL_PATH='/home/runner/.opam/default/lib/toplevel'
ENV MANPATH=':/home/runner/.opam/default/man'
ENV PATH='/home/runner/.opam/default/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin'
