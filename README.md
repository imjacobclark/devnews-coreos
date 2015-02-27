# devnews-coreos
Configuration for deploying a highly avaliable and clustered [Developer News](http://devnews.today) enviroment onto a CoreOS platform

### Launch the fleet

```shell
fleetctl submit devnews-core@.service devnews-core-discovery@.service
fleetctl load devnews-core@{port}.service devnews-core-discovery@{port{.service
fleetctl start devnews-core@{port}.service
```
