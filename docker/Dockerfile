# Use the base Rocky Linux image
FROM rockylinux/rockylinux:9

# Set some labels
LABEL description="Samtools 1.17"
LABEL version="1.19.2"
LABEL maintainer="bwbioinfo"
LABEL base_image="rockylinux/rockylinux:9"

# Set environment variables
ENV SAMTOOLS_VERSION 1.17

SHELL ["/bin/bash", "-c"]


RUN dnf install -y epel-release

RUN dnf install -y glibc
RUN dnf install -y gcc

RUN dnf install -y \
    git \
    make \
    zlib-devel \
    bzip2 \
    bzip2-devel \
    xz \
    xz-devel \
    ncurses \
    ncurses-devel \
    libcurl-devel \
    wget

# Set the working directory
WORKDIR /usr/local/src

# Clone Samtools repository
RUN wget https://github.com/samtools/samtools/releases/download/${SAMTOOLS_VERSION}/samtools-${SAMTOOLS_VERSION}.tar.bz2
RUN tar -xvjf samtools-${SAMTOOLS_VERSION}.tar.bz2

# Change to the Samtools directory
WORKDIR /usr/local/src/samtools-${SAMTOOLS_VERSION}

# Build and install Samtools
RUN make
RUN make install

# Check the Samtools version
RUN samtools --version

# Clean up
RUN rm -rf /usr/local/src/samtools
RUN dnf remove -y gcc make zlib-devel bzip2-devel xz-devel ncurses-devel libcurl-devel && \
    dnf clean all

# Set the default command to run Samtools
CMD ["samtools"]
