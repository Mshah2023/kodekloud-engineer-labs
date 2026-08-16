# Create a Kubernetes Pod with Resource Requests and Limits

## Objective

Create a Kubernetes pod named `httpd-pod` with a container named `httpd-container`. Configure CPU and memory resource requests and limits for the container to control resource utilization.

### Requirements

* **Pod Name:** `httpd-pod`
* **Container Name:** `httpd-container`
* **Image:** `httpd:latest`
* **Memory Request:** `15Mi`
* **CPU Request:** `100m`
* **Memory Limit:** `20Mi`
* **CPU Limit:** `100m`
* **Server:** Jump Host

---

## Steps

### 1. Create the Pod YAML File

Create a file named `httpd-pod.yaml`:

```bash
vi httpd-pod.yaml
```

Add the following configuration:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: httpd-pod
spec:
  containers:
    - name: httpd-container
      image: httpd:latest
      resources:
        requests:
          memory: "15Mi"
          cpu: "100m"
        limits:
          memory: "20Mi"
          cpu: "100m"
```

Save and exit the file.

### 2. Create the Pod

Apply the YAML configuration using `kubectl`:

```bash
kubectl apply -f httpd-pod.yaml
```

Expected output:

```text
pod/httpd-pod created
```

### 3. Verify the Pod

Check the pod status:

```bash
kubectl get pod httpd-pod
```

Expected output:

```text
NAME        READY   STATUS    RESTARTS   AGE
httpd-pod   1/1     Running   0          ...
```

### 4. Verify Resource Configuration

Check the pod details:

```bash
kubectl describe pod httpd-pod
```

Under the **Containers** section, verify:

```text
Requests:
  cpu:     100m
  memory:  15Mi
Limits:
  cpu:     100m
  memory:  20Mi
```

You can also verify the complete YAML configuration:

```bash
kubectl get pod httpd-pod -o yaml
```

---

## Command Summary

```bash
vi httpd-pod.yaml

kubectl apply -f httpd-pod.yaml

kubectl get pod httpd-pod

kubectl describe pod httpd-pod

kubectl get pod httpd-pod -o yaml
```


## Result

A pod named **httpd-pod** is created with the following configuration:

* **Container:** `httpd-container`
* **Image:** `httpd:latest`
* **CPU Request:** `100m`
* **Memory Request:** `15Mi`
* **CPU Limit:** `100m`
* **Memory Limit:** `20Mi`

## Key Takeaway

Using a YAML manifest makes the Kubernetes configuration declarative, repeatable, and easy to version-control. Resource requests help Kubernetes schedule the pod appropriately, while resource limits prevent the container from exceeding its defined CPU and memory constraints.
