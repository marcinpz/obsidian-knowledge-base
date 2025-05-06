# ArgoCD for DevOps

## Overview

ArgoCD (Argo Continuous Delivery) is a declarative, GitOps continuous delivery tool for Kubernetes. It enables DevOps teams to manage infrastructure and application deployments easily, ensuring consistency and reliability through Git as the source of truth.

## Key Features

- **Declarative GitOps Approach**: Automatically synchronize Kubernetes resources with Git repositories.
    
- **Multi-Cluster Management**: Manage multiple Kubernetes clusters from a single ArgoCD instance.
    
- **Application Health Monitoring**: Visual status dashboards, health checks, and automatic drift detection.
    
- **RBAC and SSO Integration**: Secure access using role-based access control and single sign-on.
    
- **Web UI and CLI**: User-friendly interfaces for managing and troubleshooting deployments.
    

## Typical DevOps Use Cases

- Continuous delivery pipelines for microservices.
    
- Infrastructure as Code (IaC) deployments.
    
- Progressive delivery strategies (blue-green deployments, canary releases).
    
- Automated rollback on failure detection.
    
- Multi-environment management (dev, staging, production).
    

## Core Concepts

- **Application**: An ArgoCD object that defines the desired state of a Kubernetes resource tree from a Git repository.
    
- **Sync**: The process of making the live state match the desired state.
    
- **Hooks**: Custom operations that can be triggered during the sync process.
    
- **Projects**: Logical grouping of applications with shared permissions and policies.
    

## Architecture

- **API Server**: The interface for CLI, UI, and Git webhook integrations.
    
- **Controller**: Watches Git repositories and Kubernetes clusters to synchronize state.
    
- **Repositories**: Git repositories serving as the source of manifests (Helm charts, Kustomize, YAML, etc.).
    
- **Clusters**: Kubernetes clusters where applications are deployed.
    

## Installation (Quickstart)

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Expose the ArgoCD API server:

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Access the UI at: `https://localhost:8080`

## Basic Workflow

1. **Install ArgoCD** on a Kubernetes cluster.
    
2. **Define Applications** linked to Git repositories.
    
3. **Sync Applications** manually or enable auto-sync.
    
4. **Monitor Health** and manage changes via the UI or CLI.
    
5. **Roll back** if necessary through UI or automation.
    

## Best Practices

- Keep manifests declarative and versioned in Git.
    
- Use ArgoCD Projects to enforce security boundaries.
    
- Automate application updates with auto-sync and hooks.
    
- Integrate with CI pipelines to trigger GitOps flows.
    
- Regularly monitor and audit application health and synchronization status.
    

## Useful Commands

```bash
# Login to ArgoCD CLI
argocd login <ARGOCD_SERVER>

# Create an application
argocd app create <APP_NAME> \
  --repo <REPO_URL> \
  --path <APP_PATH> \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace <NAMESPACE>

# Sync an application
argocd app sync <APP_NAME>

# Check application status
argocd app get <APP_NAME>
```

## Further Resources

- [ArgoCD Official Documentation](https://argo-cd.readthedocs.io/en/stable/)
    
- [GitOps Principles](https://www.gitops.tech/)
    
- [Argo Project GitHub](https://github.com/argoproj/argo-cd)
    

---

#tags: #DevOps #ArgoCD #GitOps #Kubernetes

---

_Notes prepared for DevOps daily operations in Obsidian._