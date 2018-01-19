### Centos 7.4

### Install Weave
```
wget https://github.com/weaveworks/weave/releases/download/v2.1.3/weave -O /usr/local/bin/

chmod +x /usr/local/bin/weave
```

### Modifiy Iptables

```
WARNING: existing iptables rule

    '-A FORWARD -j REJECT --reject-with icmp-host-prohibited'

will block name resolution via weaveDNS - please reconfigure your firewall.

/sbin/iptables -D FORWARD -j REJECT --reject-with icmp-host-prohibited
/sbin/iptables -D INPUT -j REJECT --reject-with icmp-host-prohibited

```
[issue](https://github.com/weaveworks/weave/issues/2192)

### Launch Weave

```
weave launch [host]

weave launch: will launch weave on localhost

weave launch host: will launch weave on localhost and connect to weave on host
```

