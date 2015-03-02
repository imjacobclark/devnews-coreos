# devnews-coreos
Configuration for deploying a highly avaliable and clustered [Developer News](http://devnews.today) enviroment onto a CoreOS platform

### Launch the fleet

Grab the repo:

```shell
git clone https://github.com/imjacobclark/devnews-coreos.git && devnews-coreos
```

Launch the static loadbalancer:

```shell
cd fleet/statics && fleetctl start devnews-core-loadbalancer.service
```

Submit templates to Fleet:

```shell
cd fleet/templates && fleetctl submit devnews-core@.service devnews-core-discovery@.service
```

Load and start the units:
```
cd fleet/instances && fleetctl start *
```

To add more units to your cluster, replacing {port} with a port number not currently in use by devnews-core:

```
cd fleet/templates && ln -s devnews-core@.service devnews-core@{port}.service && ln -s devnews-core-discovery@.service devnews-core-discovery@{port}.service
```

View the IPs and Ports of each running service:
```shell
etcdctl ls --recursive /
```

Enjoy.
