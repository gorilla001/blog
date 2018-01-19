## centos 7.4 

### Install Etcd
```
yum install -y etcd
```

### Config Etcd
```
vim /etc/etcd/etcd.conf

ETCD_LISTEN_CLIENT_URLS="http://0.0.0.0:2379"

ETCD_ADVERTISE_CLIENT_URLS="http://0.0.0.0:2379"
```
### Restart Etcd
```
systemctl restart etcd
```

### Create Network
```
etcdctl --endpoint http://127.0.0.1:2379 set /flannel/network/config '{"Network":"10.0.0.0/16","SubnetLen":24,"Backend":{"Type":"vxlan","VNI":0}}'
```

### Install Flannel
```
yum install -y flannel
```

### Create Log Directory
```
mkdir /var/log/flannel
```

### Config Flannel
```
vim /etc/sysconfig/flanneld

# Flanneld configuration options  

# etcd url location.  Point this to the server where etcd runs
FLANNEL_ETCD_ENDPOINTS="http://127.0.0.1:2379"

# etcd config key.  This is the configuration key that flannel queries
# For address range assignment
FLANNEL_ETCD_PREFIX="/flannel/network"

# Any additional options that you want to pass
FLANNEL_OPTIONS="--logtostderr=false --log_dir=/var/log/flannel/"
```

### Restart Flannel
```
systemctl daemon-reload flanneld

systemctl restart flannel

systemctl enable flanneld
```

```
cat /run/flannel/subnet.env
```
```
FLANNEL_NETWORK=10.0.0.0/16
FLANNEL_SUBNET=10.0.58.1/24
FLANNEL_MTU=1450
FLANNEL_IPMASQ=false
```

```
cat /run/flannel/docker
```
```
DOCKER_OPT_BIP="--bip=10.0.58.1/24"
DOCKER_OPT_IPMASQ="--ip-masq=true"
DOCKER_OPT_MTU="--mtu=1450"
DOCKER_NETWORK_OPTIONS=" --bip=10.0.58.1/24 --ip-masq=true --mtu=1450"
```

### Config Docker
```
vim /etc/systemd/system/docker.service.d/override.conf

[Service]
ExecStart=
ExecStart=/usr/bin/dockerd $DOCKER_NETWORK_OPTIONS
```

### Restart Docker
```
systemctl daemon-reload

systemctl restart docker
```

### Test
```
docker run -it --name ip_test busybox
```


