---
layout: post
title: "Building Production-Grade Infrastructure for a Simple App"
subtitle: "Why I chose complexity over simplicity for my DevOps portfolio"
description: "A TV show aggregator became a showcase for GitOps, observability, and cloud-native architecture patterns"
date: 2025-08-19
categories: [devops, kubernetes, architecture]
tags: [kubernetes, argocd, terraform, gitops, gke, portfolio]
---

## The Paradox of Portfolio Projects

I faced a classic engineering dilemma: **build something complex that needs sophisticated infrastructure, or build something simple and add sophisticated infrastructure anyway?**

After cycling through ideas (distributed microservices, ML pipelines, IoT dashboards) I kept returning to one idea: a TV show aggregator. Because it was an app with some appeal and usefulness beyond demonstrating its own tech stack. The app itself is straightforward: fetch trending shows from TMDB and TVmaze APIs, rank by popularity, display in a clean interface.

**But there's a twist.** I deployed it with enterprise-grade DevOps practices that would typically serve a team of a 50+ engineers. Or at least a dozen.

## Strategic Design Decisions

### **Simple App, Complex Infrastructure**

I specifically chose a simple application to isolate and focus on infrastructure complexity. Here's why this approach worked:

**Cognitive Load Management**: Managing ArgoCD, Vault integration, and Prometheus monitoring is challenging enough without debugging distributed system race conditions simultaneously.

**Clear Separation of Concerns**: When something breaks, I can immediately identify whether it's an application bug (less likely, given the simplicity) or an infrastructure configuration issue (very likely, given the learning curve).

**Real-World Simulation**: Most production systems start simple and grow complex. This project demonstrates the infrastructure foundation that scales.

## Technical Architecture

The application architecture is intentionally minimal:

```
React Frontend ←→ Node.js API ←→ PostgreSQL ←→ External APIs
```

The **infrastructure architecture** tells a different story:

```
GitHub → Actions → GCR → ArgoCD → GKE Autopilot
    ↓                        ↓
Terraform → GCP Resources   Vault → External Secrets → K8s Secrets
    ↓                        ↓
Monitoring ← Prometheus ← Applications → Logs
```

### **Production-Grade Components**

**GitOps with ArgoCD**: Declarative deployments with dev/staging/prod environment promotion. Changes flow through Git, not `kubectl apply`.

**Infrastructure as Code**: Terraform manages GKE clusters, static IPs, DNS records, and IAM policies.

**Secrets Management**: HashiCorp Vault with External Secrets Operator. API keys and database credentials never touch Git or container images.

**Multi-Environment Overlays**: Kustomize overlays handle environment-specific configurations. Production can use different resource limits, replica counts, and ingress rules than development.

**Observability Stack**: Prometheus metrics collection with Grafana dashboards. Custom application metrics track API response times and cache hit rates.

## What I Learned

### **1. Mental Model Clarity**

Complex infrastructure demands clear mental models. When ArgoCD shows "OutOfSync" status, I need to immediately understand:
- Which Git commit should be deployed?
- What Kustomize transformations apply?
- How do external secrets affect pod startup?

**Practical Impact**: Reduced debugging time from hours to minutes by maintaining clear architectural diagrams and understanding component dependencies.

### **2. Architectural Trade-offs**

Every decision has implications. For example: [Vault as ArgoCD Application]({{ '/blog/vault-gitops/' | relative_url }}) explores why I kept secrets management outside GitOps workflows.

**Key Trade-off**: GitOps consistency vs. bootstrap complexity. Pure GitOps purists would manage Vault through ArgoCD, but circular dependencies make this operationally complex.

**Decision Framework**: Evaluate based on operational simplicity, recovery scenarios, and production patterns, not theoretical purity.

### **3. Systematic Debugging**

Production systems fail in creative ways. In [The Cluster Doctor]({{ '/blog/debugging-502-errors/' | relative_url }}) blog post I demonstrate my approach to systematic troubleshooting.

**Core Principle**: Most failures are configuration mismatches, not infrastructure failures. Port conflicts, service discovery issues, and protocol mismatches accounted for the vast majority of my deployment problems.

## Why This Approach Works

### **For Learning**
Starting with a simple application let me focus on infrastructure concepts without application complexity interference. I could experiment with GitOps workflows, monitoring configurations, and security policies without worrying about business logic bugs. For the most part :)

### **For Demonstrating**
**Systems Thinking**: Understanding how components interact across multiple layers (application, orchestration, infrastructure, security).

**Production Readiness**: Moving beyond "it works on my machine" to "it works reliably in production with proper monitoring, security, and deployment practices."

**Technology Integration**: Connecting multiple tools (ArgoCD, Vault, Prometheus, Terraform) into cohesive workflows rather than using them in isolation.

**Decision Making**: Choosing appropriate architectural patterns based on trade-offs. A lot more fun, and difficult, than following tutorials.

## Current Status
[Live application](http://tv-hub.navillasa.dev) with full GitOps deployment, multi-environment promotion, and comprehensive monitoring.

**Next Phases**: Cost optimization dashboard, Redis caching layer, and advanced alerting rules.

## The Meta-Learning

This project demonstrates that I can build production-ready infrastructure, make informed architectural decisions, and systematically debug complex systems.

More than learning how to use individual tools, I learned how they integrate, _when_ to use them, and what trade-offs each decision creates.

Building infrastructure for a simple application taught me more about production DevOps than building a complex application with simple deployment ever could.
