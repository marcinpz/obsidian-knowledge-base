# Kubernetes Application Scaling

Scaling applications in Kubernetes means adjusting the number of pods running to match demand. There are three main types of scaling:

---

## 1. Manual Scaling

You can manually set the number of replicas using `kubectl` or by editing the manifest.

### Example with kubectl:

```bash
kubectl scale deployment <deployment-name> --replicas=5
```

### Example in YAML:

```yaml
spec:
  replicas: 5
```

---

## 2. Horizontal Pod Autoscaler (HPA)

HPA automatically adjusts the number of pod replicas based on metrics like CPU or memory usage.

### Quick setup using CPU utilization:

```bash
kubectl autoscale deployment <deployment-name> --cpu-percent=50 --min=2 --max=10
```

### YAML example:

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: example-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-app
  minReplicas: 2
  maxReplicas: 10
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 50
```

📌 **Note:** HPA requires metrics-server to be installed and running in the cluster.

---

## 3. Vertical Pod Autoscaler (VPA)

VPA adjusts CPU and memory requests/limits of pods. It typically restarts the pods to apply changes.

### Use cases:

- Long-running workloads with stable usage
    
- Optimizing resource requests for cost efficiency
    

---

## 4. Cluster Autoscaler

This scales the number of **nodes** in the cluster, especially useful when HPA cannot schedule new pods due to resource constraints.

- Works with cloud providers like GCP, AWS, and Azure.
    
- Reacts to unschedulable pods or underutilized nodes.
    

---

## Summary

|Scaling Type|What it Adjusts|Typical Use Case|
|---|---|---|
|Manual|Pod replicas|Quick control, testing|
|HPA|Pod replicas|Varying traffic/load|
|VPA|CPU/Memory resources|Optimize resource allocation|
|Cluster Autoscaler|Node count|Ensure cluster can meet demands|

---

Do you want to include custom metrics scaling with Prometheus or KEDA in the note?