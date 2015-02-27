# devnews-coreos
Configuration for deploying a highly avaliable and clustered [Developer News](http://devnews.today) enviroment onto a CoreOS platform

### Launch the fleet

Grab the repo:

```shell
git clone https://github.com/imjacobclark/devnews-coreos.git && devnews-coreos
```

Submit to Fleet:

```shell
fleetctl submit devnews-core@.service devnews-core-discovery@.service
```

Load and start the units, repeat for the number of units you require, replacing {port} with a unique number each time:
```
fleetctl load devnews-core@{port}.service devnews-core-discovery@{port}.service
fleetctl start devnews-core@{port}.service
```

View the IPs and Ports of each running service:
```shell
etcdctl ls --recursive /
```

Enjoy.
