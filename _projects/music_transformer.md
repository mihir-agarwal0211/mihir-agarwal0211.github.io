---
layout: page
title: Music Transformer
description: Comparing Vanilla Attention vs. Relative Attention for MIDI generation.
img: assets/img/music_transformer.png
importance: 1
category: work
selected: true
related_publications: false
---

**Abstract**
Generating music with long-term structure is a challenging task for standard deep learning models. In this project, I reproduced the [Music Transformer](https://arxiv.org/abs/1809.04281) architecture to generate coherent MIDI sequences.

### 1. Model Architecture
My implementation modifies the standard Transformer Decoder. Instead of using absolute positional embeddings (which struggle with relative distance), I injected relative position information directly into the attention mechanism.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/music_transformer_architecture.jpg" title="Model Architecture" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The architecture uses a stack of 6 Decoder layers with <strong>Skewed Relative Attention</strong> to process MIDI events.
</div>

### 2. The Core Innovation: Relative Attention
Standard Transformers use "Absolute Positional Embeddings," which means they treat a melody played at the start of a song as mathematically different from the same melody played later. This makes it hard to generate repeating musical themes (motifs).

To solve this, I implemented the "Skewing" mechanism, allowing the model to focus on *distance* rather than *position*.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/attention_analysis.png" title="Attention Analysis" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    <strong>Left:</strong> Standard Attention learns fixed grid-like positions. <br>
    <strong>Right:</strong> My Relative Attention learns <strong>diagonal bands</strong>, proving it captures relative distance (rhythm) regardless of position.
</div>

### Key Contributions
* **Relative Attention:** Implemented the relative attention mechanism from scratch in PyTorch to capture timing and rhythm.
* **Memory Optimization:** Used the "Skewing" algorithm to reduce memory complexity from $O(L^2D)$ to $O(L^2)$.
* **Infrastructure:** Trained on the MAESTRO dataset using 4x NVIDIA A100 GPUs.

### Resources
* [<i class="fas fa-file-pdf"></i> View Project Report](/assets/pdf/music_transformer_report.pdf){: .btn .btn-outline-primary .mr-2 }
* [<i class="fab fa-github"></i> View Code](https://github.com/mihir-agarwal0211/music-transformer){: .btn .btn-outline-primary }