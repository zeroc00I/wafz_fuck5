## AWS BLOCK IP RANGE

https://github.com/corbanworks/aws-blocker

## Rate limiting per IP

https://blog.programster.org/rate-limit-requests-with-iptables#:~:text=You%20can%20rate%20limit%20connections,of%20connection%2C%20based%20on%20port.
```
#!/bin/bash
IPT=/sbin/iptables
# Max connection in seconds
TIME_PERIOD=100
# Max connections per IP
BLOCKCOUNT=100

# default action can be DROP or REJECT
DACTION="DROP"
$IPT -A INPUT -p tcp --dport 80 -i eth0 -m state --state NEW -m recent --set
$IPT -A INPUT -p tcp --dport 80 -i eth0 -m state --state NEW -m recent --update --seconds $TIME_PERIOD --hitcount $BLOCKCOUNT -j $DACTION

$IPT -A INPUT -p tcp --dport 443 -i eth0 -m state --state NEW -m recent --set
$IPT -A INPUT -p tcp --dport 443 -i eth0 -m state --state NEW -m recent --update --seconds $TIME_PERIOD --hitcount $BLOCKCOUNT -j $DACTION
```
