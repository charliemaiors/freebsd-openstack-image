# FreeBSD Openstack Image
This repository provides the base files for build your own FreeBSD image for Openstack using normal build system (using GENERIC kernel) and [CLOUDWARE](https://www.freebsd.org/cgi/man.cgi?release(7)).

## Requirements

The only requirements are the ```src```(source) component installed and ```net/py-python-openstackclient``` port (for image upload)

## Instructions

In order to build your Openstack FreeBSD image please download the archive from the release page, and extract it in the ```/usr/src/release/``` folder. Then follow these instructions:

1. Fetch the archive ```fetch <latest-release-url>```
2. Extract the archive ```tar -C /usr/src/release -xvf openstack.tar.xz```
3. Move the src folder (```cd /usr/src```)
4. Build the userland and the kernel ```make buildworld buildkernel```
5. Move to the release folder ```cd /usr/src/release```
6. Run ```make cloudware-release WITH_CLOUDWARE=yes CLOUDWARE=OPENSTACK```