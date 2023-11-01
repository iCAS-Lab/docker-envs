# Tutorial 2: Practicing Managing Images/Containers

Similar to managing your operating systems files and directories, you will to manage your Docker images and containers. Here we will walk through how to view/list the images and containers that are located on your machine.

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

4. You should see the following output:

   ```
   REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
   hello-world   latest    9c7a54a9a43c   6 months ago   13.3kB
   ```

5. This gives us several fields of information. The first is the repository name. In this case the repository name is `hello-world` i.e. the name of the image but you may also see something like `dockerhub-username/image-name` indicating the repository's owner and the image's name. If you wish to launch a container owned by someone else you simply run it like:

   ```shell
   docker run dockerhub-username/image-name
   ```

6. The next field is the tag. This can be used like a version number or branch in `git`. It is typically used to signify a different image. Pay close attention to the TAG when you download and run images. You can specify a specific tag of an image using a colon after the owner and image name in `dockerhub-username/image-name`. For example:

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

   This is not the only command that can use the image id in place of the image name, but some commands do not allow the usage of the image id (i.e. `docker pull`).

8. The created field simply shows when the image was originally created.

9. Finally, the last field is the SIZE of the image. This is how much disk space the Docker image is using on the computer's disk drive.
