# Kubernetes Access Methods: Port Forwarding vs Proxy

This note compares two methods to access Kubernetes resources (e.g., a `ClusterIP` service) from your local machine: **[[port forwarding]]** (`kubectl port-forward`) and **[[proxy]]** (`kubectl proxy`).

---

## Port Forwarding (`kubectl port-forward`)

### How It Works
- Creates a direct tunnel from a local port to a specific resource (pod, service, etc.) in the cluster.
- Bypasses the Kubernetes API server for data transfer.

### Syntax
```bash
kubectl port-forward <resource-type>/<resource-name> <local-port>:<remote-port>
```
**Example:**
```bash
kubectl port-forward service/nginx-service 8080:80
```
- Local: `localhost:8080` → Service: `nginx-service:80`

### Use Case
- Debugging or testing a specific application (e.g., hitting an Nginx endpoint).
- Direct, low-latency access to a pod or service.

### Pros
- Simple and fast for single-resource access.
- No API server overhead.

### Cons
- Limited to one resource at a time.
- Requires specifying the resource and ports.

### Example
```bash
kubectl port-forward service/nginx-service 8080:80
curl http://localhost:8080
# Output: "Welcome to nginx!"
```

---

## Proxy (`kubectl proxy`)

### How It Works
- Runs a local server that proxies requests to the Kubernetes API server.
- Exposes the entire API and allows access to resources via API endpoints (e.g., `/proxy/`).

### Syntax
```bash
kubectl proxy
```
- Default port: `8001`

### Access URL
```bash
http://localhost:8001/api/v1/namespaces/<namespace>/services/<service-name>/proxy/
```
**Example:**
```bash
curl http://localhost:8001/api/v1/namespaces/default/services/nginx-service/proxy/
```

### Use Case
- Exploring the Kubernetes API or accessing multiple resources.
- Quick access to services without knowing their internal IPs.

### Pros
- Broad access to all cluster resources via the API.
- No need to specify individual resources upfront.

### Cons
- Indirect access (API server adds overhead).
- Less efficient for high-throughput testing.

### Example
```bash
kubectl proxy
curl http://localhost:8001/api/v1/namespaces/default/services/nginx-service/proxy/
# Output: "Welcome to nginx!"
```

---

## Comparison

| Feature            | Port Forwarding            | Proxy                     |
|--------------------|----------------------------|---------------------------|
| **Target**         | Single resource            | Entire API                |
| **Traffic Path**   | Local → Resource           | Local → API → Resource    |
| **Scope**          | Specific pod/service       | Cluster-wide              |
| **Performance**    | Direct, low latency        | Indirect, API overhead    |
| **Best For**       | App debugging              | API exploration           |

---

## When to Use
- **Port Forwarding:** Use for direct access to a specific app (e.g., `curl http://localhost:8080`).
- **Proxy:** Use for API interaction or accessing multiple resources without individual setup.

---

## Tags
#kubernetes #networking #kubectl #debugging