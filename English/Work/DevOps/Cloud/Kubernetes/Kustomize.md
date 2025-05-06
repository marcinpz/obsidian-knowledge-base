# Kustomize for DevOps

## Introduction

Kustomize is a tool for managing Kubernetes manifests with a focus on **declarative customization** without modifying the original YAML files. It is natively integrated into `kubectl`, making it a powerful tool for DevOps engineers to manage complex deployments.

## Key Concepts

- **Base**: The original Kubernetes YAML files (Deployments, Services, etc.).
    
- **Overlay**: A customized version of a base, adjusted for different environments like dev, staging, or production.
    
- **Patches**: YAML snippets that modify parts of the base resources.
    
- **Kustomization File (`kustomization.yaml`)**: The configuration file that defines how resources are composed and patched.
    

## Why Use Kustomize for DevOps?

- **Environment-specific configurations**: Manage multiple environments (dev, staging, prod) cleanly.
    
- **No template engine required**: Pure YAML without introducing another templating language.
    
- **Version control friendly**: Keep bases and overlays separately, making GitOps workflows more efficient.
    
- **Built-in Kubernetes support**: Works seamlessly with `kubectl apply -k`.
    

## Basic Directory Structure

```
.
├── base
│   ├── deployment.yaml
│   ├── service.yaml
│   └── kustomization.yaml
└── overlays
    ├── dev
    │   ├── kustomization.yaml
    │   └── patch.yaml
    ├── staging
    │   └── kustomization.yaml
    └── prod
        └── kustomization.yaml
```

## Example Usage

### Base `kustomization.yaml`

```yaml
resources:
  - deployment.yaml
  - service.yaml
```

### Overlay `kustomization.yaml` (for dev)

```yaml
bases:
  - ../../base

patchesStrategicMerge:
  - patch.yaml
```

### Patch Example (`patch.yaml`)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 2
```

This patch changes the number of replicas only for the dev environment.

## Advanced Features

- **Transformers**: Automatically modify labels, annotations, namespaces, etc.
    
- **Generators**: Create ConfigMaps and Secrets on the fly.
    
- **Variables and Substitutions**: Inject environment-specific values dynamically.
    

## Common Commands

```bash
# Build the resources and output the final YAML
kustomize build overlays/dev

# Apply resources to the cluster
kubectl apply -k overlays/dev

# Diff current cluster resources vs. local
kubectl diff -k overlays/dev
```

## Best Practices

- Keep base manifests minimal and reusable.
    
- Use overlays to manage environment-specific changes.
    
- Validate overlays using `kustomize build` before applying.
    
- Integrate into CI/CD pipelines (e.g., GitHub Actions, GitLab CI, Jenkins).
    
- Combine with GitOps tools like Argo CD or Flux.
    

## Useful Links

- [Kustomize Official Documentation](https://kubectl.docs.kubernetes.io/references/kustomize/)
    
- [GitHub - kubernetes-sigs/kustomize](https://github.com/kubernetes-sigs/kustomize)