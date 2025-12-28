---
layout: about
title: about
permalink: /
subtitle: >
  MS Data Science @ <a href="https://www.columbia.edu">Columbia University</a> • 
  Previously: <a href="https://www.shell.com">Shell</a> / <a href="https://www.linkedin.com/company/vidrona-ltd/">Vidrona</a> / <a href = "https://www.isep.fr/en/research-at-isep/">ISEP</a> • 
  learn ⇄ implement ⇄ optimize
profile:
  align: right
  image: prof_pic.jpg
  image_circular: false
  more_info: >
    <p>New York, NY</p>
    <p>ma4874@columbia.edu</p>

selected_papers: true 
selected_projects: true
news: false
social: true 

announcements:
  enabled: false 
  scrollable: true 
  limit: 5 

latest_posts:
  enabled: false 
  scrollable: true
  limit: 3 
---
Hello! Welcome to my personal archive. 👋

I am a Master’s student at **[Columbia University](https://www.columbia.edu/)**, focusing on the intersection of **Deep Learning** and **Systems Engineering**. My goal is to build systems that are not only theoretically sound but computationally efficient at scale.

My recent research centers on efficient generative modeling. Currently, I am developing **[neuro-symbolic frameworks](/projects/neurolob/)** that integrate **Neural Point Processes** with **Diffusion Models** to capture complex continuous-time dynamics.

### Professional Background
I approach research with a strong engineering discipline, honed during my three years as a **Software Engineer at [Shell](https://www.shell.com/)**. There, I engineered ML-driven automation pipelines and optimized large-scale testing systems, successfully reducing execution overhead by 35%.

My research journey began at **[ISEP (Paris)](https://en.isep.fr/)**, where I co-authored a **[Springer Journal](https://doi.org/10.1007/s11042-023-16399-2)** paper on ML based resource management for distributed systems (Fog Computing). I also have experience deploying computer vision models for industrial drone inspections at **[Vidrona (London)](https://vidrona.com/)**.

### What's Next
I am actively looking to apply my engineering experience to theoretical challenges. I am also open to industrial opportunities for **Summer 2026**.

I am always open to discussing technical challenges or potential [collaborations](mailto:ma4874@columbia.edu).

{% if page.selected_projects %}
  <h2>Selected Projects</h2>
  <div class="projects">
    <div class="table-responsive">
      <table class="table table-sm table-borderless">
      {% for project in site.projects %}
        {% if project.selected %}
        <tr>
          <th scope="row" style="width: 25%">
            {% if project.img %}
              <img class="img-fluid z-depth-1 rounded" src="{{ project.img | relative_url }}" alt="{{ project.title }}">
            {% endif %}
          </th>
          <td>
            <a href="{{ project.url | relative_url }}">{{ project.title }}</a>
            <br>
            {{ project.description }}
          </td>
        </tr>
        {% endif %}
      {% endfor %}
      </table>
    </div>
  </div>
{% endif %}

<h2>Experience</h2>
<div class="table-responsive">
  <table class="table table-borderless table-sm">
    
    <tr>
      <th scope="row" style="width: 25%; vertical-align: middle; text-align: center;">
        <img src="{{ '/assets/img/shell.png' | relative_url }}" style="max-width: 400px; width: 100%; height: auto; border-radius: 5px;">
      </th>
      <td>
        <strong>Shell</strong> (Bengaluru, India)<br>
        <em>Software Engineer</em> &nbsp; <span style="font-size: 0.85rem; color: #666;">(Aug 2022 - Aug 2025)</span>
        <ul>
            <li>Built an AI-powered HR Chatbot (RAG, LangChain) saving $102k in annualized costs.</li>
            <li>Developed ML-driven test prioritization tools, reducing execution time by 35%.</li>
            <li>Engineered robust, scalable software solutions for enterprise deployment.</li>
        </ul>
      </td>
    </tr>

    <tr>
      <th scope="row" style="width: 25%; vertical-align: middle; text-align: center;">
        <img src="{{ '/assets/img/Isep.png' | relative_url }}" style="max-width: 400px; width: 100%; height: auto; border-radius: 5px;">
      </th>
      <td>
        <strong>ISEP</strong> (Paris)<br>
        <em>Researcher</em> &nbsp; <span style="font-size: 0.85rem; color: #666;">(Jan 2022 - Aug 2022)</span>
        <p>Co-authored Springer paper on ML-based resource management to optimize Fog Computing latency.</p>
      </td>
    </tr>

    <tr>
      <th scope="row" style="width: 15%; vertical-align: middle; text-align: center;">
        <img src="{{ '/assets/img/Vidrona.png' | relative_url }}" style="max-width: 400px; width: 100%; height: auto; border-radius: 5px;">
      </th>
      <td>
        <strong>Vidrona</strong> (London)<br>
        <em>Machine Learning Intern</em> &nbsp; <span style="font-size: 0.85rem; color: #666;">(July 2020 - Aug 2022)</span>
        <p>Deployed YOLO/Faster R-CNN models for automated inspections, saving 300+ manual hours weekly.</p>
      </td>
    </tr>

  </table>
</div>
<hr>