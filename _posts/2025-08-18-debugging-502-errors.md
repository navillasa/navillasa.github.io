---
layout: post
title: "The K8s Doctor, or How I Learned to Stop Worrying and Debug 502s"
subtitle: "A systematic approach to debugging port and protocol mismatches"
date: 2025-08-18
categories: [kubernetes, debugging, devops]
tags: [kubernetes, 502-errors, troubleshooting, nginx, ingress]
---

## The Problem Pattern

Throughout this project, I've hit the same type of issue repeatedly:
- **Frontend** looking for `dev-backend-service` instead of `prod-backend-service`
- **ArgoCD ingress** using port 443 instead of port 80
- **Vault** connection errors due to service discovery issues
- **External Secrets** pointing to wrong Vault paths

**The common thread**: 502 Bad Gateway errors caused by communication mismatches.

## The 502 Error: What It Really Means

```
502 Bad Gateway = "I can reach something, but it's not responding correctly"
```

**This is different from:**
- **404**: "I can't find anything at this path"
- **503**: "Service is temporarily unavailable"  
- **Connection timeout**: "I can't reach anything at all"

**502 specifically means**: The proxy/load balancer reached a backend, but the backend response was invalid.

## The Systematic Debugging Approach

### Step 1: Identify the Communication Chain

Every 502 has a path like this:
```
Client → Load Balancer → Service → Pod
```

Find where it breaks by checking each link.

### Step 2: Check Backend Health in Load Balancer

```bash
# Get detailed ingress status
kubectl describe ingress <ingress-name> -n <namespace>

# Look for backend health status
# Example output:
ingress.kubernetes.io/backends: {
  "k8s1-backend-service-443":"UNHEALTHY"  # ← The smoking gun!
}
```

**Key indicators:**
- `UNHEALTHY` = Backend isn't responding on expected port/protocol
- `HEALTHY` = Backend is fine, look elsewhere

## Pro Tips for Faster Debugging

### 1. **Use Port-Forward for Direct Testing**
```bash
# Bypass ingress/service and test pod directly
kubectl port-forward pod/<pod-name> 8080:8080
curl http://localhost:8080/health
```

### 2. **Check Multiple Namespaces**
```bash
# Service in wrong namespace is super common
kubectl get services --all-namespaces | grep <service-name>
```

The key insight: Most 502 errors are configuration mismatches, not infrastructure failures. A systematic approach beats random troubleshooting every time.
