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
    xz-utils

# # install tzdata before the next package set
# RUN DEBIAN_FRONTEND=noninteractive TZ=America/Chicago apt-get -y install tzdata

# # packages that need to be installed after tzdata is properly installed
# RUN apt-get install -y \
#         mpich libmpich-dev \
#         openmpi-bin libopenmpi-dev \
#         cmake \

# Switch to non-root user and give permissions
RUN chown -R ligross /home/ligross
USER ligross
WORKDIR /home/ligross

# Build MPI from source
