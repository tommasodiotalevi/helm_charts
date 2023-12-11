## HTCONDOR Helm Chart

### Values

```yaml
# Default values for htcondor.
# This is a YAML-formatted file.
# Declare variables to be passed into your templates.

cluster:
  secret: <shared secret here>

schedd: 
  mapfile: |
    SCITOKENS https://dodas-iam.cloud.cnaf.infn.it/ dodas@users.htcondor.org
    PASSWORD (*.) condor
    GSI (.*) anonymous
  extraconfig: ""
  hostname: localhost
  service:
    type: NodePort
    nodePort: 31618
    targetPort: 31618
  image:
    name: htcondor/submit
    tag:  "8.9.9-el7"
    pullPolicy: InNotPresent
  persistence:
    spooldir:
      enabled: true
      storageClass: longhorn
      size: <storage_size> 
  requests:
    memory: "500M"
    cpu: "100m" 

master:
  publicIP: <master public IP>
  extraconfig: ""
  hostname: localhost
  service:
    type: NodePort
    nodePort: 30618
    targetPort: 30618
  image:
    name: htcondor/cm
    tag:  "8.9.9-el7"
    pullPolicy: InNotPresent
  requests:
    memory: "500M"
    cpu: "100m" 

wn:
  replicas: 1
  image:
    name:  ttedesch/htcondor-execute
    tag:  "root-tokensv2"
    pullPolicy: InNotPresent
  slotType:
  requests:
    memory: "500M"
    cpu: "100m" 

htcClient:
  enabled: false
  image:
    name: htcondor/execute
    pullPolicy: InNotPresent
    tag: "8.9.9-el7"

prometheusExporter:
  image:  
    name: ttedesch/htcondor-exporter
    pullPolicy: InNotPresent
    tag: "v2"

autoscaling:
  enabled: false
  minReplicas: 1
  maxReplicas: 10
  targetMetric: condor_slot_activity_busy
  targetMetricValue: 0.75
```
