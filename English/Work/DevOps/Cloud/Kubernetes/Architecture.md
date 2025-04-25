# Kubernetes Architecture

Kubernetes (K8s) is an open-source container orchestration platform that automates deploying, scaling, and managing containerized applications.

## 🧠 Control Plane

The control plane manages the cluster and makes global decisions about the cluster (e.g., scheduling), and detects and responds to cluster events.

- **kube-apiserver**: Exposes the Kubernetes API. It's the front-end for the Kubernetes control plane.
- **etcd**: A consistent and highly-available key-value store used as Kubernetes' backing store for all cluster data.
- **kube-scheduler**: Assigns pods to nodes based on resource availability.
- **kube-controller-manager**: Runs controller processes that handle routine tasks in the cluster.
- **cloud-controller-manager**: Manages cloud-specific control logic like managing load balancers or storage.

## ⚙️ Node (Worker Node)

A node is a worker machine in Kubernetes. It runs containerized applications.

- **kubelet**: An agent that ensures containers are running in a pod.
- **kube-proxy**: Maintains network rules on nodes and handles traffic routing.
- **Container Runtime**: Software responsible for running containers (e.g., containerd, Docker).

## 📦 Pod

A pod is the smallest deployable unit in Kubernetes. A pod can host one or more containers with shared storage/network resources.

## 🛠 Key Resources

- **Deployment**: Manages the creation and scaling of Pods.
- **Service**: Exposes Pods via a stable network endpoint.
- **ConfigMap / Secret**: Used for injecting configuration data or sensitive info.
- **Namespace**: Supports multiple virtual clusters within the same physical cluster.

## Diagram

![[resources/kubernetes-architecture.png]]