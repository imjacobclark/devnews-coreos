# devnews-coreos
Configuration for deploying a highly avaliable and clustered [Developer News API](http://api.devnews.today) enviroment onto a CoreOS platform

### Requirements

- 3 node minimum CoreOS cluster

### Launch the fleet

Grab the repo:

```shell
git clone https://github.com/imjacobclark/devnews-coreos.git && devnews-coreos
```

Launch the static loadbalancer:

```shell
fleetctl start fleet/statics/devnews-core-loadbalancer.service
```

Submit templates to Fleet:

```shell
fleetctl submit fleet/templates/devnews-core@.service fleet/templates/devnews-core-discovery@.service
```

Load and start the units:

```shell
fleetctl start fleet/instances*
```

To add more units to your cluster, replacing {port} with a port number not currently in use by devnews-core:

```shell
ln -s fleet/templates/devnews-core@.service fleet/instances/devnews-core@{port}.service && ln -s fleet/templates/devnews-core-discovery@.service fleet/instances/devnews-core-discovery@{port}.service
```

View the IPs of each running service:

```shell
etcdctl ls --recursive /services/devnews-core
```
View the IPs and Ports of each running service, replacing {ip} with a returned IP from the previous command:

```shell
etcdctl get /services/devnews-core/{ip}
```

Enjoy.
