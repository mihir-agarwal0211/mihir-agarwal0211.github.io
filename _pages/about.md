---
layout: about
title: about
permalink: /
subtitle: >
  MS Data Science @ <a href="https://www.columbia.edu">Columbia University</a> • 
  Previously: <a href="https://www.shell.com">Shell</a> / <a href="https://www.linkedin.com/company/vidrona-ltd/">Vidrona</a> / <a href = "https://www.isep.fr/en/research-at-isep/">ISEP</a> • 
  learn ⇄ implement ⇄ optimize
  <p>Bridging the gap between mathematical theory and high-performance implementation.</p>
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

Hi, thanks for stopping by! 👋

I am a Master’s student at **Columbia University**, focusing on the intersection of **Deep Learning** and **Systems Engineering**.

My research centers on efficient generative modeling. Currently, I am developing neuro-symbolic frameworks that integrate **Neural Point Processes** with **Diffusion Models** to capture complex continuous-time dynamics.

### Professional Background
I approach research with a strong engineering discipline, honed during my three years as a **Software Engineer at Shell**. There, I engineered ML-driven automation pipelines and optimized large-scale testing systems, successfully reducing execution overhead by 35%.

My research journey began at **ISEP (Paris)**, where I co-authored a **Springer Journal** paper on resource management for distributed systems (Fog Computing). I also have experience deploying computer vision models for industrial drone inspections at **Vidrona (London)**.

### What's Next
I am actively looking to apply my engineering experience to theoretical challenges. I am also open to industrial opportunities for **Summer 2026**.

I am always open to discussing technical challenges or potential collaborations.

{% if page.selected_projects %}
  <h2>Selected Projects</h2>
  <div class="projects">
    <div class="table-responsive">
      <table class="table table-sm table-borderless">
      {% for project in site.projects %}
        {% if project.selected %}
        <tr>
          <th scope="row" style="width: 20%">
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