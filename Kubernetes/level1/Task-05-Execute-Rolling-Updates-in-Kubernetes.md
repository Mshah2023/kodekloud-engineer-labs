# Perform a Rolling Update for an Nginx Deployment

## Objective

Update the existing Kubernetes Deployment named `nginx-deployment` from its current Nginx image to `nginx:1.18` using a rolling update strategy.

### Requirements

* **Deployment Name:** `nginx-deployment`
* **New Image:** `nginx:1.18`
* **Update Type:** Rolling Update
* **Server:** Jump Host

---

## Steps

### 1. Check the Existing Deployment

Verify the current Deployment:

```bash
kubectl get deployment nginx-deployment
```

Check the existing Pods:

```bash
kubectl get pods
```

### 2. Check the Current Image

View the current image used by the Deployment:

```bash
kubectl describe deployment nginx-deployment
```

You can also run:

```bash
kubectl get deployment nginx-deployment -o yaml
```

### 3. Perform the Rolling Update

Update the Deployment to use `nginx:1.18`:

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.18
```

Expected output:

```text
deployment.apps/nginx-deployment image updated
```

> The container name `nginx` is used in the command above. If the existing Deployment uses a different container name, check it with `kubectl describe deployment nginx-deployment` and use that name instead.

### 4. Monitor the Rolling Update

Watch the rollout progress:

```bash
kubectl rollout status deployment/nginx-deployment
```

Expected output:

```text
deployment "nginx-deployment" successfully rolled out
```

### 5. Verify All Pods Are Running

Check the Pods:

```bash
kubectl get pods
```

Ensure all Pods show `Running` and are ready.

### 6. Verify the New Image

Confirm that the Deployment is using `nginx:1.18`:

```bash
kubectl describe deployment nginx-deployment
```

You can also verify directly:

```bash
kubectl get deployment nginx-deployment -o yaml
```

The container image should show:

```text
image: nginx:1.18
```

---

## Command Summary

```bash
kubectl get deployment nginx-deployment

kubectl get pods

kubectl describe deployment nginx-deployment

kubectl set image deployment/nginx-deployment nginx=nginx:1.18

kubectl rollout status deployment/nginx-deployment

kubectl get pods

kubectl get deployment nginx-deployment -o yaml
```

## Result

The `nginx-deployment` Deployment is updated from its previous image to **nginx:1.18** using a rolling update.

The rollout is monitored using `kubectl rollout status`, and the Pods are verified to ensure they are operational after the update.

## Key Takeaway

A rolling update allows Kubernetes to gradually replace existing Pods with new Pods running the updated image, helping maintain application availability during the deployment.
