---
layout: post
title: "The CI/CD Pipeline I Wish I'd Built Sooner"
subtitle: "The Joys of Building a GitOps Pipeline That Actually Works"
date: 2025-08-19
categories: [devops, kubernetes, gitops, ci-cd]
author: Natalie Villasana
---

When I started building my [TV Hub project]({% link _posts/2025-08-24-tv-hub-production-infrastructure.md %}), I did what most developers do: push to main and pray nothing breaks. Of course things did break, and I realized I needed something more sophisticated. Here's the GitOps pipeline I wish I'd built from day one.

## The Problem

My original setup was very simple and anxiety-inducingly fragile. Every git push triggered a full deployment to production. No gates, no testing environment, just vibes.

When a color-changing button broke the frontend one too many times, I realized I needed a system that could move fast without breaking things. The solution needed to automatically deploy tested code while preventing untested changes from reaching "production."

## The Solution: Two-Speed GitOps

I ended up with a hybrid approach that treats development and production very differently:

```
git push → GitHub Actions → new images → dev deploys automatically
                                      → prod requires manual promotion
```

Here's how it works:

**Development environment:** Every successful build auto-deploys. Fast feedback, immediate testing, maximum iteration speed.

**Production environment:** Requires explicit promotion of a tested version. Slower, deliberate, with human accountability.

## How the Pipeline Works

When I push code to main, GitHub Actions runs the full test suite, builds Docker images, and tags them with a date-based version like `v20250819-f3b8541`. If tests pass, it automatically updates the development Kubernetes manifests and pushes the change back to git.

ArgoCD watches the git repo and syncs any changes to the development cluster within about 30 seconds. I can immediately test the new version at the dev URL.

For production, there's no automatic deployment. Instead, I run a promotion script:

```bash
# See what versions are available
./scripts/promote-to-prod.sh

# Promote a tested version to production  
./scripts/promote-to-prod.sh v20250819-f3b8541
```

The script shows me exactly what will change, asks for confirmation, then updates the production manifests and pushes to git. ArgoCD syncs the change to production.

## Technical Choices

I made several specific decisions that shaped how this pipeline works:

**Date-based versioning:** Instead of incrementing numbers, I use `v$(date +%Y%m%d)-$(git-hash)`. This makes it obvious when a version was created and provides a direct link back to the source code. Much easier for operations than trying to remember what v1.47 contained.

**Kustomize overlays:** The same base Kubernetes manifests work for both environments, with environment-specific patches. Development gets relaxed resource limits and debug logging; production gets proper resource constraints, and theoretically should get structured logs.

**ArgoCD split configuration:** The development ArgoCD app has `automated: true` for immediate deployments. The production app has automated sync disabled, requiring manual intervention for every change.

**Container registry strategy:** Both environments pull from the same registry, just with different tags. This ensures what I test in dev is exactly what deploys to prod—no separate build processes or subtle differences.

## What I Could Have Done Differently

**Full automation:** I could have set up comprehensive integration tests and deployed to production automatically if everything passes. The tooling exists—Argo Rollouts for progressive delivery, sophisticated test suites, automated rollback triggers.

I chose manual promotion instead because I wanted deliberate production changes. This is my portfolio project after all! The slight overhead of manual promotion forces me to actually test changes in dev and think about the impact.

**Branch-based environments:** Many teams use feature branches for feature environments, develop branch for staging, and main branch for production. I went with a simpler model where main always goes to dev, and production gets explicit promotions.

The branch approach would have been more "textbook correct" but would have required more operational overhead managing multiple environments and branch policies. For a portfolio project, the current approach demonstrates the core GitOps concepts without unnecessary complexity.

**External tools:** I could have used Flux instead of ArgoCD, or Tekton instead of GitHub Actions, or Jenkins X for the whole pipeline. The GitHub Actions + ArgoCD combination is incredibly common in the industry, well-documented, and has good operational tooling.

## Results

The manual promotion gate adds maybe 2 minutes to the deployment process but provides huge peace of mind. I can deploy more frequently because I'm confident each change has been tested and validated.

For a team environment, I'd probably add Slack notifications for deployments and automated integration tests against the dev environment. But for a solo project, this pipeline hits the sweet spot of safety, speed, and simplicity.

The beauty of GitOps is that these patterns scale. The same basic structure works whether you're promoting manually like I do, or using sophisticated automated promotion with comprehensive test coverage. The deployment mechanism stays consistent—only the automation boundaries change.

---

*This pipeline powers the [TV Hub project](http://tv-hub.navillasa.dev) with full source available in the [GitHub repo](https://github.com/navillasa/tv-dashboard-k8s). You can see real deployment metrics in the [live monitoring dashboard](https://monitoring.navillasa.dev/d/e0c978bd-6077-403e-ab3b-ba03f4b34962/tv-hub-business-intelligence-dashboard).*
