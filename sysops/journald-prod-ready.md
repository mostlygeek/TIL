# Production ready journald

The default settings on a centos7 box is for `journald` to log to the ramdisk at `/run/log/journal/*`. While quite fast, it doesn't persist logs on reboot or have much space.

To have journald log to disk, edit `/etc/systemd/journald.conf` set: 

```
[journal]
...
Storage=persistent
...
``` 

Also by default journald will suppress messages from a service if they exceed the default burst limit. Losing important logs in production is bad, particularly if they feed a metrics pipeline. 

Disable message suppression:

```
RateLimitBurst=0
``` 

Setting `RateLimitBurst=0` in `/etc/systemd/journald.conf` disables suppression. Log files are automatically rotated so disk space won't be consumed unbounded. 