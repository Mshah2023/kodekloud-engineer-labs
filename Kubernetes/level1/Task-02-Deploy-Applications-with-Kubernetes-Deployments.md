# Create an Nginx Kubernetes Deployment

## Objective

Create a Kubernetes deployment named `nginx` to deploy the Nginx application using the `nginx:latest` image.

### Requirements

* **Deployment Name:** `nginx`
* **Application:** `nginx`
* **Image:** `nginx:latest`
* **Server:** Jump Host

---

## Steps

### 1. Create the Deployment YAML File

Create a file named `nginx-deployment.yaml`:
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

### Manifest Explanation

* `apiVersion: apps/v1` — Uses the Kubernetes Apps API.
* `kind: Deployment` — Defines the resource as a Deployment.
* `metadata.name` — Sets the Deployment name to `nginx`.
* `spec.replicas` — Specifies that 1 Pod replica should be maintained.
* `spec.selector` — Defines how the Deployment identifies its Pods.
* `matchLabels` — Matches Pods with the label `app: nginx`.
* `template` — Defines the configuration for Pods created by the Deployment.
* `template.metadata.labels` — Adds the label `app: nginx` to the Pods.
* `spec.containers` — Defines the container running inside the Pod.
* `name` — Sets the container name to `nginx`.
* `image` — Uses the `nginx:latest` container image.


```bash
vi nginx-deployment.yaml
```

Add the following configuration:

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
        - name: nginx-container
          image: nginx:latest
```

Save and exit the file.

### 2. Create the Deployment

Apply the YAML configuration:

```bash
kubectl apply -f nginx-deployment.yaml
```

Expected output:

```text
deployment.apps/nginx created
```

### 3. Verify the Deployment

Check the deployment:

```bash
kubectl get deployment nginx
```

Expected output:

```text
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
nginx   1/1     1            1           ...
```

### 4. Verify the Pod

Check the pod created by the deployment:

```bash
kubectl get pods
```

The pod should be in the `Running` state.

### 5. Verify the Deployment Configuration

```bash
kubectl describe deployment nginx
```

You can also verify the image:

```bash
kubectl get deployment nginx -o yaml
```

Confirm that the deployment uses:

```text
Image: nginx:latest
```

---

## Command Summary

```bash
vi nginx-deployment.yaml

kubectl apply -f nginx-deployment.yaml

kubectl get deployment nginx

kubectl get pods

kubectl describe deployment nginx

kubectl get deployment nginx -o yaml
```

## Result

A Kubernetes deployment named **nginx** is created with one replica running the **nginx:latest** image.

## Key Takeaway

Using a Kubernetes Deployment provides declarative management of the Nginx application and ensures that the desired number of Nginx pods are maintained by the Kubernetes cluster.



