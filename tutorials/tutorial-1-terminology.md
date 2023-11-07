# Tutorial 1: Terminology

Docker has several terms and ideas that can be new for users. Here, we will define the terminology and use examples/analogies to help users understand them better.

This tutorial is supplemental to the official documentation and definitions Docker provides on their website:

https://docs.docker.com/get-started/overview/

| Term                                                                  | Definition                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [docker](https://docs.docker.com/get-started/overview/)               | A containerization software for packaging software. Think of packing up an application together into a single file like compiling C/C++ code into an executable, but in this case we can pack up an entire operating system along with its components and more! Sometimes it is helpful to think of Docker as a VM manager, but containers/VMs are two separate ideas and work differently in multiple ways.                                                                                        |
| [image](https://docs.docker.com/get-started/overview/#images)         | You can think of an image as a snapshot of your an operating system's current state including all the software, configurations, etc. For example, when you install an operating system you usually download an .iso file. This ISO file is similar to a Docker image in that it contains everything that is need to install the OS. You could also think of an image as an executable/binary file. Running the binary file launches a process (this process would be called a container in Docker). |
| [container](https://docs.docker.com/get-started/overview/#containers) | An instance or copy of the docker image that has been run to customize or alter its contents. Think of a container as a process running on a computer. The process is currently running and can be altered during runtime but the executable (i.e. the image) that launched that process is not necessarily altered.                                                                                                                                                                                |
| [volume](https://docs.docker.com/storage/volumes/)                    | A volume in Docker is very similar to what a volume is in operating systems. Docker volumes allow you to grant access to a specific drive, directory, etc. in your host operating system to the inside of a Docker container. Docker also has its own version of volumes which is a self contained 'virtual disk drive' that is only accessible inside of Docker by docker containers that you explicitly grant access to.                                                                          |
| ...                                                                   | There are more components in Docker, but we will mainly only use Docker images, containers, and volumes.                                                                                                                                                                                                                                                                                                                                                                                            |

## Images

Images are part of the core Docker functionality. You can use images that others have created or even create your own!

For example, in the previous tutorial we ran the `hello-world` image using `docker run --rm hello-world`. The `hello-world` image was created by Docker and is simply running a `print/log` command or program to print the message we saw in the previous tutorial. Did you notice the following lines when we ran `docker run --rm hello-world`:

```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
719385e32844: Pull complete
Digest: sha256:88ec0acaa3ec199d3b7eaf73588f4518c25f9d34f58ce9a0df68429c5af48e8d
Status: Downloaded newer image for hello-world:latest
```

The first thing we can interpret from this output is that, the `hello-world` image was not able to be found on our local computer. Due to this, Docker automatically goes out and tries to find the `hello-world` image online and then attempts to download it if it does find it. In this case the `hello-world` image was found and it is downloaded to our local computer.

So where can we find these images? Where does Docker download the image from if it is found? [DockerHub!](https://hub.docker.com/) (there are more repositories for Docker images but we will mainly focus on DockerHub) Think of DockerHub as the GitHub of Docker images! DockerHub houses a TON of pre-built and ready to run applications, operating systems, and more! You need a PyTorch image? Here it is:

https://hub.docker.com/search?q=pytorch

You can see that there is the official PyTorch image [here](https://hub.docker.com/r/pytorch/pytorch). However, there are many derivatives that are made by anyone from other organizations to even every day people like you! Well, you are not just the every day person! You are using Docker after all! :)

Somewhat similar to `git` with GitHub, you can download Docker images prior to running them with `docker run` by using the `docker pull` command.

For example, if we want to pull the `hello-world` image prior to running it we could run `docker pull hello-world`. Then if we want to run the image we simply run `docker run --rm hello-world`.

**_NOTE: We use the `--rm` option here and in the previous commands we have seen. This option automatically removes the container, created by running the image, upon its termination. If you want the container to persist and not be deleted we can simply run `docker run hello-world`._**

## Containers

Containers are created by running their respective image or importing them from a file (we will discuss this later).

Whenever you use the `docker run` command on an image, a container is created. By default this container persists meaning that it and its contents are preserved and not deleted. However, in the previous `docker run` commands we used the `--rm` option that removes the container after it terminates.

If we run a container without the `--rm` option the container can be rerun even if it terminates and the contents as well as any changes made inside the container will remain between the consecutive times the container is used.

One of the most common early mistakes in Docker is that to reuse a Docker container, you should use the `docker run` command. However, this is not the case. The `docker run` command is ONLY for running an image and thus creating a container the first time. After a container is created (and possibly run the first time), you must then use the `docker start` command to rerun the container or, more accurately, restart the container. By default, starting a container starts the default command/process that was defined by the image. However, we will discuss how you can change this behavior in later tutorials.

## Helpful Analogies

- docker => VM: This is helpful at first but Docker and VMs are different in how they communicate with the host operating system (unless you are using Docker Desktop in which Docker uses a VM "under the hood")

- image => iso file

- image => VM image (what you input into the VM software to create your Virtual Machine)

- image => zipped (compressed) folder

- image => template

- image => executable/binary file

- image => answer key / exam template

- container => copy

- container => process

- container => a running VM

- container => your personal modified exam

# [Continue to Tutorial 2](./tutorial-2-practice.md)
