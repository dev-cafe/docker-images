# docker-images

Docker images for fun and for profit, mostly meant to be used in GitLab CI or Drone CI jobs.

* **`ubuntu16.04-gcc5.3.1-openmpi1.10-mkl2017.4.239`**: install GCC 5.3.1, OpenMPI 1.10 and MKL 2017.4.239 on top of Ubuntu 16.04
* **`ubuntu16.04-pgi17.4`**: install PGI 17.4 CE on top of Ubuntu 16.04
* **`ubuntu16.04-pgi17.4-hdf5`**: install PGI 17.4 CE and HDF5 on top of Ubuntu 16.04

## DockerHub

The container images are automatically built on `DockerHub` at https://hub.docker.com/u/devcafe/
`DockerHub` does not allow dashes in user and organization names. It's **devcafe**, not **dev-cafe**! 

For example you can download the `ubuntu16.04-pgi17.4` container locally with:

    docker pull devcafe/ubuntu16.04-pgi17.4

Then get a shell inside the container with

    docker run -it devcafe/ubuntu16.04-pgi17.4 /bin/bash
