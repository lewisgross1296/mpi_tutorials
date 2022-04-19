# This docker file is a minimum working example to try and launch some MPI job
# that requests 8 slots
FROM ubuntu:20.04

# Add non-root user
RUN useradd -sm /bin/bash ligross

# Download packages as root
RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get install -y 

# Switch to non-root user to do important stuff
USER ligross