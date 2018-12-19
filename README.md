# FreeBSD Openstack Image
This repository provides the base files for build your own FreeBSD image for Openstack using normal build system (using GENERIC kernel) and [CLOUDWARE](https://www.freebsd.org/cgi/man.cgi?release(7)).

## License
License BSD

## Requirements

The only requirements are the ```src```(source) component installed and ```net/py-python-openstackclient``` port (for image upload).
Source or define also the variables for openstack upload:

* **OS_USERNAME**: Your Openstack username.
* **OS_PASSWORD**: Your Openstack password.
* **OS_AUTH_URL**: The auth URL for Keystone    
* **OS_PROJECT_NAME**: The old fashion tenant name
* **OS_USER_DOMAIN_NAME**: The user domain name (only for Keystone v3)
* **OS_PROJECT_DOMAIN_NAME**: The Project domain name (only for Keystone v3)
* **OS_IDENTITY_API_VERSION**: Keystone Identity API version

## Instructions

In order to build your Openstack FreeBSD image please download the archive from the release page, and extract it in the ```/usr/src/release/``` folder. Then follow these instructions:

1. Fetch the archive ```fetch <latest-release-url>```
2. Extract the archive ```tar -C /usr/src/release -xvf openstack.tar.xz```
3. Move the src folder (```cd /usr/src```)
4. Build the userland and the kernel ```make buildworld buildkernel```
5. Move to the release folder ```cd /usr/src/release```
6. Run ```make cloudware-release WITH_CLOUDWARE=yes CLOUDWARE=OPENSTACK```
7. Run ```make openstack-upload``` to upload (and also install the port if missing) the image to your openstack cluster.

## FreeBSD Versions

Tested on:

* FreeBSD 11.x
* FreeBSD 12.0

## Known Issues

* No logs available in Horizon (tested with rsyslog and syslog)
* No Python at default (add ```python``` to ```VM_EXTRA_PACKAGES``` in ```tools/openstack.conf```), if you are planning to manage it with ansible do not forget to use ```ansible_python_interpreter=/usr/local/bin/python2.7``` to your inventory.

## Notes

* ZFS Module is present in the kernel, could be loaded using ```kldload zfs```
