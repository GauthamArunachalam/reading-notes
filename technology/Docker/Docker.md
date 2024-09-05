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
