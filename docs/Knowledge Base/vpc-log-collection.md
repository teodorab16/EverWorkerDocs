---
title: How to collect detailed logs from VPC setup
excerpt: >-
  This article explains the proccess that allows to collect logging from all
  kubernetes pod replicas
deprecated: false
hidden: true
icon: fad fa-rocket-launch
metadata:
  robots: index
---
# Setting the log level

Increase the log level by changing the environment variable EW_OBSERVATORY__LOG_LEVEL to DEBUG in 'values.yaml'.

Reproduce the error after the change.

# Collecting the logs

<br />

1. Find the Deployment's pod label selector (copy the matchLabels)

```
kubectl -n everworker get deploy everworker -o jsonpath='{.spec.selector.matchLabels}{"\n"}
```

2. Use those labels to pull logs from ALL pods (all replicas)  
   _Example if you saw: `{"app":"everworker"`}_

```
kubectl -n everworker logs -l app=everworker --all-containers --prefix=true --timestamps=true
```

3. Save to a file

```
kubectl -n everworker logs -l app=everworker --all-containers --prefix=true --timestamps=true > everworker.log
```

4. If pods restart, also capture the "previous" logs (per pod)  
   _(kubectl can't do --previous with -l selector, so loop pods)_

```Text
for p in $(kubectl -n everworker get pods -l app=everworker -o name); do
  kubectl -n everworker logs ${p#pod/} --all-containers --prefix=true --timestamps=true --previous \
    > "everworker_${p#pod/}_previous.log" 2>&1 || true
```

<br />
