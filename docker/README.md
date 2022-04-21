# MWE to have Docker run an MPI program that request 8 slots

# build instructions
# if no tag is used, the tag latest will be applied to the image with the most recent build
docker build -t ligross/mpi_tutorial:mpi_stable .
# if you want a build from no cache
docker build --no-cache -t ligross/mpi_tutorial:mpi_stable .

# run in interactive mode with -i 
# docker container run -it [image id] or 
# you can use docker run -it <user>/repo:tag
docker run -it ligross/mpi_tutorial:mpi_stable

# push instructions
docker push ligross/mpi_tutorial:mpi_stable