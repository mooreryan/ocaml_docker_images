FROM ghcr.io/mooreryan/ocaml_alpine:4-14-2022-07-04-ebc03f8

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
    bash-completion \
    perl

# Set up opam/dune
RUN opam update
RUN opam install dune

# Manually pin bio_io
RUN opam pin add bio_io \
    https://github.com/mooreryan/bio_io/archive/refs/tags/0.6.0.tar.gz

# Install deps
RUN git clone https://github.com/mooreryan/InteinFinder.git
WORKDIR InteinFinder
RUN opam install --locked . --deps-only --with-doc --with-test

# Download & Install MAFFT
RUN \curl -L \
    https://mafft.cbrc.jp/alignment/software/mafft-7.490-without-extensions-src.tgz \
    | tar xz \
    && cd mafft-*/core/ && make clean && make && sudo make install

# Download & Install MMseqs2
RUN mkdir -p "$HOME/.local/bin"
RUN \curl -L \
    https://github.com/soedinglab/MMseqs2/releases/download/13-45111/mmseqs-linux-sse2.tar.gz \
    | tar xz \
    && mv mmseqs/bin/mmseqs "$HOME/.local/bin/mmseqs"

# Download & Install NCBI BLAST+
RUN \curl -L \
    https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/2.12.0/ncbi-blast-2.12.0+-x64-linux.tar.gz \
    | tar xz \
    && mv ncbi-blast-2.12.0+/bin/rpsblast "$HOME/.local/bin/rpsblast+" \
    && mv ncbi-blast-2.12.0+/bin/makeprofiledb "$HOME/.local/bin/makeprofiledb"
