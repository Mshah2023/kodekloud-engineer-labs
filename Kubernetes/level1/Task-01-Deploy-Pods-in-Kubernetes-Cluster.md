# Kubernetes Task 1 – Create a Pod Using a YAML Manifest

This task demonstrates how to create a basic Kubernetes Pod using a YAML manifest and deploy it with `kubectl`.

## Objective

Create a Kubernetes Pod with the following configuration:

| Property       | Value             |
| -------------- | ----------------- |
| Pod Name       | `pod-nginx`       |
| Container Name | `nginx-container` |
| Image          | `nginx:latest`    |
| Label          | `app=nginx_app`   |

---

## Files

```text
.
├── README.md
└── pod-nginx.yaml
```

---

## YAML Manifest

Create a file named `pod-nginx.yaml`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-nginx
  labels:
    app: nginx_app
spec:
  containers:
    - name: nginx-container
      image: nginx:latest
```

---

## Deploy the Pod

```bash
kubectl apply -f pod-nginx.yaml
```

Expected output:

```text
pod/pod-nginx created
```

---

## Verify the Deployment

List the Pods and display their labels:

```bash
kubectl get pods --show-labels
```

Example output:

```text
NAME        READY   STATUS    RESTARTS   AGE   LABELS
pod-nginx   1/1     Running   0          10s   app=nginx_app
```

View detailed information about the Pod:

```bash
kubectl describe pod pod-nginx
```
