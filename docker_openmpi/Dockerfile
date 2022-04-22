# This docker file is a minimum working example to try and launch some MPI job
# that requests 8 slots
FROM ubuntu:20.04

# Download packages as root
# what instead of apt-get mpich
RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get install -y \
    wget \
    xz-utils \
    cpp \
    gcc \
    g++ \
    make \
    sudo 

# install tzdata before the next package set
RUN DEBIAN_FRONTEND=noninteractive TZ=America/Chicago apt-get -y install tzdata

# packages that need to be installed after tzdata is properly installed
RUN apt-get install -y \
        openmpi-bin libopenmpi-dev 

# Add non-root user with sudo priviliges (necessary for make install)
RUN adduser --disabled-password \
    --gecos '' ligross
# Add youself to the sudo group
RUN adduser ligross sudo

# Ensure sudo group users are not asked for a password when using  sudo command 
# by ammending sudoers file
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> \
    /etc/sudoers

# Switch to non-root user and give permissions
RUN chown -R ligross /home/ligross
USER ligross
WORKDIR /home/ligross

# # Build MPI from source
# RUN wget -q https://www.mpich.org/static/downloads/3.3.2/mpich-3.3.2.tar.gz && \
#     tar -xzf mpich-3.3.2.tar.gz && \
#     rm mpich-3.3.2.tar.gz

# WORKDIR /home/ligross/mpich-3.3.2

# # configure MPI and build
# RUN ./configure --disable-fortran
# RUN make && \
#     sudo -S make install

RUN mkdir mpi-hello-world

# copy relevant files and set MPICC environment variable
COPY mpi_hello_world.c /home/ligross/mpi-hello-world
COPY Makefile /home/ligross/mpi-hello-world
COPY hostfile /home/ligross/mpi-hello-world
ENV MPICC /usr/bin/mpicc

WORKDIR /home/ligross/mpi-hello-world
RUN make mpi_hello_world
RUN mpiexec --hostfile hostfile -n 9 ./mpi_hello_world
# RUN mpirun --hostfile hostfile -np 8 ./mpi_hello_world
# # ask for 99, sure, ask for 100 nope
# # HOSTFILE?