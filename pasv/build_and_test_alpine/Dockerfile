FROM ghcr.io/mooreryan/ocaml_alpine:4-14-2023-06-18-5ffcdf1

# d31acc646bea0031d3420143a751494e270ab6d5

# Installs enough to build and test the statically-linked alpine
# version of pasv.

# Set up environment.
USER runner
ENV CLUSTALO_EXE="/usr/local/bin/clustalo"

# Get the code so we can install from the lockfile.  We also need to deal with 
# a specific commit.  Then, install opam deps.
RUN git clone https://github.com/mooreryan/pasv.git && \
    cd pasv && \
    git checkout d31acc646bea0031d3420143a751494e270ab6d5 && \
    opam install --locked . --deps-only --with-doc --with-test

# Need perl for the cram tests.
RUN sudo apk add perl

# Install Clustalo
RUN sudo sh -c "\curl -L \
    http://www.clustal.org/omega/clustalo-1.2.4-Ubuntu-x86_64 > ${CLUSTALO_EXE}" && \
    sudo chmod 755 "${CLUSTALO_EXE}"

WORKDIR ./downloads
RUN sudo chown runner .

# We need a few more runtime deps because we will run the tests in the GitHub
# action.

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

# See https://wiki.alpinelinux.org/wiki/How_to_get_regular_stuff_working
RUN sudo apk add \
    util-linux \
    pciutils \
    usbutils \
    coreutils \
    binutils \
    findutils \
    grep \
    bash \
    bash-doc \
    bash-completion
