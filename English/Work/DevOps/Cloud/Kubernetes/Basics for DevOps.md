# Kubernetes Basics for DevOps 🚀

## **Core Kubernetes Components**

### **1️⃣ Pod (Basic Unit in K8s)**

A pod is the smallest deployable unit in Kubernetes, containing one or more containers.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-nginx
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
```

👉 **Deploy the pod**:

```sh
kubectl apply -f my-nginx.yaml
kubectl get pods
```

---

### **2️⃣ Deployment (Managing Scaling & Updates)**

A Deployment manages pods, ensuring replication and updates.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
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
          image: nginx:latest
          ports:
            - containerPort: 80
```

👉 **Deploy & scale**:

```sh
kubectl apply -f nginx-deployment.yaml
kubectl scale deployment nginx-deployment --replicas=5
```

---

### **3️⃣ Service (Exposing Applications)**

Pods have dynamic IPs, so we use **Service** to expose applications.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

👉 **Deploy & list services**:

```sh
kubectl apply -f nginx-service.yaml
kubectl get services
```

🔹 **Service Types:**

- **ClusterIP** – default, internal communication
    
- **NodePort** – accessible via `NodeIP:Port`
    
- **LoadBalancer** – integrates with cloud load balancers
    
- **Ingress** – HTTP(S) routing for multiple apps
    

---

### **4️⃣ ConfigMap & Secret (Configuration Storage)**

Store configuration separately from application code.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  APP_ENV: "production"
  LOG_LEVEL: "info"
```

👉 **Use ConfigMap in a pod**:

```yaml
containers:
  - name: my-app
    image: my-app:latest
    envFrom:
      - configMapRef:
          name: my-config
```

📌 **Create Secret for sensitive data**:

```sh
kubectl create secret generic my-secret --from-literal=DB_PASS=supersecret
```

---

### **5️⃣ Namespace (Resource Isolation)**

Namespaces allow resource segmentation within a cluster.

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: dev-environment
```

👉 **Use Namespace in a resource**:

```yaml
metadata:
  namespace: dev-environment
```

📌 **List namespaces**:

```sh
kubectl get namespaces
```

---

### **6️⃣ Logs & Debugging**

📌 **Check container logs**:

```sh
kubectl logs pod-name
```

📌 **Access a running container**:

```sh
kubectl exec -it pod-name -- /bin/sh
```

📌 **Describe resources**:

```sh
kubectl describe pod pod-name
```

---

### **7️⃣ Helm (Package Management for Kubernetes)**

Helm simplifies application deployment in Kubernetes.

📌 **Install Helm & Nginx chart**:

```sh
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install my-nginx bitnami/nginx
```

📌 **List installed Helm releases**:

```sh
helm list
```

---

## **Summary**

✅ **Pod** – Smallest unit in K8s  
✅ **Deployment** – Manages applications  
✅ **Service** – Exposes applications  
✅ **ConfigMap & Secret** – Configuration storage  
✅ **Namespace** – Resource isolation  
✅ **Debugging** – Logs, describe, exec  
✅ **Helm** – Kubernetes package manager

These are the core Kubernetes basics for DevOps! 🚀
problem,aktywnosc i rezulatat