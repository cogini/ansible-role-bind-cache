# bind-cache

Install a caching / forwarding name server using bind9.

When your app is acting as a proxy to back end servers, it it may need to do
a DNS lookup to convert the host name of the server into an IP hundreds of
times a second. DNS can become the bottleneck for requests. It also puts heavy
load on hosting provider DNS servers, which may not be able to take it, or they
may get unhappy with you. Hard coding IPs of back end servers is dangerous, as
they may change over time.

Running a local caching DNS server on the app server machine caches results of
DNS lookups to make them fast and reduce load on external DNS servers.

The local DNS server forwards requests to the upstream DNS servers and caches
the results.

# Role Variables

The `bind_cache_upstream_dns_servers` variable sets the upstream DNS servers.

By default, this role Google's DNS servers.

```yaml
bind_cache_upstream_dns_servers:
    - 8.8.8.8
    - 8.8.4.4
```

You can set it to the upstream DNS servers for your hosting provider.

You should also configure `/etc/resolv.conf` to specify the caching DNS first,
followed by your upstream DNS servers:

    nameserver 127.0.0.1
    nameserver 8.8.8.8
    nameserver 8.8.4.4

# Example Playbook

```yaml
- hosts: '*'
  roles:
     - cogini.bind_cache
```

# License

MIT

# Author Information

Jake Morrison at [Cogini](http://www.cogini.com/)
