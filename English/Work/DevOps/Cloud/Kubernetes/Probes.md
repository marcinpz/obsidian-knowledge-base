# Kubernetes Probes

Kubernetes uses three types of probes—**liveness**, **readiness**, and **startup**—to manage container health and lifecycle. Each probe serves a distinct purpose, ensuring applications run reliably and serve traffic appropriately. This document outlines their roles, configurations, and best practices.

## Liveness Probe

### Overview

A liveness probe checks if a container is running and healthy. If it fails, Kubernetes restarts the container to recover from issues like crashes or deadlocks.

### Purpose

- Detects unhealthy states (e.g., application crashes, memory leaks).
- Triggers automatic restarts to restore functionality.

### Use Cases

- Monitoring web servers for health check responses.
- Detecting stuck background workers or batch jobs.
- Recovering from app-level failures.

### Configuration Example

```yaml
spec:
  containers:
  - name: my-app
    image: my-app:latest
    livenessProbe:
      httpGet:
        path: /health
        port: 8080
      initialDelaySeconds: 15
      periodSeconds: 10
      timeoutSeconds: 5
      failureThreshold: 3
```

- **httpGet**: Expects HTTP 200–399 from `/health`.
- **initialDelaySeconds**: Waits 15 seconds before starting.
- **periodSeconds**: Probes every 10 seconds.
- **timeoutSeconds**: Waits 5 seconds for a response.
- **failureThreshold**: Restarts after 3 failures.

### Alternatives

- **TCP**: Checks port connectivity.
- **Exec**: Runs a command (e.g., `pgrep my-process`).

### Best Practices

- Use lightweight `/health` endpoints (avoid external dependency checks).
- Set `initialDelaySeconds` for startup (e.g., 30 seconds for Java apps).
- Avoid frequent probes (e.g., `periodSeconds: 20`).
- Increase `failureThreshold` for flaky apps.

### Debugging

- Check logs: `kubectl logs <pod-name>`.
- Inspect events: `kubectl describe pod <pod-name>`.
- Test endpoint: `kubectl exec <pod-name> -- curl http://localhost:8080/health`.

---

## Readiness Probe

### Overview

A readiness probe determines if a container is ready to serve traffic. If it fails, the pod is removed from Service endpoints, preventing traffic routing.

### Purpose

- Ensures pods only receive traffic when fully operational.
- Supports zero-downtime deployments and temporary unavailability.

### Use Cases

- Delaying traffic until database/cache connections are established.
- Excluding pods during maintenance or overload.
- Ensuring new pods are ready during rolling updates.

### Configuration Example

```yaml
spec:
  containers:
  - name: my-app
    image: my-app:latest
    readinessProbe:
      httpGet:
        path: /ready
        port: 8080
      initialDelaySeconds: 5
      periodSeconds: 5
      timeoutSeconds: 3
      failureThreshold: 3
```

- **httpGet**: Expects HTTP 200–399 from `/ready`.
- **initialDelaySeconds**: Waits 5 seconds.
- **periodSeconds**: Probes every 5 seconds.
- **timeoutSeconds**: Waits 3 seconds.
- **failureThreshold**: Marks unready after 3 failures.

### Alternatives

- **TCP**: Verifies port availability.
- **Exec**: Runs a readiness script.

### Best Practices

- Use `/ready` to check dependencies (e.g., database).
- Set shorter `periodSeconds` (5–10) than liveness for quick traffic adjustments.
- Optimize endpoints to avoid performance impact.

### Debugging

- Check pod status: `kubectl describe pod <pod-name>`.
- Verify endpoints: `kubectl get endpoints <service-name>`.
- Test: `kubectl exec <pod-name> -- curl http://localhost:8080/ready`.

---

## Startup Probe

### Overview

A startup probe verifies if a container’s application has started. It delays liveness and readiness probes until it succeeds, preventing premature failures.

### Purpose

- Handles slow-starting apps (e.g., Java, ML models).
- Avoids liveness probe restarts during long initializations.

### Use Cases

- Apps loading large datasets or models.
- Services waiting for external dependencies (e.g., databases).
- Legacy apps with unpredictable startup.

### Configuration Example

```yaml
spec:
  containers:
  - name: my-app
    image: my-app:latest
    startupProbe:
      httpGet:
        path: /startup
        port: 8080
      initialDelaySeconds: 10
      periodSeconds: 10
      timeoutSeconds: 5
      failureThreshold: 30
```

- **httpGet**: Expects HTTP 200–399 from `/startup`.
- **initialDelaySeconds**: Waits 10 seconds.
- **periodSeconds**: Probes every 10 seconds.
- **timeoutSeconds**: Waits 5 seconds.
- **failureThreshold**: Allows 300 seconds (30 × 10) for startup.

### Alternatives

- **TCP**: Checks port.
- **Exec**: Runs a startup check (e.g., `cat /tmp/started`).

### Best Practices

- Use for apps with startup >30 seconds.
- Set `failureThreshold * periodSeconds` to cover max startup (e.g., 600 seconds).
- Use lightweight `/startup` endpoints.
- Pair with init containers for dependency waits:
    
    ```yaml
    initContainers:
    - name: wait-for-db
      image: busybox
      command: ['sh', '-c', 'until nslookup db-service; do sleep 2; done;']
    ```
    

### Debugging

- Check events: `kubectl describe pod <pod-name>`.
- Test endpoint: `kubectl exec <pod-name> -- curl http://localhost:8080/startup`.
- Monitor logs: `kubectl logs <pod-name>`.

---

## General Notes

- **Probe Types**: All probes support HTTP, TCP, or Exec checks.
- **Best Practices**:
    - Use distinct endpoints (`/health`, `/ready`, `/startup`).
    - Monitor with Prometheus/Grafana for failure trends.
    - Adjust thresholds based on app behavior.
- **Common Issues**:
    - Misconfigured endpoints: Verify with `curl` or logs.
    - Overloaded apps: Increase `periodSeconds` or optimize endpoints.
    - Slow startups: Use startup probes with high `failureThreshold`.

## Tags

#Kubernetes #LivenessProbe #ReadinessProbe #StartupProbe #HealthCheck #ContainerManagement