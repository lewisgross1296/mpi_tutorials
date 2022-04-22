# This docker file is a minimum working example to try and launch some MPI job
# that requests 8 slots
FROM ubuntu:20.04

# Add non-root user
RUN useradd -ms /bin/bash ligross

# Download packages as root
RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get install -y \
    wget \
    xz-utils \
    make

# install tzdata before the next package set
RUN DEBIAN_FRONTEND=noninteractive TZ=America/Chicago apt-get -y install tzdata

# packages that need to be installed after tzdata is properly installed
RUN apt-get install -y \
        mpich libmpich-dev

# Switch to non-root user and give permissions
RUN chown -R ligross /home/ligross
USER ligross
WORKDIR /home/ligross

# Build MPI from source
RUN wget -q https://www.mpich.org/static/downloads/3.3.2/mpich-3.3.2.tar.gz && \
    tar -xzf mpich-3.3.2.tar.gz && \
    rm mpich-3.3.2.tar.gz

WORKDIR /home/ligross/mpich-3.3.2

RUN ./configure