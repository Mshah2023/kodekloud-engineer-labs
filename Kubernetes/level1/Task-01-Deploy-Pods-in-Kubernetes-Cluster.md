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
```

### Command Output

```text
pod/pod-nginx created
```

This confirms that the `pod-nginx` Pod was successfully created.

---

## 🔍 Step 3: Verify the Pod

Check the Pod status and labels:

```bash
kubectl get pod pod-nginx --show-labels
```

### Command Output

```text
NAME        READY   STATUS    RESTARTS   AGE   LABELS
pod-nginx   1/1     Running   0          10s   app=nginx_app
```

The output confirms that:

* The Pod is named `pod-nginx`.
* The container is ready (`1/1`).
* The Pod is in the `Running` state.
* The label `app=nginx_app` is correctly applied.

---

## 🔎 Step 4: Verify the Container Configuration

To verify the container name and image, run:

```bash
kubectl describe pod pod-nginx
```

### Relevant Command Output

```text
Name:             pod-nginx
Namespace:        default
Status:           Running

Containers:
  nginx-container:
    Image:          nginx:latest
    State:          Running
    Ready:          True
```

---

## ✅ Final Configuration

The resulting Pod has the following configuration:

```text
Pod:        pod-nginx
Container:  nginx-container
Image:      nginx:latest
Label:      app=nginx_app
Status:     Running
```

This completes the Kubernetes Pod creation lab using a YAML manifest.
