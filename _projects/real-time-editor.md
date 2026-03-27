---
layout: page
title: Real-Time Collaborative Code Editor
description: A low-latency distributed system for live coding interviews with AI assistance. <a href="/real-time-code-editor-demo/" target="_blank">Live Demo</a>
img: assets/img/real-time-code-editor.png
importance: 1
category: work
related_publications: false
github: https://github.com/mihir-agarwal0211/Real-Time-Code-Editor
selected: true
---

<style>
    /* Wide container for the project page */
    @media (min-width: 1200px) {
        .container { max-width: 1400px !important; }
    }
    
    /* Ensure the Title area can hold our button nicely */
    .post-title {
        display: flex;
        justify-content: space-between;
        align-items: center;
        flex-wrap: wrap; 
    }
</style>

<div id="editor-action-btn" class="text-center mb-4">
    <a href="/real-time-code-editor-demo/" target="_blank" class="btn btn-primary z-depth-1">
        <i class="fas fa-code mr-2"></i> Launch Live Editor
    </a>
</div>

<script>
document.addEventListener("DOMContentLoaded", function() {
    var btn = document.getElementById("editor-action-btn");
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

<div class="row justify-content-center"> 
    <div class="col-sm-6 mt-3 mt-md-0"> 
        {% include figure.liquid loading="eager" path="assets/img/real-time-code-editor.png" title="Editor Interface" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The live coding interface supporting multi-user synchronization, AI debugging, and code execution.
</div>

## Overview

This project is a **low-latency collaborative coding platform** designed to mimic Google Docs for code. It solves the challenge of synchronizing state across multiple clients in real-time while allowing for secure remote code execution and AI-driven assistance.

## Technical Architecture

The system mimics a distributed architecture common in high-frequency trading or gaming servers, prioritizing speed and consistency.

* **Frontend:** React.js with Monaco Editor (VS Code engine). It uses optimistic UI updates to ensure typing feels instant, even with network latency.
* **Backend:** Python **FastAPI** coupled with **WebSockets**. I chose FastAPI over Django/Flask for its asynchronous capabilities (`async/await`), which allows handling thousands of concurrent connections.
* **AI Integration:** **Google Gemini API** is integrated directly into the backend to parse code context and generate fix suggestions or optimizations on demand.
* **Synchronization:** Implemented a broadcast pattern where cursor positions and keystrokes are transmitted via WebSockets and synchronized across all active clients in milliseconds.
* **Deployment:**
    * **Frontend:** Vercel (CDN edge network).
    * **Backend:** Render (Containerized Python environment).
    * **Database:** PostgreSQL (hosted on Neon) with SQLAlchemy.

## Key Features

1.  **Real-Time Synchronization:** Users can type simultaneously without race conditions.
2.  **AI-Powered Debugging:** Leveraging Google Gemini, the editor can analyze the current code buffer, identify syntax or logic errors, and suggest optimized refactors with a single click.
3.  **Live Cursor Tracking:** See exactly where other users are typing (multi-cursor support).
4.  **Remote Code Execution:** Securely sends code to the backend, executes it in an isolated Python environment, and streams stdout/stderr back to the client.

## Challenges & Learnings

The biggest engineering challenge was handling the **"Ghost User" problem** with WebSockets. When a user disconnected abruptly (closed tab), the server maintained the connection state. I implemented a robust cleanup protocol using WebSocket lifecycle events (`on_disconnect`) and a heartbeat mechanism to ensure the active user list remains accurate.