# Kubernetes Lab: Create an Nginx Pod

## 📌 Objective

Create a Kubernetes Pod named `pod-nginx` using a YAML manifest with the following configuration:

| Requirement    | Value             |
| -------------- | ----------------- |
| Pod Name       | `pod-nginx`       |
| Container Name | `nginx-container` |
| Image          | `nginx:latest`    |
| Label          | `app: nginx_app`  |

---

## 📝 Step 1: Create the YAML Manifest

Create a file named `pod-nginx.yaml`:

```bash
![alt text](image.png)
```

### Manifest Explanation

* `apiVersion: v1` — Uses the Kubernetes Core API.
* `kind: Pod` — Defines the resource as a Pod.
* `metadata.name` — Sets the Pod name to `pod-nginx`.
* `metadata.labels` — Adds the label `app: nginx_app`.
* `spec.containers` — Defines the container running inside the Pod.
* `name` — Sets the container name to `nginx-container`.
* `image` — Uses the `nginx:latest` container image.

---

## 🚀 Step 2: Create the Pod

Apply the YAML manifest using:

```bash
kubectl apply -f pod-nginx.yaml
![alt text](image-1.png)
```

---

## 🔍 Step 3: Verify the Pod

Check the Pod status:

```bash
kubectl get pod pod-nginx --show-lebals
![alt text](image-2.png) 
```

---

## ✅ Final Configuration

The resulting Pod should have:

```text
Pod:        pod-nginx
Container:  nginx-container
Image:      nginx:latest
Label:      app=nginx_app
```

This completes the Kubernetes Pod creation lab using a YAML manifest.
