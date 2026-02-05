---
title: VPC log collection
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

Increase the log level by changing the environment variable EW_OBSERVATORY__LOG_LEVEL to DEBUG

# Collecting the logs

1. Find the Deployment's pod label selector (copy the matchLabels)
2. Use those labels to pull logs from ALL pods (all replicas)  
   Example if you saw: `{"app":"everworker"`}

<br />
