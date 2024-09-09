# Docker

- Docker allows the developers to package their apps into **images** that run on **containers**.
- Docker uses images and containers to allow apps to run consistently anywhere.
- Images are created from light weight config files that describes everything that our app needs to run.

## Containers Vs VMs

- Virtual machines virtualize hardware and Containers virtualize operating system kernels

### VM

- VM run on Hypervisor bridge, the main job of hypervisor is to translate operations from emulated hardware of the VM to the real hardware of the host of the VM
- VM require OS to be installed within them before we can configure our apps.
- VMs can run multiple apps within them.
- Apps in VM cannot see apps that are hosted in the host of the VM.

### Container

- Containers run on container runtime.
- Container runtime work with the OS to allocate hardware, to copy files and directories.
- Do not require OS. Container runtime does not emulate any hardware. All containers running in the same host are using the hardware the host is using.
- Less space is required
- Can only run one app.
- Can interact with the apps running in the host.

## Anatomy of Container

- Container contains of 2 things
    - Linux namespace
    - Linux control group
- Namespaces provide different **views** of the system
    - They can make the app running on a container think it is running as a super user in hardware with access to a full file system and hardware. While its actually running in as a random user with access to only a single file system.
    - Linux supports 8 namespaces. Docker can use all the namespaces expect the time namespace.
- Control groups limits the amount of resource each process can utilize.
- Docker used control groups for
    - Monitor and restrict CPU usage of each container.
    - Monitors and restrict network and disk bandwidth
    - Monitor and restrict memory consumption of each container.

## Docker Limitations

- As namespaces and control groups are linux based functions. Docker only runs natively in linux
- Images are tied to the kernel they were created from. i.e Containers configured for linux kernels can only run on linux and conversely containers created from container images configured for windows can run only in windows.

## Docker Advantages

- Docker makes configuring container env really easy
- dockerfiles are used to tell how their containers should be configured.
- Docker uses these docker files to package the app into images.
- Docker hub is a global repository of images that helps users to share their images quickly and easily
- Docker CLI gives a easy interface to stat and manage the containers

## Docker Machine

- As docker uses control groups and namespaces which are primarily linux functionalities. Docker introduced docker machine to work resolve this issue so that docker can run in windows and mac
- Docker machine used VirtualBox to create a small VM with linux that can be used to run docker.
- This added the dependencies that developers need to learn VirtualBox to mount/unmount and exposing and connect ports

## Docker Desktop

- This runs a smaller and faster VM that runs on native hypervisor called Virtual Kit for Apple and Hyper-V for windows
- Automatically handles volume mounting and unmounting and also handles network port mapping
- Windows can run a real linux in windows from windows 10 Anniversary edition using **WSL 2** without virtualization

## Docker Containers

- Containers are created from container images. Container images are pre compressed and pre-packaged file system that contains our app and its configurations and env.
- Docker images are just layers of images compressed together.
- Docker creates an image for every command in our docker file these are called as intermediatory images. While the full build is completed it squashes all these images into a single image.


## Ways of creating an container from an image

- We can use docker container create and docker container start to create and start a container
- Another short hand approach is to use docker container run which will have the same behavior along with attaching the terminal to the docker logs

## Binding ports to container

- Port bindings can be used to interact with the applications that the containers run from the host machine. For eg. if the container services a web application to see that in the browser we need to bind the port of the container in which the container serves the page with the port of the host so that we can see the web page in the browser.
- To achieve this we can use -p flag with the pattern **"${host-port}:${container-port}"**

## Saving data from the container

- Everything that gets created inside the container stays within the container.
- Once we stop the container the all the data will be lost.
- To store the data even after the removing the container we should the volume mount feature.
- This maps a folder in out host machine to a folder inside the container.
- This follows the same pattern as **"${host-file-path}:${container-file-path}"** with the flag -v
- we can also map file to files. Any non existing file path will be considered as an directory

## Docker commands

- Docker exec can be used to execute commands in one particular container terminals or commands on a specific container
- docker stop - can be used to stop running containers. It usually takes a bit of time because its tries to gracefully stop the container. We can forcefully stop containers with the flag **-t 0**
- docker rm can be used to remove containers. This generally removes only the stopped containers. To include all the running container we can use flag **-f**
- docker rmi can be used to remove images.