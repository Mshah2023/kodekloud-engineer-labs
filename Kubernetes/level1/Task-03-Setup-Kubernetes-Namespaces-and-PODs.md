Yes — for this task, the README should use **YAML manifests** rather than `kubectl run`. Following the same structure as your previous examples:

# Create a Namespace and Nginx Pod Using YAML

> **KodeKloud Engineer Task**
> Create a namespace named `dev` and deploy an Nginx Pod named `dev-nginx-pod` inside it using a Kubernetes YAML manifest.

---

## Objective

Create the following Kubernetes resources:

| Requirement     | Value              |
| --------------- | ------------------ |
| Namespace       | `dev`              |
| Pod Name        | `dev-nginx-pod`    |
| Container Image | `nginx:latest`     |
| Target          | Kubernetes Cluster |

> **Note:** The `kubectl` utility on the jump host has been configured to work with the Kubernetes cluster.

---

## Implementation

### 1. Create the YAML File

Create a YAML file for the namespace and Pod:

```bash
vi pod.yml
```

Add the following configuration:

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: dev

---

apiVersion: v1
kind: Pod
metadata:
  name: dev-nginx-pod
  namespace: dev
spec:
  containers:
    - name: nginx-container
      image: nginx:latest
```

The YAML file contains two resources:

* A `Namespace` named `dev`.
* A `Pod` named `dev-nginx-pod` inside the `dev` namespace.

The container explicitly uses the required image:

```text
nginx:latest
```

---

### 2. Apply the YAML Configuration

Create the resources using:

```bash
kubectl apply -f pod.yml
```

Expected output:

```text
namespace/dev created
pod/dev-nginx-pod created
```

---

## Verification

### Verify the Namespace

```bash
kubectl get namespace dev
```

Expected output:

```text
NAME   STATUS   AGE
dev    Active   ...
```

---

### Verify the Pod

Check the Pod in the `dev` namespace:

```bash
kubectl get pod -n dev
```

Expected output:

```text
NAME            READY   STATUS    RESTARTS   AGE
dev-nginx-pod   1/1     Running   0          ...
```

The `1/1 Running` status confirms that the Nginx container is running successfully.

---

### Verify the Pod Configuration

To verify that the Pod is using the required image:

```bash
kubectl get pod dev-nginx-pod -n dev -o yaml
```

Look for:

```yaml
containers:
  - name: nginx-container
    image: nginx:latest
```

---

## Command Summary

```bash
vi pod.yml

kubectl apply -f pod.yml

kubectl get namespace dev

kubectl get pod -n dev

kubectl get pod dev-nginx-pod -n dev -o yaml
```

---

## Result

The Kubernetes task was successfully completed.

* Namespace `dev` was created.
* Pod `dev-nginx-pod` was created inside the `dev` namespace.
* The Pod uses the required `nginx:latest` image.
* The Nginx container is running successfully.
* Final Pod status is `1/1 Running`.

---

## Key Takeaway

Kubernetes resources can be defined declaratively using YAML manifests.

In this task, both the namespace and Pod are defined in the same YAML file:

```yaml
apiVersion: v1
kind: Namespace
```

and:

```yaml
apiVersion: v1
kind: Pod
```

The Pod is placed in the correct namespace using:

```yaml
metadata:
  name: dev-nginx-pod
  namespace: dev
```

Using:

```yaml
image: nginx:latest
```

also ensures that the required image tag is explicitly specified.
