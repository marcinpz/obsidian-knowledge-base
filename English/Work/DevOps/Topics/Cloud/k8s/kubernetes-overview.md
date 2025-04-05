# Kubernetes Overview

## What is Kubernetes?
- **Definition**: Kubernetes (K8s) is an open-source platform for automating deployment, scaling, and management of containerized applications.
- **Purpose**: Simplifies orchestration of containers, ensuring high availability, scalability, and resilience.
- **Origin**: Developed by Google, open-sourced in 2014, maintained by the Cloud Native Computing Foundation (CNCF).

## Core Concepts
- **Cluster**: A set of nodes running containerized applications managed by Kubernetes.
- **Pod**: Smallest deployable unit, containing one or more containers sharing storage/network.
- **Node**: Worker machine (physical or virtual) running Pods.
- **Control Plane**: Manages the cluster (e.g., API Server, Scheduler).
- **Workload Resources**:
  - **Deployment**: Manages stateless apps with replicas and updates.
  - **StatefulSet**: Manages stateful apps with persistent identities.
  - **DaemonSet**: Runs a Pod on every node.

## Key Features
- **Self-Healing**: Restarts failed containers, reschedules Pods, kills unresponsive ones.
- **Auto-Scaling**: Horizontal Pod Autoscaler (HPA) adjusts Pod count based on CPU/memory.
- **Service Discovery & Load Balancing**: Routes traffic to Pods automatically.
- **Storage Orchestration**: Mounts storage (local or cloud) to Pods.
- **Declarative Configuration**: Define state in YAML/JSON, applied via `kubectl`.

## Architecture
- **Control Plane Components**:
  - **API Server**: Exposes Kubernetes API, cluster control frontend.
  - **etcd**: Distributed key-value store for cluster data.
  - **Scheduler**: Assigns Pods to nodes based on resources.
  - **Controller Manager**: Runs controllers to maintain desired state.
- **Node Components**:
  - **Kubelet**: Ensures containers in Pods are running.
  - **Kube-Proxy**: Manages network rules.
  - **Container Runtime**: Runs containers (e.g., Docker, containerd).

## Basic Commands
- `kubectl get pods`: Lists all Pods.
- `kubectl apply -f file.yaml`: Applies a configuration file.
- `kubectl describe pod <pod-name>`: Shows Pod details.
- `kubectl scale deployment <name> --replicas=3`: Scales a Deployment.

---

# Ingress in Kubernetes

## What is Ingress?
- **Definition**: An API object managing external access to services, typically HTTP/HTTPS, via routing rules.
- **Purpose**: Exposes multiple services under one IP, providing load balancing, SSL termination, and virtual hosting.

## Why Use Ingress?
- Unlike a **Service** (e.g., LoadBalancer), Ingress handles multiple apps efficiently.
- Reduces need for multiple external load balancers, cutting costs.

## Components
- **Ingress Resource**: YAML file defining routing rules.
- **Ingress Controller**: Implements rules (e.g., NGINX, Traefik).
  - Must be deployed (e.g., `nginx-ingress` via Helm).
- **External Load Balancer**: Routes traffic to the controller (common in cloud setups).

## Example Ingress YAML
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /app1
        pathType: Prefix
        backend:
          service:
            name: app1-service
            port:
              number: 80
      - path: /app2
        pathType: Prefix
        backend:
          service:
            name: app2-service
            port:
              number: 80
  tls:
  - hosts:
    - example.com
    secretName: example-tls
```
- **Explanation**:
  - Routes `example.com/app1` to `app1-service`.
  - Routes `example.com/app2` to `app2-service`.
  - Enables HTTPS with `example-tls` Secret.

## How It Works
1. Traffic enters via an external IP (e.g., cloud load balancer).
2. Ingress Controller interprets rules, directs traffic to Services.
3. Services forward traffic to Pods.

## Setup Steps
1. Deploy an Ingress Controller: `helm install ingress-nginx ingress-nginx/ingress-nginx`.
2. Apply Ingress: `kubectl apply -f ingress.yaml`.
3. Verify: `kubectl get ingress`, test with `curl example.com/app1`.

## Common Use Cases
- Routing traffic to microservices by URL paths or hostnames.
- Securing apps with TLS/SSL.
- Load balancing with custom rules.

## Troubleshooting
- Check controller logs: `kubectl logs -n ingress-nginx <controller-pod>`.
- Verify rules: `kubectl describe ingress my-ingress`.
- Ensure DNS points to Ingress IP.

---

**Tags**: #Kubernetes #K8s #Ingress #DevOps #Containerization