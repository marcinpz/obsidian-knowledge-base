# Kubernetes StatefulSet

## Overview

A StatefulSet is a Kubernetes controller used to manage stateful applications. Unlike Deployments, StatefulSets maintain a unique identity for each Pod and provide guarantees about the ordering and uniqueness of these Pods.

## Key Features

- **Stable, unique network identity**
    
- **Stable, persistent storage** (via PersistentVolumeClaim)
    
- **Ordered deployment and scaling**
    
- **Ordered, graceful deletion and termination**
    

## Use Cases

- Databases (e.g., MySQL, PostgreSQL)
    
- Distributed systems (e.g., Kafka, Cassandra)
    
- Any service requiring stable network identity and storage
    

## Pod Naming

Pods in a StatefulSet have a predictable naming convention:

```
<statefulset-name>-<ordinal>
```

Example: `web-0`, `web-1`, `web-2`

## Volume Claim Templates

StatefulSets use volumeClaimTemplates to provide stable storage for each pod.

```yaml
volumeClaimTemplates:
- metadata:
    name: data
  spec:
    accessModes: [ "ReadWriteOnce" ]
    resources:
      requests:
        storage: 1Gi
```

Each pod gets its own [[PersistentVolumeClaim]].

## Example YAML

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web
spec:
  serviceName: "web"
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
  volumeClaimTemplates:
  - metadata:
      name: www
    spec:
      accessModes: ["ReadWriteOnce"]
      resources:
        requests:
          storage: 1Gi
```

## Headless Service Requirement

StatefulSets require a **headless service** to work properly:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: web
spec:
  clusterIP: None
  selector:
    app: nginx
  ports:
  - port: 80
    name: web
```

## Lifecycle Guarantees

- Pods are created in order: `web-0` → `web-1` → `web-2`
    
- Pods are terminated in reverse order
    
- Restarts maintain identity and volume binding
    

## Tips

- Don’t use StatefulSet if your application doesn’t need persistent identity or storage
    
- Use `PodDisruptionBudget` for availability guarantees
    
- Combine with `initContainers` for data initialization
    

## Limitations

- Rolling updates are slower due to ordered pod management
    
- Requires a headless service and stable DNS setup
    
- Deleting a StatefulSet doesn’t delete PVCs by default
    

## Cleanup

To fully remove a StatefulSet and its volumes:

```bash
kubectl delete statefulset <name>
kubectl delete pvc -l app=<label>
```

---

**References**:

- [https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)
    
- [https://kubernetes.io/docs/tutorials/stateful-application/basic-stateful-set/](https://kubernetes.io/docs/tutorials/stateful-application/basic-stateful-set/)