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
                <p>DevOps Engineer with 3+ years of production Kubernetes and cloud infrastructure experience, returning to tech after a brief adventure in advertising. I combine deep technical skills in cloud-native technologies with strong communication abilities.</p>
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
                <h3 class="project-title">📺 TV Hub</h3>
                <div class="project-links">
                    <a href="https://github.com/navillasa/tv-dashboard-k8s" target="_blank" class="project-link">GitHub</a>
                    <a href="http://tv-hub.navillasa.dev" target="_blank" class="project-link">Live Demo</a>
                </div>
            </div>
            <p class="project-description">
                A production-ready TV show dashboard showcasing enterprise DevOps practices. While the app is intentionally simple (aggregating trending shows), the infrastructure demonstrates GitOps, observability, and cloud-native architecture patterns.
            </p>
            <div class="tech-stack">
                <span class="tech-tag">Terraform</span>
                <span class="tech-tag">Kubernetes</span>
                <span class="tech-tag">ArgoCD</span>
                <span class="tech-tag">Prometheus</span>
                <span class="tech-tag">GCP</span>
                <span class="tech-tag">Docker</span>
                <span class="tech-tag">Node.js</span>
                <span class="tech-tag">PostgreSQL</span>
                <span class="tech-tag">React</span>
            </div>
            <div class="live-dashboard">
                <h4 class="blog-section-title">🚀 Live Dashboard:</h4>
                <ul class="blog-list">
                    <li><a href="https://monitoring.navillasa.dev/d/e0c978bd-6077-403e-ab3b-ba03f4b34962/tv-hub-business-intelligence-dashboard" target="_blank" class="project-link dashboard-link">Business Intelligence Dashboard</a></li>
                </ul>
                <p class="dashboard-note">Interactive monitoring with streaming analytics (demo/password)</p>
            </div>
            <div class="blog-posts">
                <h4 class="blog-section-title">Related Blog Posts:</h4>
                <ul class="blog-list">
                    <li><a href="{{ '/blog/tv-hub-project-overview/' | relative_url }}" class="blog-link">Building Production-Grade Infrastructure for a Simple App</a></li>
                    <li><a href="{{ '/blog/gitops-cicd-pipeline/' | relative_url }}" class="blog-link">The CI/CD Pipeline I Wish I'd Built Sooner</a></li>
                    <li><a href="{{ '/blog/debugging-502-errors/' | relative_url }}" class="blog-link">The Cluster Doctor, or How I Learned to Stop Worrying and Debug 502s</a></li>
                    <li><a href="{{ '/blog/vault-gitops/' | relative_url }}" class="blog-link">Why I Didn't Make Vault an ArgoCD Application</a></li>
                </ul>
            </div>
        </div>

        <!-- Self-Hosted LLM Project -->
        <div class="project-card">
            <div class="project-header">
                <h3 class="project-title">🧠 Self-Hosted Mini LLM API</h3>
                <div class="project-links">
                    <a href="https://github.com/navillasa/self-hosted-mini-llm" target="_blank" class="project-link">GitHub</a>
                    <a href="https://llm.navillasa.dev" target="_blank" class="project-link">Live Demo</a>
                </div>
            </div>
            <p class="project-description">
                A lightweight, self-hosted LLM server using GPT4All, running entirely on CPU. Demonstrates infrastructure provisioning, containerization, and secure API deployment with HTTPS and authentication.
            </p>
            <div class="tech-stack">
                <span class="tech-tag">Python</span>
                <span class="tech-tag">FastAPI</span>
                <span class="tech-tag">Docker</span>
                <span class="tech-tag">Terraform</span>
                <span class="tech-tag">Traefik</span>
                <span class="tech-tag">GPT4All</span>
                <span class="tech-tag">Hetzner Cloud</span>
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
