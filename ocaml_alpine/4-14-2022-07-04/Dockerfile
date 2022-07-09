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
