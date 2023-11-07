# Tutorial 2: Practicing Managing Images/Containers

Similar to managing your operating systems files and directories, you will need to manage your Docker images and containers. Here we will walk through how to view/list the images and containers that are located on your machine.

## Images

1. Run the `hello-world` image again.

   ```shell
   docker run hello-world
   ```

2. You should see the `hello-world` output from before and this time, if you didn't delete the image, the image didn't need to be downloaded.

3. Run the following command to list the images located on your computer:

   ```shell
   docker images # a nice alias for this could be dils
   ```

4. You should see the following output (or similar):

   ```
   REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
   hello-world   latest    9c7a54a9a43c   6 months ago   13.3kB
   ```

5. This gives us several fields of information. The first is the repository name. In this case the repository name is `hello-world` i.e. the name of the image but you may also see something like `dockerhub-username/image-name` indicating the repository's owner and the image's name. If you wish to launch a container owned by someone else you simply run it like:

   ```shell
   docker run dockerhub-username/image-name
   ```

6. The next field is the tag. This can be used like a version number or branch in `git`. It is typically used to signify a different image. The images that differ by their TAG value are typically different versions of the same software. However, some repos may choose to use the TAG to signify the image has a different underlying operating system or etc. We will investigate this in more detail later, but be sure to pay close attention to the TAG when you download and run images. You can specify a specific tag of an image using a colon after the owner and image name in `dockerhub-username/image-name`. For example:

   ```shell
   # Using pull
   docker pull dockerhub-username/image-name:TAG
   # OR using docker run
   docker run dockerhub-username/image-name:TAG
   ```

7. The next field is the image id. This ID is used to identify the Docker image. Each image with a distinct tag is assigned a different id. You can use this ID in many places where the you would normally use the Docker image's name. For example:

   ```shell
   # Instead of running docker run hello-world we can use the id
   docker run a88e16c330cf
   ```

   This is not the necessarily the only command that can use the image id in place of the image name, but some commands do not allow the usage of the image id (i.e. `docker pull`).

8. The created field simply shows when the image was originally created.

9. Finally, the last field is the SIZE of the image. This is how much disk space the Docker image is using on the computer's disk drive.

10. If you want to remove an image you can do so by providing the `docker rmi` or `docker image rm` command with the images' names or ids. For example:

    ```shell
    docker rmi hello-world
    docker image rm a88e16c330cf
    ```

    These commands are equivalent, but one is just shorter than the other. An even shorter alias that you can create for the command is `drmi`.

## Containers

So far, we have only dealt with images in this tutorial. To use an image, we need to run an instance of it which will create a container. To do this with the `hello-world` container we can either:

- Create the container from the image without running it OR
- Create the container and run it in the same command

1. To create a container without running it use:

   ```shell
   docker create hello-world
   ```

2. Now we can check that the container was created by running the following command:

   ```shell
   docker container ls -a
   ```

   A good alias for this VERY long command would be the much simpler `dcls`.

3. You should output similar to the following:

   ```
   CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS    PORTS     NAMES
   0c53d790475d   hello-world   "/hello"   11 minutes ago   Created             distracted_boyd
   ```

4. We can see the output from `docker container ls -a` looks similar to the `docker images` command but not exactly. We can see that each container is provided with a CONTAINER ID which differs from the IMAGE ID. We can also see that the container is an instance of the `hello-world` image. The command which the container run's by default is `/hello`. We can also see that the STATUS is set to created (i.e. meaning the container exists but has not been executed). If we specified any network ports to be mapped (more on this later), we would see them under the PORTS field. Finally, notice that a name has been assigned for our container. In my case the container was named `distracted_boyd`. This was randomly chosen by Docker for simplifying working with the container versus working with the container ID. What if we want a different name? Continue!

5. To set the name of your Docker container you can simply use the `--name` option when you create or run the container for the first time. For example, using the run command:

   ```shell
   docker run --name howdy hello-world
   ```

   Since we used the `docker run` command this time, you will see the `hello-world` image's output like we have already seen several times before.

6. Now re-run the `docker container ls -a` command. You should see a similar output to the following:

   ```shell
   CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                     PORTS     NAMES
   29dda4d87a7c   hello-world   "/hello"   3 seconds ago    Exited (0) 2 seconds ago             howdy
   0c53d790475d   hello-world   "/hello"   22 minutes ago   Created                              distracted_boyd
   ```

7. Now we can see that a new container was created named `howdy` and it has a different CONTAINER ID, CREATED time, and a different STATUS. In this case, we created and ran the container using the `docker run` command. We can see that the STATUS indicates that the container ran the program that it was meant to run, in this case the `/hello` program, and exited/terminated. This means that the container is no longer running.

8. What if we want to run the container that we created with the `docker create` command earlier? Well, we cannot use the `docker run` since it creates a new container. Thus we must use a new command i.e. the `docker start` command along with the container's name or id:

   ```shell
   docker start <container-name-or-id>
   ```

   If you ran this command you would notice that it just prints the name/id of the container. Whoa! What happened? This is because after the container is created, it does not know where to direct STDOUT and STDERR. By default, the `docker run` command prints STDOUT/STDERR to the terminal the first time the container is run. As an optional exercise try starting the `howdy` container. You will see that starting the `howdy` container results in the same behavior as the exhibited by starting the container we created via `docker create`.

9. So how do we get the container(s) to print the output of the `/hello` program like we have seen before? We need to `attach` the the terminal to the container's STDOUT and STDERR using the `-a` or `--attach` option with `docker start`:

   ```shell
   docker start -a <container-name-or-id>
   ```

   Now we are golden! You should see the this results in what we expected and the `/hello` program's output is dumped to the terminal.

# [Continue to Tutorial 3](./tutorial-2-practice.md)
