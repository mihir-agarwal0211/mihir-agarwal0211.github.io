---
layout: page
title: NeuroLOB
description: Generative Market Intelligence using Neural Point Processes & Diffusion.
img: assets/img/neurolob_architecture.png
importance: 1
category: work
---

<div class="row justify-content-center mb-4">
    <div class="col-md-8 text-center">
        <p class="lead">
            A neuro-symbolic framework for generating high-fidelity financial market data.
        </p>
        <a href="/neurolob-demo/" target="_blank" class="btn btn-primary btn-lg z-depth-1">
            <i class="fas fa-rocket mr-2"></i> Launch Live System
        </a>
        <p class="text-muted mt-2" style="font-size: 0.8rem;">
            *Opens the interactive inference engine in a new full-screen tab.*
        </p>
    </div>
</div>

<hr>

### System Architecture
To bring this research model to the web, I implemented a **Hybrid Cloud Architecture**:
* **Frontend:** Static portfolio hosted on **GitHub Pages**.
* **Backend:** Containerized inference engine hosted on **Hugging Face Spaces**.
* **Model:** The `DiffusionPipeline` runs on a custom **PyTorch** backend.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/neurolob_architecture.png" title="Model Architecture" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<hr>

**Abstract**
Financial microstructure data (Limit Order Books) is event-driven and irregular. **NeuroLOB** is a neuro-symbolic framework integrating **Neural Point Processes (NPP)** with **Diffusion Models** to generate high-fidelity synthetic market data.

### Key Innovations
* **Continuous Time Encoding:** Implemented **Rotary Positional Embeddings (RoPE)** to inject continuous time information directly into the attention mechanism.
* **Diffusion-Based Generation:** Used a conditional DDPM to capture the multi-modal distribution of price returns.
* **Physics-Informed Regularization:** Enforced financial stylized facts (fat tails and volatility clustering) using a GARCH(1,1) post-processing layer.

### Resources
* [<i class="fas fa-file-pdf"></i> Read Report](/assets/pdf/neurolob_report.pdf){: .btn .btn-outline-primary .mr-2 }
* [<i class="fas fa-chart-line"></i> View Poster](/assets/pdf/neurolob_poster.pdf){: .btn .btn-outline-primary .mr-2 }
* [<i class="fab fa-github"></i> View Source Code](https://github.com/mihir-agarwal0211/neurolob){: .btn .btn-outline-primary }