





## 2025-01-18

In order to figure out AI deployment in helm chart.

```shell
➜  tools helm show values lgame-online-service-v0.1.0-10.tgz --version v0.1.16
# Default values for lgame_online_service.
# This is a YAML-formatted file.
# Declare variables to be passed into your templates.

replicaCount: 1
replicaCountLast: 1
terminationGracePeriodSeconds: 3600
...

helm list
helm list -a
helm history {release-name}

helm get manifest {release-name}
helm get values {release-name}
helm get all {}

helm status {}
```



