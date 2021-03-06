# TIL

> Today I Learned

A collection of concise write-ups on small things I learn day to day across a variety of languages and technologies. This was blatently copied from [jbranchaud/til](https://github.com/jbranchaud/til) which I discovered from this [HN post](https://news.ycombinator.com/item?id=11068902).

---
## Categories 

* [git](#git)
* [OSX](#osx)
* [puppet](#puppet)
* [sysops](#sysops)

---

## Firefox

* [manage cpu/memory with e10s](firefox/e10s-cpu-ram.md) - OSX specific

## Golang

* [Speed up vendored cgo libaries](golang/speedup-vendored-cgo-libs.md)

## Git

* [Credential cache for HTTPS auth](git/credential-cache.md) 

## Puppet

* [Using versioncmp in a conditional](puppet/versioncmp.md) 

## OS X

* [Protect against corrupt timemachine backups with ZFS on FreeNAS](osx/timemachine-zfs-freenas.md)

## SysOps

Sysadmin and operations related things

* [curl with dns override](sysops/curl-dns-override.md) - useful for testing TLS services before repointing DNS
* [make journald production ready](sysops/journald-prod-ready.md) - better settings for a production server
* [install dev tools in centos](sysops/install-dev-tools.md) -  install all necesary tools to compile things from source
* [configure docker for direct-lvm](sysops/docker-direct-lvm.md) - much faster than default loopback storage in centos7
* [FreeBSD Debugging pubkey ssh login](sysops/freebsd-ssh.md) - pubkey login failing for FreeBSD? `tail /var/log/auth.log`.  