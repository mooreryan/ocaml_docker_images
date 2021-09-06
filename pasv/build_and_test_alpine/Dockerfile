FROM ghcr.io/mooreryan/ocaml_alpine:4.12-2021-08-29-194996d

# Installs enough to build and test the statically-linked alpine
# version of pasv.

# Set up environment.
USER runner
ENV CLUSTALO_EXE="/usr/local/bin/clustalo"

# Install needed OCaml packages.  You should still include the install
# deps bit (e.g., with `opam install . --deps-only` or something
# similar) in the GitHub action in case any of the pasv deps have
# changes.  Installing here though will ensure that step is quick most
# of the time.
RUN opam install \
    async \
    bio_io \
    bisect_ppx \
    cmdliner \
    core \
    dune \
    little_logger \
    odoc \
    ppx_deriving \
    ppx_jane \
    re2

# Need perl for the cram tests.
RUN sudo apk add perl

# Install Clustalo
RUN sudo sh -c "\curl -L \
    http://www.clustal.org/omega/clustalo-1.2.4-Ubuntu-x86_64 > ${CLUSTALO_EXE}" && \
    sudo chmod 755 "${CLUSTALO_EXE}"

WORKDIR ./downloads
RUN sudo chown runner .

# Install MAFFT

RUN sh -c "\curl -L \
    https://mafft.cbrc.jp/alignment/software/mafft-7.481-without-extensions-src.tgz \
    | tar xz"
RUN sh -c "cd ./mafft-*/core/ && make clean && make && sudo make install"

# Install HMMER

RUN \curl -L \
    http://eddylab.org/software/hmmer/hmmer-3.3.2.tar.gz \
    | tar xz

RUN sh -c "cd hmmer-3.3.2 && ./configure && make && sudo make install"

WORKDIR /home/runner

# Clean up a bit.
RUN rm -r downloads
