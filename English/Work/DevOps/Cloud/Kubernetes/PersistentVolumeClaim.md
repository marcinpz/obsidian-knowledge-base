# Kubernetes PersistentVolumeClaim (PVC)

## What Is a PVC?

A **PersistentVolumeClaim (PVC)** is a request for persistent storage in [[Kubernetes]]. It acts as an abstraction over a **PersistentVolume (PV)**, enabling users to consume storage resources without needing to know the underlying infrastructure.

## Key Concepts

- **PersistentVolume (PV)**: A piece of storage in the cluster.
    
- **PersistentVolumeClaim (PVC)**: A request for storage by a user or a pod.
    
- **StorageClass**: Defines how dynamic provisioning of volumes is performed.
    

## PVC Lifecycle

1. User creates a PVC.
    
2. Kubernetes finds a suitable PV or dynamically provisions one using the specified StorageClass.
    
3. PVC gets bound to the PV.
    
4. The Pod mounts the PVC as a volume.
    

## PVC Example

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
  storageClassName: standard
```

### Fields Explained

- `accessModes`:
    
    - `ReadWriteOnce`: The volume can be mounted as read-write by a single node.
        
    - `ReadOnlyMany`: The volume can be mounted read-only by many nodes.
        
    - `ReadWriteMany`: The volume can be mounted read-write by many nodes.
        
- `resources.requests.storage`: Specifies how much storage is requested.
    
- `storageClassName`: Which StorageClass to use for dynamic provisioning.
    

## Pod Using a PVC

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: my-container
    image: nginx
    volumeMounts:
    - mountPath: "/usr/share/nginx/html"
      name: my-storage
  volumes:
  - name: my-storage
    persistentVolumeClaim:
      claimName: my-pvc
```

## Dynamic vs Static Provisioning

- **Dynamic**: PVC triggers automatic PV creation via a StorageClass.
    
- **Static**: Admin manually creates PVs; PVCs bind to matching ones.
    

## Reclaim Policies

- **Retain**: PV data is preserved after PVC deletion.
    
- **Delete**: PV and its storage are deleted with the PVC.
    
- **Recycle** (deprecated): Basic scrub and reuse.
    

## Common Use Cases

- Database persistent storage
    
- Application caches
    
- StatefulSets and legacy storage needs
    

## Tips

- Use dynamic provisioning whenever possible.
    
- Monitor PVC usage to avoid orphaned volumes.
    
- Combine with StatefulSets for stable volume-to-pod binding.
    

---

**References**:

- [https://kubernetes.io/docs/concepts/storage/persistent-volumes/](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)
    
- [https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)