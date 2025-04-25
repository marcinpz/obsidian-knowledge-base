# Kubernetes Service vs Ingress

This document compares **Kubernetes Service** and **Ingress**, two Kubernetes resources for managing network traffic. While they often work together, they serve distinct purposes.

## Kubernetes Service

- **Purpose**: Exposes a set of pods internally or externally by providing a stable endpoint (IP or DNS name) for communication.
- **Functionality**:
  - Load-balances traffic across pods based on labels/selectors.
  - Types:
    - **ClusterIP** (default, internal)
    - **NodePort** (exposes on node IPs)
    - **LoadBalancer** (cloud provider load balancer)
    - **ExternalName** (maps to external DNS)
  - Operates at **Layer 4** (TCP/UDP).
- **Use Case**: Internal pod-to-pod communication or exposing services to external traffic with basic load balancing.
- **Example**:

  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: my-service
  spec:
    selector:
      app: my-app
    ports:
      - protocol: TCP
        port: 80
        targetPort: 8080
    type: ClusterIP
  ```

## Ingress

- **Purpose**: Manages external HTTP/HTTPS traffic to services, providing advanced routing and load balancing.
- **Functionality**:
  - Operates at **Layer 7** (HTTP/HTTPS).
  - Routes traffic based on URL paths, hostnames, or other rules.
  - Requires an **Ingress Controller** (e.g., NGINX, Traefik) to function.
  - Supports TLS termination, path-based routing, and virtual hosting.
- **Use Case**: Exposing multiple services under a single external IP with domain-based or path-based routing (e.g., `example.com/api` vs. `example.com/web`).
- **Example**:

  ```yaml
  apiVersion: networking.k8s.io/v1
  kind: Ingress
  metadata:
    name: my-ingress
  spec:
    rules:
    - host: example.com
      http:
        paths:
        - path: /api
          pathType: Prefix
          backend:
            service:
              name: api-service
              port:
                number: 80
        - path: /web
          pathType: Prefix
          backend:
            service:
              name: web-service
              port:
                number: 80
    tls:
    - hosts:
      - example.com
      secretName: tls-secret
  ```

## Key Differences

| Aspect | Service | Ingress |
| --- | --- | --- |
| **Layer** | Layer 4 (TCP/UDP) | Layer 7 (HTTP/HTTPS) |
| **Scope** | Internal or external pod access | External HTTP/HTTPS traffic routing |
| **Routing** | Basic load balancing across pods | Advanced routing (path, host, etc.) |
| **Dependency** | Standalone | Requires Ingress Controller |
| **Use Case** | Pod-to-pod or simple external access | Complex HTTP routing, TLS, virtual hosts |
| **Configuration** | Simple port mapping | Rules-based routing, TLS support |

## How They Work Together

- A **Service** exposes pods and provides a stable endpoint.
- An **Ingress** routes external HTTP/HTTPS traffic to the appropriate Service based on rules.
- **Example Workflow**: External traffic hits the Ingress Controller, which uses Ingress rules to route requests to a Service, which then load-balances to pods.

## When to Use

- Use a **Service** for internal communication or basic external exposure (e.g., via LoadBalancer).
- Use an **Ingress** for managing multiple HTTP services under one IP with domain/path-based routing or TLS.

For specific setup or configuration help, refer to the Kubernetes documentation or reach out for assistance.

---

**Tags**: #Kubernetes #Networking #Service #Ingress