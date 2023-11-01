# Tutorial 0: Installation

Before installing Docker we should understand the difference between two different installs available:

- [Docker Desktop](https://docs.docker.com/desktop/)
- [Docker Engine](https://docs.docker.com/engine/)

Docker Desktop is a version of Docker meant to be used on Desktops/Laptops which have graphical user interfaces or GUIs. In general, Docker Desktop is more user friendly and typically helps new users of Docker to understand the basics without touching the command line. Keep in mind that the implementations of Docker on Desktop/Laptop operating systems use virtual machines or VMs to operate. This may cause slower container performance compared to native installs.

Docker Engine can be considered the 'brains' behind Docker with most of the functionality of Docker Desktop, just minus the GUI and some of the 'conveniences'. Docker Engine alone without the GUI and VM middleware tends to run applications faster since the containers do not have to communicate through a hypervisor.

Regardless of the version of Docker you choose to install, you should be able to follow this tutorial. However, keep in mind most of this tutorial will be focused on the command line aspect of Docker instead of using the GUI included with Docker Desktop. Understanding the command line interface or CLI for Docker will sufficiently prepare you to use most of the available features included in the GUI.

Typically, the OS you are using decides which version of Docker you get. If you are running a **_Windows or MacOS_** computer you will need to install `Docker Desktop`. While there is a version of Docker Desktop for Linux, working with Docker Engine on Linux is typically more simplistic, minimal, and performant.

## Docker Desktop Installation (Windows/MacOS):

**_Recommended for Windows or MacOS_**

**_WINDOWS USERS: You will need setup Windows Subsystem for Linux (WSL) 2 to properly use Docker on Windows. See the install documentation [here](https://learn.microsoft.com/en-us/windows/wsl/install) for details on setting up WSL and the Docker setup documentation [here](https://docs.docker.com/desktop/install/windows-install/)._**

**_MAC USERS: If you are using an M-Series CPU Mac (i.e. with an ARM CPU) you will need to install the Rosetta translation software prior to installing using `softwareupdate --install-rosetta` in the command line._**

To install Docker Desktop download the Docker Desktop installer from Docker's website:

https://www.docker.com/products/docker-desktop/

Once you download the installer simply follow your respective operating system's instructions:

- [Windows](https://docs.docker.com/desktop/install/windows-install/)
- [MacOS](https://docs.docker.com/desktop/install/mac-install/)
- [Linux (Docker Engine Recommended)](https://docs.docker.com/desktop/install/linux-install/)

## Docker Engine Installation (Linux ONLY):

**_Recommended for Linux_**

Installing Docker Engine via the command line is a bit of a lengthy process but this process typically allows you to update Docker via your Linux distribution package manager like `apt` on Debian distros. We will break it down command-by-command here for Ubuntu (for other distros click [here](https://docs.docker.com/engine/install/) and select your distro under `Server`):

1. Open a terminal on your Linux computer.

2. Remove any current installs of Docker-related packages installed via your package manager:

   ```shell
   for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
   ```

   This will remove the following packages if they are installed:

   - docker.io
   - docker-compose
   - docker-compose-v2
   - docker-doc
   - podman-docker

   Additionally run the following two commands to purge all Docker related leftover files from your system:

   ```shell
   sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
   sudo rm -rf /var/lib/docker
   sudo rm -rf /var/lib/containerd
   ```

3. Run the following command to update your package manager's package repositories:

   ```shell
   sudo apt update
   ```

4. Install a couple packages so that we can perform the next steps. These packages are typically installed by default in Ubuntu and help with storing certificates for trusted software sources:

   ```shell
   sudo apt install ca-certificates curl gnupg
   ```

5. Set the permission of the `/etc/apt/keyrings` directory to `rwxr-xr-x` (i.e. all permissions for the root, read and execute for group and everyone else):

   ```shell
   sudo install -m 0755 -d /etc/apt/keyrings

   ```

6. Download the Docker gpg key and store it in `/etc/apt/keyrings` so that we can update/install Docker via the package manager:

   ```shell
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
   ```

7. Change the permissions of the newly downloaded and stored Docker repository key to allow anyone to read the file:

   ```shell
   sudo chmod a+r /etc/apt/keyrings/docker.gpg
   ```

8. Add the key package manager's repo sources list so that apt can find the Docker sources:

   ```shell
        echo \
           "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
           "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
        sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```

9. Update the package manager's repo list:

   ```shell
   sudo apt update
   ```

10. Install Docker and its components:
    ```shell
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```

If all goes well, Docker should be installed and you should be able to run `docker run --rm hello-world` which results in the following:

```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
719385e32844: Pull complete
Digest: sha256:88ec0acaa3ec199d3b7eaf73588f4518c25f9d34f58ce9a0df68429c5af48e8d
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

### Post Install Steps (Optional)

While Docker will work completely fine without using the following instructions, they will make using Docker a bit more simpler by allowing you to run the `docker` command without using `sudo`. Keep in mind this consideration documented by Docker [here](https://docs.docker.com/engine/install/linux-postinstall/):

```
The docker group grants root-level privileges to the user. For details on how this impacts security in your system, see Docker Daemon Attack Surface.
```

1. Create the `docker` group if it has not already been created:

   ```shell
   sudo groupadd docker
   ```

2. Add your user to the group:

   ```shell
   sudo usermod -aG docker $USER
   ```

3. Log out and back in or simply reboot your computer. You can also run `newgrp docker` bypass the logout/reboot process.

4. Test running the `hello-world` image again without using `sudo` to confirm it works:
   ```shell
   docker run --rm hello-world
   ```

If you run into any issue refer to the following documentation by Docker:

https://docs.docker.com/engine/install/linux-postinstall/

### Enable Docker on Computer Startup

To enable Docker on startup use the typical `systemd` commands:

```shell
sudo systemctl enable docker.service
sudo systemctl enable docker.socket
sudo systemctl enable containerd.service
```

# [Continue to Tutorial 1](./tutorial-1-terminology.md)
