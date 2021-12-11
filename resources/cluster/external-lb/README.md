### HAProxy

**Allow HAProxy to bind to non-local IP addresses when using Keepalived VIP**

```shell
net.ipv4.ip_nonlocal_bind = 1
net.ipv6.ip_nonlocal_bind = 1
```

### References

- HAProxy : https://www.haproxy.com/
- Keepalived : https://github.com/acassen/keepalived
