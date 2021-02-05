# Basic Docker VM

This is a basic Docker VM for development purposes.

## Prerequisites

You must have the following installed on your system:
- VirtualBox - https://www.virtualbox.org/wiki/Downloads
- VirtualBox Extension Pack - https://www.virtualbox.org/wiki/Downloads
- Vagrant - https://www.vagrantup.com/downloads

## Configuration

You can change several default settings by creating `config.yml` file. 

Use the `sample-config.yml` as a template.

## Host binaries

You can use Docker in this VM directly from your host system.

To do this, you need to download the client binaries and put them on your PATH:
- Docker (you only need the docker binary, not the full installation)
  - Mac - https://download.docker.com/mac/static/stable/x86_64
  - Linux - https://download.docker.com/linux/static/stable
  - Windows - https://download.docker.com/win/static/stable/x86_64
- Docker Compose - https://github.com/docker/compose/releases

You must also define the following environment variable:
```
export DOCKER_HOST='tcp://192.168.99.10:2375'
```

### File sharing

You can map files and folders on your host system to Docker containers as long as the path you are working with is within the VM's shared folder path, which by default is your home directory.

It is required because Docker Engine actually looks for the files on the system it is running on. In this case, it is the VM. To make the sharing from the host system work, this setup shares your home directory or some other directory of your choice with the VM at the same path.

## Usage

Just run the following command and wait until it completes:
```
vagrant up
```