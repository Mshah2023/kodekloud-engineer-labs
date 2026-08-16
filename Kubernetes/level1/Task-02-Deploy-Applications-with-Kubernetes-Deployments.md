Absolutely — here is a README in the same style as your example, but updated for the **Deployment** task. I’ve also corrected the commands so they match the actual requirement (`deployment` named `nginx`, using `nginx:latest`).

# Kubernetes Lab: Create an Nginx Deployment

## 📌 Objective

Create a Kubernetes Deployment named `nginx` to deploy the Nginx application using the `nginx:latest` container image.

| Requirement     | Value          |
| --------------- | -------------- |
| Deployment Name | `nginx`        |
| Application     | `nginx`        |
| Image           | `nginx:latest` |

---


```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 1
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
```

## 📝 Step 1: Create the YAML Manifest

Create a file named `nginx-deployment.yaml`:

### Manifest Explanation

* `apiVersion: apps/v1` — Uses the Kubernetes Apps API for Deployments.
* `kind: Deployment` — Defines the Kubernetes resource as a Deployment.
* `metadata.name` — Sets the Deployment name to `nginx`.
* `spec.replicas` — Specifies that one replica of the application should run.
* `selector.matchLabels` — Identifies the Pods managed by the Deployment.
* `template.metadata.labels` — Adds the `app: nginx` label to the Pods.
* `containers` — Defines the container that runs inside each Pod.
* `name` — Sets the container name to `nginx`.
* `image` — Uses the explicitly tagged `nginx:latest` container image.

---

## 🚀 Step 2: Create the Deployment

Apply the YAML manifest using:

```bash
kubectl apply -f nginx-deployment.yaml
```

---

## 🔍 Step 3: Verify the Deployment

Check the Deployment status:

```bash
kubectl get deployment nginx
```

To verify the Pods created by the Deployment:

```bash
kubectl get pods 
```

---

## ✅ Final Configuration

The resulting Kubernetes resources should have:

```text
Deployment:  nginx
Replicas:    1
Container:   nginx
Image:       nginx:latest
Label:       app=nginx
```

This completes the Kubernetes Deployment creation lab using an Nginx container image.



