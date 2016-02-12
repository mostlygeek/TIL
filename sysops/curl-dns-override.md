# curl with DNS override

Testing a TLS protected web service is hard when the correct DNS hostname hasn't been pointed to it yet. Luckily [curl](https://curl.haxx.se/) has the `--resolve` flag. Combined with [dig](https://en.wikipedia.org/wiki/Dig_(command)) it is very easy to fully test TLS services without complex dns hackery.

The resolve flag looks like this: `--resolve HOST:PORT:ADDRESS  Force resolve of HOST:PORT to ADDRESS`

Using it:


```
> curl \
   --resolve mostlygeek.com:443:$(dig new.mostlygeek.com +short | head -1) \   [1]
   https://mostlygeek.com                                                      [2]
```

This is what `[1]` does: 

* uses `dig` to lookup the ip addresses for `new.mostlygeek.com`
* pops off the first line with `head`
* uses the new IP address for `mostlygeek.com` 

In `[2]`: 

* curl will load `https://mostlygeek.com`
* rather than do a regular DNS resolution it will use the IP provided in `[1]`

## Why use `dig`?

`dig` makes it easy to work with load balancers like the [AWS elastic load balancer](https://aws.amazon.com/elasticloadbalancing/) which resolves to multiple, frequently changing IP addresses. 

Instead of `new.mostlygeek.com`, it is possible to use the ELB's hostname: 

```
> curl --resolve mostlygeek.com:443:$(dig mg-elb-12345.us-west-2.elb.amazonaws.com +short | head -1) https://mostlygeek.com
```

