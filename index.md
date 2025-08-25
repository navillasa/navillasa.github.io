---
layout: default
title: "DevOps Engineer"
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
                    <p class="title">DevOps Engineer</p>
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
                <p>DevOps Engineer with 5 years of production cloud infrastructure and development experience. I combine deep technical skills in cloud-native technologies with strong communication abilities.</p>
                <p>Previously built and scaled distributed cloud storage systems at Storj Labs. Currently expanding expertise in modern DevOps practices through hands-on projects featuring GitOps, observability, and infrastructure automation.</p>
            </div>
        </div>
    </section>

    <!-- Projects Section -->
    <section class="projects">
        <h2 class="section-title">Featured Projects</h2>
        
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

        <!-- Multi-Cloud LLM Router Project (In Progress) -->
        <div class="project-card">
            <div class="project-header">
                <h3 class="project-title">🪼 Multi-Cloud LLM Router <em>(In Progress)</em></h3>
                <div class="project-links">
                    <a href="https://github.com/navillasa/multi-cloud-llm-router" target="_blank" class="project-link">GitHub</a>
                </div>
            </div>
            <p class="project-description">
                An intelligent routing system that automatically distributes LLM requests to the cheapest available cluster across AWS, GCP, and Azure. Features real-time cost calculation, health monitoring, and scale-to-zero capabilities. Currently working locally with AWS infrastructure provisioned - cloud deployment in progress.
            </p>
            <div class="project-overview">
                <p><strong>📋 Technical Deep-Dive:</strong> <a href="{{ '/blog/multi-cloud-llm-router-journey/' | relative_url }}" class="blog-link project-overview-link">Multi-Cloud Architecture & Cost Optimization</a></p>
            </div>
            <div class="tech-stack">
                <span class="tech-tag">Go</span>
                <span class="tech-tag">Pulumi</span>
                <span class="tech-tag">Kubernetes</span>
                <span class="tech-tag">ArgoCD</span>
                <span class="tech-tag">AWS EKS</span>
                <span class="tech-tag">GCP GKE</span>
                <span class="tech-tag">Azure AKS</span>
                <span class="tech-tag">llama.cpp</span>
                <span class="tech-tag">Prometheus</span>
            </div>
        </div>

        <!-- VPN Ad Blocker Project -->
        <div class="project-card">
            <div class="project-header">
                <h3 class="project-title">🛡️ VPN Ad Blocker</h3>
                <div class="project-links">
                    <a href="https://github.com/navillasa/vpn-ad-blocker" target="_blank" class="project-link">GitHub</a>
                </div>
            </div>
            <p class="project-description">
                A self-hosted WireGuard VPN combined with AdGuard Home for DNS-level ad blocking. Features automated setup scripts, secure configuration, and multi-device support with QR code generation.
            </p>
            <div class="tech-stack">
                <span class="tech-tag">WireGuard</span>
                <span class="tech-tag">AdGuard Home</span>
                <span class="tech-tag">Ubuntu</span>
                <span class="tech-tag">UFW</span>
                <span class="tech-tag">Bash</span>
                <span class="tech-tag">Hetzner Cloud</span>
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
