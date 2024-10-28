# HA PostgresSQL CloudNativePG for Kubernetes HA
Cloud-Native PostgresSQL Kubernetes Operator CloudNativePg HA 

## Provisioning CloudNativePG using GitOps Workflows
In-Progress
### Provisioning CloudNativePG using ArgoCD ApplicationSets
In-Progress

### Provisioning CloudNativePG using FluxCD
In-Progress
### Provisioning CloudNativePG using Crossplane and ArgoCD
In-Progress
### Provisioning CloudNativePG using Crossplane and FluxCD
In-Progress

## CloudNativePG Cluster CR for HA Failover No-Data Loss 

```Yaml
apiVersion: postgresql.cnpg.io/v1
kind: Cluster
metadata:
  name: crypto-exh-postgresql-cluster
spec:
  instances: 3
  primaryUpdateMethod: switchover
  synchronousMode: true
  synchronousReplicaCount: 1  # Ensures at least one synchronous replica
  enableSuperuserAccess: true
  bootstrap:
    initdb:
      dataChecksums: true
  postgresql:
    parameters:
      synchronous_standby_names: '1 (crypto-exh-postgresql-cluster-replica-1)'  # Designate one synchronous replica
      wal_level: replica
      max_wal_senders: 10
      wal_keep_size: 64MB
  resources:
    requests:
      cpu: "500m"
      memory: "1Gi"
```
