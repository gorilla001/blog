## Environment
```
os: centos 7.4 x86_64
docker: 17.12.0-ce x86_64
```

### Create Macvlan Network
```
docker network  create  -d macvlan --subnet=192.168.0.0/16 --ip-range=192.168.2.0/24 -o macvlan_mode=bridge -o parent=enp0s3 macvlan
```

### Run Container
```
docker run --net=macvlan -it --name macvlan --rm alpine /bin/sh
```

### Make Host Connect To Container
```
sudo ip link add macvlan link enp0s3 type macvlan mode bridge
sudo ip addr add 192.168.2.10/24 dev macvlan
sudo ifconfig macvlan up
```

### Macvaln Need IPAM


[macvlan](https://sreeninet.wordpress.com/2016/05/29/docker-macvlan-and-ipvlan-network-plugins)
