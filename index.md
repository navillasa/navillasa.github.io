---
                <span class="tech-tag">Prometheus</span>
layout: default
title: "Software / DevOps Engineer"
---

<div class="container">
    <!-- Header Section -->
    <header class="header">
        <div class="header-content">
            <div class="profile-section">
                <div class="profile-picture">
                    <img src="{{ '/assets/images/squarephoto.jpg' | relative_url }}" alt="Natalie Villasana" class="profile-image">
                </div>
                <div class="profile-info">
                    <h1 class="name">{{ site.author.name }}</h1>
                    <p class="title">Software / DevOps Engineer</p>
                    <p class="location">{{ site.author.location }} • {{ site.author.domain }}</p>
                </div>
            </div>
            <div class="contact-links">
                <a href="mailto:{{ site.author.email }}" class="contact-link">Email</a>
                <a href="https://github.com/{{ site.author.github }}" target="_blank" class="contact-link">GitHub</a>
                <a href="https://www.linkedin.com/in/{{ site.author.linkedin }}/" target="_blank" class="contact-link">LinkedIn</a>
            </div>
        </div>
    </header>

    <!-- About Section -->
    <section class="about">
        <div class="about-container">
            <h2 class="section-title">About</h2>
            <div class="about-content">
                <p>Software / DevOps Engineer with 5 years of production cloud infrastructure experience at Storj Labs. After exploring advertising and creative work, I'm returning to tech with renewed focus on modern practices including GitOps, observability, and infrastructure automation through hands-on projects.</p>
            </div>
        </div>
    </section>

    <!-- Projects Section -->
    <section class="projects">
        <h2 class="section-title">Featured Projects</h2>

        <!-- Homelab -->
        <div class="project-card">
            <div class="project-header">
                <h3 class="project-title">😶‍🌫️ Kubernetes Homelab with Proxmox & MicroK8s</h3>
                <div class="project-links">
                    <a href="https://github.com/navillasa/kubernetes-homelab" target="_blank" class="project-link">GitHub</a>
                </div>
            </div>
            <p class="project-description">
Self-hosted Kubernetes homelab built on a Dell Wyse 5070 thin client running Proxmox VE with virtualized infrastructure managed by Terraform. Built to prototype AI/LLM workloads, experiment with automation, and to refine infrastructure-as-code practices.
            </p>
            <div class="tech-stack">
                <span class="tech-tag">Kubernetes</span>
                <span class="tech-tag">Prometheus</span>
                <span class="tech-tag">ArgoCD</span>
            </div>
        </div>

        <!-- Multi-Cloud LLM Router Project -->
        <div class="project-card">
            <div class="project-header">
                <h3 class="project-title">🪼 Multi-Cloud LLM Router (API Gateway)</h3>
                <div class="project-links">
                    <a href="https://github.com/navillasa/multi-cloud-llm-router" target="_blank" class="project-link">GitHub</a>
                </div>
            </div>
            <p class="project-description">
                An AI gateway implementation that distributes LLM requests to the cheapest available cluster across external providers (OpenAI, Claude, Gemini) and LLMs self-hosted on Kubernetes clusters in AWS, GCP, and Azure. Routing based on cost, latency, and capability requirements. Features real-time cost calculation, health monitoring, and scale-to-zero capabilities.
            </p>
            <div class="live-dashboard">
                <h4 class="blog-section-title">🧊 Simulated Demo:</h4>
                <ul class="blog-list">
                    <li><a href="https://demo-multicloud.navillasa.dev" target="_blank" class="project-link dashboard-link">Router Dashboard</a></li>
                </ul>
                <p class="dashboard-note">Password: demo123</p>
            </div>
            <div class="project-overview">
                <p><strong>📋 Technical Deep-Dive:</strong> <a href="{{ '/blog/multi-cloud-llm-router-journey/' | relative_url }}" class="blog-link project-overview-link">Multi-Cloud Architecture & Cost Optimization</a></p>
            </div>
            <div class="tech-stack">
                <span class="tech-tag">Go</span>
                <span class="tech-tag">Pulumi</span>
                <span class="tech-tag">Kubernetes</span>
                <span class="tech-tag">Prometheus</span>
                <span class="tech-tag">ArgoCD</span>
                <span class="tech-tag">AWS EKS</span>
                <span class="tech-tag">GCP GKE</span>
                <span class="tech-tag">Azure AKS</span>
                <span class="tech-tag">OpenAI</span>
                <span class="tech-tag">Claude</span>
                <span class="tech-tag">Gemini</span>
            </div>
        </div>
        
        <!-- TV Hub Project -->
        <div class="project-card">
            <div class="project-header">
                <h3 class="project-title">📺 TV Dashboard on Kubernetes</h3>
                <div class="project-links">
                    <a href="https://github.com/navillasa/tv-dashboard-k8s" target="_blank" class="project-link">GitHub</a>
                    <a href="http://tv-hub.navillasa.dev" target="_blank" class="project-link">Live Demo</a>
                </div>
            </div>
            <p class="project-description">
                A full-stack dashboard using production-grade DevOps practices including GitOps with ArgoCD, observability with Prometheus and Grafana, secrets management with Vault, and CI/CD pipelines deployed on Google Kubernetes Engine. Built around a simple premise – tracking trending shows across streaming platforms – to demonstrate cloud-native architecture patterns.
            </p>

<!-- Commenting dead links for now
            <div class="live-dashboard">
                <h4 class="blog-section-title">🚀 Live Dashboard:</h4>
                <ul class="blog-list">
                    <li><a href="https://monitoring.navillasa.dev/d/fee614ea-a1d2-4efb-af86-2f4db349482a/tv-hub-business-intelligence-dashboard?orgId=1&refresh=5s" target="_blank" class="project-link dashboard-link">Business Intelligence Dashboard</a></li>
                </ul>
                <p class="dashboard-note">Interactive monitoring with streaming analytics</p>
            </div>
-->
            <div class="project-overview">
                <p><strong>📋 Technical Deep-Dive:</strong> <a href="{{ '/blog/go-big-stay-simple/' | relative_url }}" class="blog-link project-overview-link">Complete Architecture & Project Walkthrough</a></p>
            </div>
            <div class="tech-stack">
                <span class="tech-tag">Terraform</span>
                <span class="tech-tag">Kubernetes</span>
                <span class="tech-tag">ArgoCD</span>
                <span class="tech-tag">Prometheus</span>
                <span class="tech-tag">Vault</span>
                <span class="tech-tag">GCP</span>
                <span class="tech-tag">Docker</span>
                <span class="tech-tag">Node.js</span>
                <span class="tech-tag">PostgreSQL</span>
                <span class="tech-tag">React</span>
            </div>
        </div>

        <!-- Storj Auditing & Repair Project -->
        <div class="project-card">
            <div class="project-header">
                <h3 class="project-title">☁️  Storj V3 Auditing & Repair Systems</h3>
                <div class="project-links">
                    <a href="https://github.com/storj/storj" target="_blank" class="project-link">Open Source Repo</a>
                </div>
            </div>
            <p class="project-description">
              Key contributor to the design, development, and infrastructure of Storj's distributed cloud storage system from 2017 to 2022. My work spanned major improvements to auditing, data repair, monitoring, incident response, fault tolerance, and driving operational excellence across the team.
            </p>
            <div class="tech-stack">
                <span class="tech-tag">Go</span>
                <span class="tech-tag">Postgres</span>
                <span class="tech-tag">gRPC</span>
                <span class="tech-tag">Microservices</span>
                <span class="tech-tag">Kubernetes</span>
                <span class="tech-tag">Prometheus</span>
            </div>
            <div class="blog-posts">
                <h4 class="blog-section-title">Contribution Highlights</h4>
                <ul class="blog-list">
                    <li><a href="https://www.storj.io/blog/decentralized-auditing-and-repair-the-low-key-life-of-data-resurrection" class="blog-link">🌟 Blog Post: Decentralized Auditing & Repair Data Resurrection</a></li>
                    <li><a href="https://github.com/storj/storj/pull/2577" class="blog-link">satellite/gc: Implement garbage collection service on satellite</a></li>
                    <li><a href="https://github.com/storj/storj/pull/2888" class="blog-link">satellite/audit: Create the audit queue</a></li>
                </ul>
            </div>
        </div>
    </section>

    <!-- Blog Section -->
    <section class="blog-section">
        <h2 class="section-title">Recent Writing</h2>
        
        <h3 style="font-size: 1rem; font-weight: 600; color: #495057; margin-bottom: 1rem; margin-top: 0.5rem; padding-bottom: 0.5rem; border-bottom: 1px solid #e9ecef;">August 2025</h3>
        <ul class="blog-list">
            <li><a href="{{ '/blog/gitops-cicd-pipeline/' | relative_url }}" class="blog-link">The CI/CD Pipeline I Wish I'd Built Sooner</a></li>
            <li><a href="{{ '/blog/vault-gitops/' | relative_url }}" class="blog-link">Why I Didn't Make Vault an ArgoCD Application</a></li>
            <li><a href="{{ '/blog/debugging-502-errors/' | relative_url }}" class="blog-link">The Cluster Doctor, or How I Learned to Stop Worrying and Debug 502s</a></li>
            <li><a href="{{ '/blog/missed-ai-revolution/' | relative_url }}" class="blog-link">Late to the AI Party: Lessons from Building LLM Infrastructure</a></li>
        </ul>
        <br>
        <h3 style="font-size: 1rem; font-weight: 600; color: #495057; margin-bottom: 1rem; margin-top: 0.5rem; padding-bottom: 0.5rem; border-bottom: 1px solid #e9ecef;">September 2025</h3>
        <ul class="blog-list">
            <li><a href="{{ '/blog/why-python-dominates-ai/' | relative_url }}" class="blog-link">Why Python Dominates AI (And How to Build Stronger Projects Even If You’re Not Training Models)</a></li>
        </ul>
    </section>

    <!-- Footer -->
    <footer class="footer">
        <div class="footer-links">
            <a href="https://github.com/{{ site.author.github }}" target="_blank">GitHub</a> • 
            <a href="https://www.linkedin.com/in/{{ site.author.linkedin }}/" target="_blank">LinkedIn</a> • 
            <a href="mailto:{{ site.author.email }}">{{ site.author.email }}</a>
        </div>
    </footer>
</div>
