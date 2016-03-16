# Configure Docker for direct-lvm

Out of the box Docker on centos7 uses `loop-lvm` which is slow but just works. For production and even for container dev box it makes sense to switch to using a `direct-lvm` since it can be significantly faster. 

I run Linux in a VirtualBox VM on a FreeBSD box (I know). Here's how to configure Docker to use `direct-lvm`.

## Configuration 

- add a new disk to the machine
- determine what the new device is, e.g. `/dev/sdb`
  - `sudo fdisk -l` can help find the device
- make sure docker is not running: `systemctl stop docker`
- delete any old docker data: `sudo rm -rf /var/lib/docker`
- Create the lvm volumes
  1. `sudo pvcreate /dev/sdb`
  1. `sudo vgcreate vg-docker /dev/sdb`
  1. `sudo lvcreate -l 90%VG -n data vg-docker` - 90% of space for data
  1. `sudo lvcreate -l 10%VG -n metadata vg-docker` - 10% for metadata
- config docker to use new volumes 
  - edit `/etc/sysconfig/docker`
  - `OPTIONS='--selinux-enabled --storage-driver=devicemapper --storage-opt dm.datadev=/dev/vg-docker/data --storage-opt dm.metadatadev=/dev/vg-docker/metadata'`
- `sudo systemctl docker start`

## Make sure it works
```
[mostlygeek@localhost ~]$ sudo docker info
Containers: 0
Images: 23
Storage Driver: devicemapper
 ...
 Data file: /dev/vg-docker/data          <- \o/
 Metadata file: /dev/vg-docker/metadata  <- *it works*
 Data Space Used: 2.721 GB
 Data Space Total: 61.84 GB
 Data Space Available: 59.12 GB
 Metadata Space Used: 3.187 MB
 Metadata Space Total: 6.87 GB
 Metadata Space Available: 6.867 GB
 ...
```

The `Data file` and `Metadata file` should point to `/dev/vg-docker/...`