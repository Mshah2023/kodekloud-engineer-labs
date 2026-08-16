# Rollback a Kubernetes Deployment

## Objective

Rollback the Kubernetes Deployment named `nginx-deployment` to its previous revision after a bug was discovered in the latest application release.

### Requirements

* **Deployment Name:** `nginx-deployment`
* **Action:** Rollback to the previous revision
* **Server:** Jump Host

---

## Steps

### 1. Check the Current Deployment

Verify that the Deployment exists:

```bash
kubectl get deployment nginx-deployment
```

Check the current Pods:

```bash
kubectl get pods
```

### 2. Check the Rollout History

View the Deployment revision history:

```bash
kubectl rollout history deployment/nginx-deployment
```

This shows the available Deployment revisions.

Example:

```text
deployment.apps/nginx-deployment
REVISION  CHANGE-CAUSE
1         <none>
2         <none>
```

### 3. Rollback to the Previous Revision

Rollback the Deployment to the previous revision:

```bash
kubectl rollout undo deployment/nginx-deployment
```

Expected output:

```text
deployment.apps/nginx-deployment rolled back
```

### 4. Monitor the Rollback

Check the rollback status:

```bash
kubectl rollout status deployment/nginx-deployment
```

Expected output:

```text
deployment "nginx-deployment" successfully rolled out
```

### 5. Verify the Pods

Check that the Pods are operational:

```bash
kubectl get pods
```

Ensure the Pods show `Running` and are ready.

### 6. Verify the Deployment

Check the Deployment details:

```bash
kubectl describe deployment nginx-deployment
```

You can also check the rollout history again:

```bash
kubectl rollout history deployment/nginx-deployment
```

---

## Command Summary

```bash
kubectl get deployment nginx-deployment

kubectl get pods

kubectl rollout history deployment/nginx-deployment

kubectl rollout undo deployment/nginx-deployment

kubectl rollout status deployment/nginx-deployment

kubectl get pods

kubectl describe deployment nginx-deployment

kubectl rollout history deployment/nginx-deployment
```


## Result

The **nginx-deployment** Deployment is rolled back to its **previous revision**.

The rollout status is checked to ensure the rollback completes successfully, and the Pods are verified to ensure they are operational.

## Key Takeaway

Kubernetes Deployments maintain revision history, allowing teams to quickly roll back to a previous stable version when a newly deployed release introduces problems.
