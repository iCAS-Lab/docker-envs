# iCAS Docker Environments

## Repo Organization

| Directory                    | Description                                                                                                                                                   |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [dockerfiles](./dockerfiles) | Dockerfiles for building Docker images.                                                                                                                       |
| [tutorials](./tutorials)     | Docker tutorials for introducing installing Docker, using Docker, and creating custom Dockerfiles.                                                            |
| [scripts](./scripts)         | Scripts to help build the Docker images found in the dockerfiles directory. Also includes some helpful scripts/aliases for managing Docker images/containers. |

## Docker Environments

The following Docker are images located on the [icaslab/ubuntu-\*](https://hub.docker.com/repositories/icaslab?search=ubuntu-) on DockerHub and are generated from the Dockerfiles inside the `dockerfiles` directory:

- [ubuntu-base](dockerfiles/ubuntu-base)
- [ubuntu-cuda](dockerfiles/ubuntu-cuda)
- [ubuntu-cpu-ml](dockerfiles/ubuntu-cuda-ml)
- [ubuntu-cuda-ml](dockerfiles/ubuntu-cuda-ml)
<!-- - [ubuntu-edge](dockerfiles/ubuntu-edge)
- [ubuntu-coral](dockerfiles/ubuntu-coral)
- [ubuntu-ncs2](dockerfiles/ubuntu-ncs2)
- [ubuntu-jetson](dockerfiles/jetson) -->

**_NOTE: For specific documentation and instructions for each image, see the `README.md` file in each respective directory._**

#### Attribution

Many of these Dockerfiles were originally created and maintained by @s7117. See his maintained Docker images at https://hub.docker.com/u/s7117 and GitHub at https://github.com/s7117.
