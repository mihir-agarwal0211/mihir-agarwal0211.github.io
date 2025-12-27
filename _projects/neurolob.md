---
layout: page
title: NeuroLOB
description: Generative Market Intelligence using Neural Point Processes & Diffusion.
img: assets/img/neurolob_architecture.png
importance: 1
category: work
selected: true
---

<style>
    /* Wide container for the poster */
    @media (min-width: 1200px) {
        .container { max-width: 1400px !important; }
    }
    
    /* Ensure the Title area can hold our button nicely */
    .post-title {
        display: flex;
        justify-content: space-between;
        align-items: center;
        flex-wrap: wrap; /* Allows wrapping on smaller screens if needed */
    }
</style>

<div id="neurolob-action-btn" class="text-center mb-4">
    <a href="/neurolob-demo/" target="_blank" class="btn btn-primary z-depth-1">
        <i class="fas fa-rocket mr-2"></i> Launch Live System
    </a>
</div>

<script>
document.addEventListener("DOMContentLoaded", function() {
    var btn = document.getElementById("neurolob-action-btn");
    var title = document.querySelector(".post-title");
    
    // Function to move button based on screen size
    function positionButton() {
        if (!btn || !title) return;

        if (window.innerWidth >= 992) {
            // DESKTOP: Move button INTO the header
            title.appendChild(btn);
            
            // Adjust styles for header
            btn.classList.remove("text-center", "mb-4"); // Remove centering
            btn.style.marginTop = "0";
            btn.style.marginLeft = "auto"; // Push to far right
        } else {
            // MOBILE: Move button back to the top of the content body
            var contentStart = document.querySelector(".post-content");
            if (contentStart) {
                contentStart.insertBefore(btn, contentStart.firstChild);
                
                // Restore mobile styles
                btn.classList.add("text-center", "mb-4");
                btn.style.marginLeft = "0";
            }
        }
    }

    // Run on load
    positionButton();
    
    // Run whenever user resizes the window
    window.addEventListener('resize', positionButton);
});
</script>

<div class="row mb-5">
    <div class="col-12">
        <embed 
            src="/assets/pdf/neurolob_poster.pdf#view=FitH&toolbar=0&navpanes=0&scrollbar=0" 
            type="application/pdf" 
            width="100%" 
            height="1100px" 
            style="border: 1px solid #333; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.3);">
        
        <div class="text-center mt-2 d-block d-md-none">
            <a href="/assets/pdf/neurolob_poster.pdf" target="_blank" class="btn btn-sm btn-outline-secondary">
                <i class="fas fa-file-pdf"></i> View Poster PDF
            </a>
        </div>
    </div>
</div>

<hr>

<div class="row justify-content-center">
    <div class="col-lg-9 col-md-10" markdown="1">

**Abstract** Financial microstructure data (Limit Order Books) is event-driven and irregular. **NeuroLOB** is a neuro-symbolic framework integrating **Neural Point Processes (NPP)** with **Diffusion Models** to generate high-fidelity synthetic market data.

### System Architecture
To bring this research model to the web, I implemented a **Hybrid Cloud Architecture**:
* **Frontend:** Static portfolio hosted on **GitHub Pages**.
* **Backend:** Containerized inference engine hosted on **Hugging Face Spaces**.
* **Model:** The `DiffusionPipeline` runs on a custom **PyTorch** backend.

{% include figure.liquid loading="lazy" path="assets/img/neurolob_architecture.png" title="Model Architecture" class="img-fluid rounded z-depth-1 mt-3 mb-3" %}

### Key Innovations
* **Continuous Time Encoding:** Implemented **Rotary Positional Embeddings (RoPE)** to inject continuous time information directly into the attention mechanism.
* **Diffusion-Based Generation:** Used a conditional DDPM to capture the multi-modal distribution of price returns.
* **Physics-Informed Regularization:** Enforced financial stylized facts (fat tails and volatility clustering) using a GARCH(1,1) post-processing layer.

### Resources
* [<i class="fas fa-file-pdf"></i> Read Report](/assets/pdf/neurolob_report.pdf){: .btn .btn-outline-primary .mr-2 }
* [<i class="fab fa-github"></i> View Source Code](https://github.com/mihir-agarwal0211/neurolob){: .btn .btn-outline-primary }

</div>