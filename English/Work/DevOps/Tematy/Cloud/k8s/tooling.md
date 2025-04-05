# Common Kubernetes Tools

## 1. Helm
- **What is it?**: A package manager for Kubernetes, often called the "Kubernetes apt-get/yum."
- **Purpose**: Simplifies deployment and management of applications using pre-configured "charts."
- **Key Features**:
  - **Charts**: Reusable templates for Kubernetes resources (e.g., Deployments, Services).
  - **Releases**: Manages installed instances of charts.
  - **Versioning**: Tracks and rolls back changes.
- **Installation**:
  1. Install Helm: [official guide](https://helm.sh/docs/intro/install/).
  2. Add a repository: `helm repo add bitnami https://charts.bitnami.com/bitnami`.
  3. Update repos: `helm repo update`.
- **Basic Commands**:
  - Install a chart: `helm install my-release bitnami/nginx`.
  - Upgrade: `helm upgrade my-release bitnami/nginx`.
  - Rollback: `helm rollback my-release 1`.
  - List releases: `helm list`.
- **Use Case**: Deploy complex apps (e.g., WordPress) with one command instead of multiple YAML files.

## 2. Minikube
- **What is it?**: A tool to run a single-node Kubernetes cluster locally.
- **Purpose**: Ideal for learning, testing, and development.
- **Key Features**:
  - Supports most Kubernetes features (e.g., Ingress, Dashboard).
  - Runs on VirtualBox, Docker, or other hypervisors.
- **Installation**:
  1. Install Minikube: [official guide](https://minikube.sigs.k8s.io/docs/start/).
  2. Start cluster: `minikube start`.
  3. Access Dashboard: `minikube dashboard`.
- **Basic Commands**:
  - Check status: `minikube status`.
  - Stop: `minikube stop`.
  - Delete: `minikube delete`.
- **Use Case**: Test Kubernetes manifests locally before deploying to production.

## 3. kubectl
- **What is it?**: The command-line tool for interacting with Kubernetes clusters.
- **Purpose**: Primary interface for managing Pods, Services, Deployments, etc.
- **Installation**: [official guide](https://kubernetes.io/docs/tasks/tools/).
- **Basic Commands**:
  - `kubectl get pods`: List Pods.
  - `kubectl apply -f file.yaml`: Apply a configuration.
  - `kubectl delete pod <name>`: Delete a Pod.
  - `kubectl logs <pod-name>`: View container logs.
- **Use Case**: Essential for all Kubernetes operations, from debugging to scaling.

## 4. Kustomize
- **What is it?**: A tool for customizing Kubernetes YAML configurations without templates.
- **Purpose**: Manages variations of manifests (e.g., dev vs. prod) using overlays.
- **Key Features**:
  - Built into `kubectl` (since v1.14).
  - No external dependencies.
- **Usage**:
  1. Create a base YAML (e.g., `deployment.yaml`).
  2. Add an overlay: `kustomization.yaml`.
  3. Apply: `kubectl apply -k ./overlay-dir/`.
- **Example `kustomization.yaml`**:
  ```yaml
  resources:
  - ../base
  patches:
  - path: patch.yaml
    target:
      kind: Deployment
  ```
- **Use Case**: Customize a base app config for different environments.

## 5. Kind (Kubernetes IN Docker)
- **What is it?**: Runs Kubernetes clusters inside Docker containers.
- **Purpose**: Fast setup for multi-node testing, especially in CI/CD pipelines.
- **Installation**:
  1. Install Kind: [official guide](https://kind.sigs.k8s.io/docs/user/quick-start/).
  2. Create cluster: `kind create cluster --name test-cluster`.
- **Basic Commands**:
  - Delete cluster: `kind delete cluster --name test-cluster`.
  - Load image: `kind load docker-image my-image:tag`.
- **Use Case**: Simulate multi-node clusters locally or in CI.

## 6. Kubeadm
- **What is it?**: A tool for manually bootstrapping Kubernetes clusters.
- **Purpose**: Sets up production-like clusters on your own machines.
- **Installation**:
  1. Install kubeadm: [official guide](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/).
  2. Initialize: `kubeadm init`.
  3. Join nodes: `kubeadm join <master-ip>:<port>`.
- **Use Case**: Learn cluster setup or create custom environments.

## 7. Lens
- **What is it?**: A graphical IDE for managing Kubernetes clusters.
- **Purpose**: Provides a visual interface for monitoring and debugging.
- **Installation**: Download from [Lens website](https://k8slens.dev/).
- **Features**:
  - View Pods, Services, logs, and metrics.
  - Edit resources directly.
- **Use Case**: Easier cluster management for beginners or visual learners.

## 8. Skaffold
- **What is it?**: A tool for continuous development with Kubernetes.
- **Purpose**: Automates building, pushing, and deploying apps during development.
- **Installation**: [official guide](https://skaffold.dev/docs/install/).
- **Basic Commands**:
  - Run: `skaffold run`.
  - Dev mode: `skaffold dev` (watches for changes).
- **Use Case**: Streamline local dev workflows with Kubernetes.

## Integration with Kubernetes
- **Helm + Minikube**: Deploy charts locally (`helm install` on Minikube).
- **kubectl + Kind**: Manage multi-node clusters in Docker.
- **Kustomize + Skaffold**: Customize and auto-deploy apps during dev.
- **Lens + Kubeadm**: Visualize and manage custom clusters.

---

**Tags**: #Kubernetes #Helm #Minikube #kubectl #Kustomize #Kind #Kubeadm #Lens #Skaffold #DevOps