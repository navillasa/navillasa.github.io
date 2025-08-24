---
layout: post
title: "Multi-Cloud LLM Routing: When Infrastructure Gets Smart About Money"
date: 2025-08-24
categories: [infrastructure, llm, multi-cloud]
tags: [go, kubernetes, argocd, pulumi, aws, gcp, azure, llm, infrastructure]
---

After successfully running a self-hosted mini LLM (gpt4all-j) on Hetzner, I found myself hungry for a bigger challenge. I wanted to combine several of my interests and learning goals into one ambitious project: running Kubernetes across all three major cloud providers, gaining more hands-on experience with ArgoCD, diving deeper into LLM hosting, and finally getting to work with Pulumi and Go (my absolute favorite programming language).

What started as a learning exercise is evolving into an ambitious multi-cloud LLM router that will automatically distribute requests to the cheapest available cluster across AWS, GCP, and Azure. Currently, I have the router working locally and the AWS infrastructure fully provisioned, with the remaining cloud deployments and full multi-cloud integration as the next major milestone.

## The Problem: LLM Cost Optimization at Scale

Large Language Models are expensive to run. Whether you're using OpenAI's API, hosting your own models, or running inference at scale, costs can quickly spiral out of control. The traditional approach involves either sticking with a single cloud provider (hello, vendor lock-in), manually switching between providers (time-consuming and error-prone), or using static routing that doesn't adapt to real-time price changes or performance.

I wanted to build something that could:
- Automatically route to the cheapest healthy cluster in real-time
- Run across multiple clouds for redundancy and cost optimization
- Scale to zero during low usage periods
- Use CPU-only inference with quantized models for maximum cost efficiency
- Provide comprehensive observability for cost tracking and performance monitoring

## The Solution: An Intelligent Multi-Cloud Router

The architecture I built follows this pattern:

```
[Client] ──HTTPS──> [Global Router (Go Application)]
                         │
          ┌──────────────┼────────────────┐
          │              │                │
   HTTPS/mTLS      HTTPS/mTLS       HTTPS/mTLS
          │              │                │
 [Ingress + Argo CD] [Ingress + Argo CD] [Ingress + Argo CD]
   AWS EKS (CPU)        GCP GKE (CPU)       Azure AKS (CPU)
      │                    │                  │
 [llama.cpp pods]    [llama.cpp pods]   [llama.cpp pods]
  (gguf models)        (gguf models)       (gguf models)
      │                    │                  │
 [Prom + Exporter]  [Prom + Exporter]  [Prom + Exporter]
      └───────────────metrics + costs─────────────┘
                         ↓
                 [Router cost engine]
```

### The Core Components

**Intelligent Router (Go):** The heart of the system handles real-time cost calculation using the formula `(node_hourly_cost / (tokens_per_sec * 3600)) * overhead_factor * 1000`, along with health monitoring that enforces SLA requirements like latency and queue depth. It uses HMAC and mTLS authentication for security, collects Prometheus metrics for observability, and implements sticky routing to prevent flapping between providers.

**Multi-Cloud Infrastructure (Pulumi):** The infrastructure layer manages AWS EKS with optimized node groups (t3.large instances for cost efficiency), plus ready-to-deploy GCP GKE and Azure AKS configurations. Everything follows consistent networking, security, and naming patterns across clouds, with automated DNS and TLS certificate management.

**GitOps Deployment (ArgoCD):** For deployment, I'm using ArgoCD with an app-of-apps pattern to manage multiple clusters, automated deployments with self-healing capabilities, environment-specific configurations via Kustomize, and platform components like ingress-nginx, cert-manager, and prometheus.

**CPU-Optimized LLM Serving:** The LLM serving layer runs llama.cpp with quantized GGUF models, uses PVC for model caching (download once per node), supports auto-scaling with scale-to-zero capabilities, and includes comprehensive metrics collection.

## Technology Choices and Learning Goals

### Why Go?
Go has become my favorite programming language for several reasons. The concurrency model is perfect for a router handling many simultaneous requests, the static typing catches errors at compile time, compilation is fast which makes iteration during development much quicker, the ecosystem has fantastic libraries for HTTP, metrics, and cloud APIs, and deployment is simple with a single binary and no dependencies.

### Why Pulumi?
Coming from Terraform, I was excited to try Pulumi because you can use a real programming language (Go in this case) instead of HCL, get type safety with IDE support and compile-time checking, use familiar patterns and existing Go knowledge and libraries, and write better tests using real Go testing frameworks.

### Why ArgoCD?
My previous experience with ArgoCD was limited, so this project was perfect for learning GitOps best practices around declarative infrastructure management, multi-cluster management with a single pane of glass for all environments, application lifecycle management with automated deployments and rollbacks, and security features like RBAC and audit trails.

## What I Built

### Project Foundation & Infrastructure
I started with proper Go module structure and comprehensive documentation covering multi-cloud architecture overview, cost calculation methodology, and development and deployment guides. Then I built reusable components for consistent cloud deployments including resource naming conventions, kubeconfig generation for all three cloud providers, and standardized tagging and labeling.

### AWS Implementation & Router Core  
The AWS infrastructure implementation includes full EKS deployment with VPC and networking optimized for cost, node groups using t3.large instances, IAM roles and security policies, and automated ArgoCD installation.

The intelligent router core became the heart of the system with:
- Cost calculation engine for real-time $/1K token calculations
- Health monitoring with SLA enforcement and circuit breaker patterns  
- Request forwarding with streaming support and authentication
- Comprehensive Prometheus metrics for observability

### Deployment & Developer Experience
I created production-grade Kubernetes deployments with an llm-server chart for llama.cpp with model caching and auto-scaling, a platform chart for core infrastructure (ingress, monitoring, certificates), and cloud-specific values optimized for each provider's services.

The GitOps configuration includes complete ArgoCD setup with app-of-apps pattern for scalability, environment-specific overlays, and automated sync policies with self-healing. I also built model performance and cost documentation, a GitHub Actions pipeline with testing and security scanning, and automated Docker image building and deployment.

To make it easy to contribute and deploy, I focused on comprehensive development documentation, interactive setup scripts with a clean UI, and multiple deployment options (local, cloud, development). The setup automation supports one-command deployment with options for local demo testing, full AWS deployment, and development environment setup.

## The Magic: Cost-Aware Routing

The core innovation is the real-time cost calculation that considers: `costPer1K = (nodeHourlyCost / (tokensPerSecond * 3600)) * overheadFactor * 1000`

Here's how it works with real numbers. An AWS t3.large costs $0.0928/hour and delivers about 15 tokens per second, which works out to roughly $0.0017 per 1K tokens. A GCP n1-standard-2 costs $0.0950/hour with 12 TPS, coming to about $0.0022 per 1K tokens. An Azure Standard_D2s_v3 costs $0.0968/hour with 14 TPS, working out to about $0.0019 per 1K tokens.

In this scenario, the router automatically selects AWS, potentially saving 10-20% on inference costs. When you're processing millions of tokens, those savings add up fast.

## Where Things Stand

**Current Status: Development Phase** - The system is working locally with AWS infrastructure provisioned. Cloud deployment across all three providers is the next major milestone.

### Working System
The router compiled successfully and is running locally. Health monitoring is detecting cluster status, API endpoints are responding correctly locally, Prometheus metrics are being collected, the cost engine is ready for real workloads, and AWS infrastructure is fully provisioned and tested.

### Production Architecture  
The production architecture is complete with infrastructure as code using Pulumi, a GitOps deployment pipeline with ArgoCD, professional Helm charts, and comprehensive monitoring and observability.

### Multi-Cloud Foundation
The multi-cloud foundation has AWS infrastructure fully implemented and working, with GCP and Azure patterns established, consistent tooling and naming across clouds, and everything ready for global deployment in the next phase.

## Performance and Cost Expectations

Based on the architecture and testing, TinyLlama 1.1B on t3.large instances should deliver around 15 tokens per second at roughly $0.0017 per 1K tokens, with latency under 1 second for short prompts and 99.9%+ availability with multi-cloud redundancy.

The scale-to-zero benefits are significant: pods scale down to 0 during low usage, models are cached in PVC so there's no re-download cost, and clusters can auto-scale nodes to minimum when not needed.

## Lessons Learned

Go really is fantastic for infrastructure tools. The concurrency model and standard library made building the router straightforward, and I'm convinced it was the right choice. Pulumi's type safety turned out to be a game-changer – catching configuration errors at compile time saved hours of debugging that I would have spent with Terraform. ArgoCD scales beautifully, and the app-of-apps pattern makes managing multiple clusters intuitive. CPU inference is surprisingly cost-effective when you use quantized models properly.

From a project management perspective, making incremental commits that tell a story made the project much more maintainable. Writing comprehensive documentation helped clarify the architecture in my own mind. And investing time in setup automation was absolutely worth it – the interactive scripts make the project accessible to new contributors.

## What's Next

The foundation is solid and ready for expansion. The immediate priorities are:

**Phase 1: Complete Cloud Deployment**
- Deploy the working system to AWS, GCP, and Azure clusters
- Validate the cost-aware routing across all three providers

**Phase 2: Production Features**
- Add more sophisticated models like Phi-3 and Llama 2 for production workloads
- Implement circuit breaker patterns for improved reliability
- Add request queueing for handling traffic spikes
- Build cost dashboards in Grafana for financial monitoring
- Implement A/B testing capabilities for model experimentation

## From Learning Project to Production System

What started as a way to learn new technologies is becoming a production-ready system that could save significant money for organizations running LLM workloads at scale. The combination of Go's performance, Pulumi's type safety, ArgoCD's GitOps capabilities, and multi-cloud redundancy creates a powerful platform for cost-optimized AI inference.

The project demonstrates that with the right architecture and tooling, you can build sophisticated infrastructure that's both cost-effective and highly available. While still in active development, the foundation is solid and the local testing validates the core concepts.

This has been an incredible journey from a simple self-hosted LLM on Hetzner to a (soon-to-be) global, multi-cloud AI infrastructure platform. The next chapter involves completing the cloud deployment and scaling to production workloads.

---

*The complete source code and documentation is available at: [github.com/navillasa/multi-cloud-llm-router](https://github.com/navillasa/multi-cloud-llm-router)*
