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

### Expected output:

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

### Expected output:

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

### Relevant Expected output:

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

## Result

A Pod named pod-nginx is created with:

```text
Pod:        pod-nginx
Container:  nginx-container
Image:      nginx:latest
Label:      app=nginx_app
Status:     Running
```

## Key Takeaway

A Kubernetes Pod manifest provides a declarative way to define the Pod, its labels, and the container it runs. Explicitly specifying nginx:latest ensures the required image tag is used.