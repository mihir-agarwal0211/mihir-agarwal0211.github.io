---
layout: page
title: Agent Self-Improvement
description: A text-to-SQL agent that detects its own degradation and learns from its failures, no human in the loop.
img: assets/img/agent_self_improvement.png
importance: 1
category: work
related_publications: false
github: https://github.com/mihir-agarwal0211/agent-self-improvement
selected: true
---

<style>
    /* Header buttons, same pattern as the other project pages */
    .post-title {
        display: flex;
        justify-content: space-between;
        align-items: center;
        flex-wrap: wrap;
    }
    #asi-action-btns .btn { margin: 0.25rem; }

    .asi-meta { color: var(--global-text-color-light); font-size: 0.95rem; }

    /* Architecture diagram (inline SVG, follows light/dark theme) */
    .asi-diagram { margin: 1.5rem 0 0.5rem; }
    .asi-diagram svg { width: 100%; height: auto; display: block; }
    .asi-diagram text { fill: var(--global-text-color); font-family: inherit; }
    .asi-diagram .asi-muted { fill: var(--global-text-color-light); }
    .asi-diagram .asi-mono { font-family: SFMono-Regular, Menlo, Consolas, monospace; }
    .asi-diagram .asi-box { fill: var(--global-card-bg-color); stroke: var(--global-text-color-light); stroke-width: 1.5; }
    .asi-diagram .asi-mine { fill: var(--global-theme-color); fill-opacity: 0.08; stroke: var(--global-theme-color); stroke-width: 2.5; }
    .asi-diagram .asi-badge { fill: var(--global-theme-color); }
    .asi-diagram .asi-badge-text { fill: #fff; font-weight: 700; }
    .asi-diagram .asi-accent { fill: var(--global-theme-color); }
    .asi-diagram .asi-line { stroke: var(--global-text-color-light); stroke-width: 1.5; fill: none; }
    .asi-diagram .asi-feedback { stroke: var(--global-theme-color); stroke-width: 2; fill: none; }
    .asi-diagram .asi-dash { stroke: var(--global-text-color-light); stroke-width: 1.2; stroke-dasharray: 4 4; fill: none; }
    .asi-diagram .asi-head { fill: var(--global-text-color-light); }
    .asi-diagram .asi-head-accent { fill: var(--global-theme-color); }
    .asi-diagram .asi-label-bg { fill: var(--global-bg-color); }
    .asi-diagram .asi-log { fill: var(--global-code-bg-color); stroke: var(--global-text-color-light); stroke-width: 1.2; }

    /* Results */
    .asi-stat { border: 1px solid var(--global-divider-color); border-radius: 8px; padding: 1rem 0.75rem; text-align: center; height: 100%; }
    .asi-stat .asi-stat-value { font-size: 1.6rem; font-weight: 700; color: var(--global-theme-color); line-height: 1.2; }
    .asi-stat .asi-stat-label { font-size: 0.85rem; color: var(--global-text-color-light); margin-top: 0.25rem; }
    .asi-bars { margin: 1.25rem 0 0.5rem; }
    .asi-bar-row { display: flex; align-items: center; margin-bottom: 0.6rem; }
    .asi-bar-label { flex: 0 0 38%; padding-right: 0.75rem; font-size: 0.9rem; }
    .asi-bar-track { flex: 1; min-width: 0; display: flex; align-items: center; background: var(--global-divider-color); border-radius: 4px; height: 1.6rem; }
    .asi-bar-fill { height: 100%; border-radius: 4px; background: var(--global-text-color-light); opacity: 0.55; }
    .asi-bar-fill.asi-best { background: var(--global-theme-color); opacity: 1; }
    .asi-bar-value { flex: 0 0 auto; padding-left: 0.5rem; font-weight: 600; font-size: 0.9rem; }
    .asi-axis { display: flex; justify-content: space-between; margin-left: 38%; font-size: 0.75rem; color: var(--global-text-color-light); }
    @media (max-width: 575px) {
        .asi-bar-row { flex-wrap: wrap; }
        .asi-bar-label { flex: 0 0 100%; padding: 0 0 0.2rem 0; }
        .asi-bar-track { flex: 0 0 100%; }
        .asi-axis { margin-left: 0; }
    }
</style>

<div id="asi-action-btns" class="text-center mb-4">
    <a href="https://github.com/mihir-agarwal0211/agent-self-improvement" target="_blank" rel="noopener" class="btn btn-primary z-depth-1">
        <i class="fa-brands fa-github mr-2"></i> View on GitHub
    </a>
    <a href="https://github.com/loganrudd/agent-self-improvement" target="_blank" rel="noopener" class="btn btn-outline-primary">
        <i class="fa-solid fa-code-branch mr-2"></i> Original repo
    </a>
</div>

<script>
document.addEventListener("DOMContentLoaded", function() {
    var btn = document.getElementById("asi-action-btns");
    var title = document.querySelector(".post-title");

    function positionButton() {
        if (!btn || !title) return;
        if (window.innerWidth >= 992) {
            // DESKTOP: move the buttons into the header
            title.appendChild(btn);
            btn.classList.remove("text-center", "mb-4");
            btn.style.marginTop = "0";
            btn.style.marginLeft = "auto";
        } else {
            // MOBILE: keep them at the top of the content
            var contentStart = document.querySelector(".post-content") || document.querySelector(".post article");
            if (contentStart) {
                contentStart.insertBefore(btn, contentStart.firstChild);
                btn.classList.add("text-center", "mb-4");
                btn.style.marginLeft = "0";
            }
        }
    }

    positionButton();
    window.addEventListener("resize", positionButton);
});
</script>

<p class="asi-meta">
    AI Engineer World's Fair Hackathon 2026 (Cerebral Valley, San Francisco) · June 27, 2026 · 24 hours · <em>The Self-Improvement Stack</em> track · Team of four
</p>

## Architecture at a glance

<div class="asi-diagram d-none d-md-block">
<svg viewBox="0 0 1000 420" role="img" aria-labelledby="asi-arch-title asi-arch-desc" xmlns="http://www.w3.org/2000/svg">
  <title id="asi-arch-title">Agent Self-Improvement architecture</title>
  <desc id="asi-arch-desc">Spider queries flow into the Harness, which emits TelemetryRecords to the Detector. The Detector emits DriftEvents to Correction. Correction writes few-shot examples back into AgentConfig, which the Harness reads. Every stage appends to events.jsonl, which the Viewer turns into a recovery curve.</desc>
  <defs>
    <marker id="asi-arrow" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" class="asi-head"/></marker>
    <marker id="asi-arrow-accent" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" class="asi-head-accent"/></marker>
  </defs>
  <!-- feedback loop -->
  <path d="M890 60 V24 H250 V56" class="asi-feedback" marker-end="url(#asi-arrow-accent)"/>
  <rect x="390" y="12" width="360" height="24" class="asi-label-bg"/>
  <text x="570" y="29" text-anchor="middle" font-size="14" class="asi-accent">feedback → <tspan class="asi-mono">AgentConfig.few_shot_examples</tspan></text>
  <!-- source -->
  <rect x="5" y="90" width="95" height="60" rx="30" class="asi-box"/>
  <text x="52" y="116" text-anchor="middle" font-size="14" font-weight="600">Spider</text>
  <text x="52" y="134" text-anchor="middle" font-size="14" font-weight="600">queries</text>
  <path d="M100 120 H146" class="asi-line" marker-end="url(#asi-arrow)"/>
  <!-- harness -->
  <rect x="150" y="60" width="200" height="120" rx="8" class="asi-box"/>
  <text x="250" y="92" text-anchor="middle" font-size="18" font-weight="700">Harness</text>
  <text x="250" y="116" text-anchor="middle" font-size="13" class="asi-muted">agent runs on Spider,</text>
  <text x="250" y="134" text-anchor="middle" font-size="13" class="asi-muted">execution-accuracy eval</text>
  <text x="250" y="164" text-anchor="middle" font-size="12" class="asi-muted">Rohan</text>
  <path d="M350 120 H466" class="asi-line" marker-end="url(#asi-arrow)"/>
  <text x="410" y="110" text-anchor="middle" font-size="12" class="asi-mono">TelemetryRecord</text>
  <!-- detector -->
  <rect x="470" y="60" width="200" height="120" rx="8" class="asi-box"/>
  <text x="570" y="92" text-anchor="middle" font-size="18" font-weight="700">Detector</text>
  <text x="570" y="116" text-anchor="middle" font-size="13" class="asi-muted">windowed drift detection</text>
  <text x="570" y="134" text-anchor="middle" font-size="12" class="asi-muted asi-mono">WARMUP→NORMAL→DRIFTING</text>
  <text x="570" y="164" text-anchor="middle" font-size="12" class="asi-muted">Logan</text>
  <path d="M670 120 H786" class="asi-line" marker-end="url(#asi-arrow)"/>
  <text x="730" y="110" text-anchor="middle" font-size="12" class="asi-mono">DriftEvent</text>
  <!-- correction (mine) -->
  <rect x="790" y="60" width="200" height="120" rx="8" class="asi-mine"/>
  <rect x="908" y="48" width="76" height="22" rx="11" class="asi-badge"/>
  <text x="946" y="63" text-anchor="middle" font-size="11" class="asi-badge-text">my stage</text>
  <text x="890" y="92" text-anchor="middle" font-size="18" font-weight="700">Correction</text>
  <text x="890" y="116" text-anchor="middle" font-size="13" class="asi-muted">teacher generates +</text>
  <text x="890" y="134" text-anchor="middle" font-size="13" class="asi-muted">verifies SQL → few-shot</text>
  <text x="890" y="164" text-anchor="middle" font-size="12" class="asi-accent" font-weight="600">Mihir</text>
  <!-- event log -->
  <path d="M250 180 V246" class="asi-dash" marker-end="url(#asi-arrow)"/>
  <path d="M570 180 V246" class="asi-dash" marker-end="url(#asi-arrow)"/>
  <path d="M890 180 V246" class="asi-dash" marker-end="url(#asi-arrow)"/>
  <rect x="150" y="250" width="840" height="40" rx="6" class="asi-log"/>
  <text x="570" y="275" text-anchor="middle" font-size="14"><tspan class="asi-mono" font-weight="600">events.jsonl</tspan><tspan class="asi-muted">  ·  append-only event log, written by every stage</tspan></text>
  <path d="M570 290 V326" class="asi-line" marker-end="url(#asi-arrow)"/>
  <!-- viewer -->
  <rect x="440" y="330" width="260" height="80" rx="8" class="asi-box"/>
  <text x="570" y="360" text-anchor="middle" font-size="18" font-weight="700">Viewer</text>
  <text x="570" y="382" text-anchor="middle" font-size="13" class="asi-muted">events.jsonl → recovery curve</text>
  <text x="570" y="400" text-anchor="middle" font-size="12" class="asi-muted">Yiwen</text>
</svg>
</div>

<div class="asi-diagram d-block d-md-none">
<svg viewBox="0 0 360 800" role="img" aria-labelledby="asi-arch-title-m" xmlns="http://www.w3.org/2000/svg">
  <title id="asi-arch-title-m">Agent Self-Improvement architecture: Spider queries, Harness, Detector, Correction, feedback into AgentConfig, events.jsonl, Viewer</title>
  <defs>
    <marker id="asi-arrow-m" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" class="asi-head"/></marker>
    <marker id="asi-arrow-accent-m" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" class="asi-head-accent"/></marker>
  </defs>
  <rect x="130" y="5" width="140" height="44" rx="22" class="asi-box"/>
  <text x="200" y="32" text-anchor="middle" font-size="15" font-weight="600">Spider queries</text>
  <path d="M200 49 V81" class="asi-line" marker-end="url(#asi-arrow-m)"/>
  <!-- harness -->
  <rect x="80" y="85" width="240" height="110" rx="8" class="asi-box"/>
  <text x="200" y="115" text-anchor="middle" font-size="18" font-weight="700">Harness</text>
  <text x="200" y="139" text-anchor="middle" font-size="13" class="asi-muted">agent runs on Spider,</text>
  <text x="200" y="157" text-anchor="middle" font-size="13" class="asi-muted">execution-accuracy eval</text>
  <text x="200" y="182" text-anchor="middle" font-size="12" class="asi-muted">Rohan</text>
  <path d="M200 195 V251" class="asi-line" marker-end="url(#asi-arrow-m)"/>
  <rect x="210" y="214" width="110" height="20" class="asi-label-bg"/>
  <text x="212" y="228" font-size="12" class="asi-mono">TelemetryRecord</text>
  <!-- detector -->
  <rect x="80" y="255" width="240" height="110" rx="8" class="asi-box"/>
  <text x="200" y="285" text-anchor="middle" font-size="18" font-weight="700">Detector</text>
  <text x="200" y="309" text-anchor="middle" font-size="13" class="asi-muted">windowed drift detection</text>
  <text x="200" y="327" text-anchor="middle" font-size="12" class="asi-muted asi-mono">WARMUP→NORMAL→DRIFTING</text>
  <text x="200" y="352" text-anchor="middle" font-size="12" class="asi-muted">Logan</text>
  <path d="M200 365 V421" class="asi-line" marker-end="url(#asi-arrow-m)"/>
  <text x="212" y="398" font-size="12" class="asi-mono">DriftEvent</text>
  <!-- correction -->
  <rect x="80" y="425" width="240" height="110" rx="8" class="asi-mine"/>
  <rect x="252" y="413" width="76" height="22" rx="11" class="asi-badge"/>
  <text x="290" y="428" text-anchor="middle" font-size="11" class="asi-badge-text">my stage</text>
  <text x="200" y="455" text-anchor="middle" font-size="18" font-weight="700">Correction</text>
  <text x="200" y="479" text-anchor="middle" font-size="13" class="asi-muted">teacher generates + verifies</text>
  <text x="200" y="497" text-anchor="middle" font-size="13" class="asi-muted">SQL → few-shot examples</text>
  <text x="200" y="522" text-anchor="middle" font-size="12" class="asi-accent" font-weight="600">Mihir</text>
  <!-- feedback loop on the left -->
  <path d="M80 480 H30 V140 H76" class="asi-feedback" marker-end="url(#asi-arrow-accent-m)"/>
  <text x="22" y="310" text-anchor="middle" font-size="12" class="asi-accent" transform="rotate(-90 22 310)">feedback: AgentConfig.few_shot_examples</text>
  <!-- event log -->
  <path d="M200 535 V611" class="asi-dash" marker-end="url(#asi-arrow-m)"/>
  <text x="212" y="578" font-size="12" class="asi-muted">every stage appends</text>
  <rect x="60" y="615" width="280" height="56" rx="6" class="asi-log"/>
  <text x="200" y="639" text-anchor="middle" font-size="14" font-weight="600" class="asi-mono">events.jsonl</text>
  <text x="200" y="659" text-anchor="middle" font-size="12" class="asi-muted">append-only event log</text>
  <path d="M200 671 V701" class="asi-line" marker-end="url(#asi-arrow-m)"/>
  <!-- viewer -->
  <rect x="80" y="705" width="240" height="85" rx="8" class="asi-box"/>
  <text x="200" y="735" text-anchor="middle" font-size="18" font-weight="700">Viewer</text>
  <text x="200" y="757" text-anchor="middle" font-size="13" class="asi-muted">events.jsonl → recovery curve</text>
  <text x="200" y="778" text-anchor="middle" font-size="12" class="asi-muted">Yiwen</text>
</svg>
</div>

- **Frozen Pydantic contracts** between stages (`TelemetryRecord`, `DriftEvent`, `CorrectionAction`, `AgentConfig`). Each stage was built and tested in isolation against mock fixtures, then wired together by one orchestrator.
- **Append-only event log.** Every stage writes to `events.jsonl`; the Viewer only reads it.
- **The loop is data, not weights.** Feedback is concretely an edit to `AgentConfig.few_shot_examples`, a list that starts empty and grows as Correction appends learned examples. Nothing is fine-tuned, nothing is reverted, and no bigger model is swapped in.

## The problem

Production AI agents drift. The input distribution shifts, accuracy slides, and nobody notices until a user does. Most "self-improving agent" demos can't tell a genuinely bad run from noise, and few check whether the improvement survives a real test.

In 24 hours our team of four built a self-correcting text-to-SQL agent that detects its own degradation, learns from its failures, and holds the improvement to a real statistical bar. I owned the Correction stage: the part that turns a detected failure into something the agent actually learns from.

## The architecture

Four typed stages with frozen Pydantic contracts between them, over an append-only event log. Harness runs the agent on Spider questions and emits `TelemetryRecord`s. Detector consumes those and emits `DriftEvent`s. Correction (mine) has a stronger teacher model generate and verify SQL to mint few-shot examples. Viewer turns the event log into a recovery curve. The feed starts on easy questions, then shifts at a change-point to hard and extra-hard ones: the detector catches the drop, Correction turns the agent's own failures into examples, and the agent recovers on hard questions it has never seen.

## What was hard, and what I decided

**Corrections you can trust.** A teacher model's output is a guess, not a label. For each failing case, the teacher (MiniMax-M3) generates corrected SQL from the question and the database schema. I accept it only if it **executes to the correct result set against the gold query** (the Spider execution-accuracy metric). If it doesn't, the teacher SQL is discarded and the gold SQL is used instead. Teacher quality affects yield, not correctness: every example that reaches the agent is known to be right.

**Not overfitting to the drift window.** The easy way to "improve" is to teach the agent the exact questions it will be graded on. Examples are stratified out-of-sample **by database**: hard questions are split into a disjoint LEARN pool, the only source of examples, and a HELD-OUT pool that serves as the benchmark. The agent can't regurgitate an example it was handed.

The second risk is forgetting. Filling the prompt with hard multi-join queries can break easy queries the agent already got right, so every correction also carries a few **anti-forgetting anchors** (easy successes). It held: of the 7 held-out questions whose outcome changed, **7 improved and 0 regressed**.

**A test that actually means something.** If the base model already knows the answers, "learning" is just prompt luck. We deliberately ran a weak base agent (MiniMax-M2.7-highspeed) against a stronger teacher, so the base genuinely struggles on hard SQL and any gain has to come from what it learned from its own failures.

**The rest of the loop.** The other stages are my teammates' work. Logan's detector is a windowed `WARMUP → NORMAL → DRIFTING` state machine that fires only when the windowed mean stays below baseline for several consecutive records, and filters transient API outages so they can't fake drift. Rohan's harness streams the change-point feed with execution-based telemetry. Yiwen's FastAPI + Chart.js viewer renders the recovery curve live from the event log.

## Results

In one unattended run the detector fired at the change-point (severity **0.295**, windowed accuracy **0.48** vs a **0.775** baseline), Correction synthesized **10 few-shot examples** (3 teacher-verified, 5 gold-fallback, 2 anti-forgetting anchors), and the agent recovered.

<div class="row mt-4">
    <div class="col-6 col-md-3 mb-3"><div class="asi-stat"><div class="asi-stat-value">+0.267</div><div class="asi-stat-label">hard-bucket accuracy gain</div></div></div>
    <div class="col-6 col-md-3 mb-3"><div class="asi-stat"><div class="asi-stat-value">p = 0.016</div><div class="asi-stat-label">paired McNemar exact test</div></div></div>
    <div class="col-6 col-md-3 mb-3"><div class="asi-stat"><div class="asi-stat-value">7 / 0</div><div class="asi-stat-label">questions improved / regressed</div></div></div>
    <div class="col-6 col-md-3 mb-3"><div class="asi-stat"><div class="asi-stat-value">0.295</div><div class="asi-stat-label">drift severity at the change-point</div></div></div>
</div>

**Hard-bucket execution accuracy**, same 30 held-out questions, same eval:

<div class="asi-bars" role="img" aria-label="Hard-bucket execution accuracy: base agent 0.300, teacher model 0.400, self-corrected base agent 0.567">
    <div class="asi-bar-row">
        <div class="asi-bar-label">Base agent, no examples</div>
        <div class="asi-bar-track"><div class="asi-bar-fill" style="width: 30%"></div><span class="asi-bar-value">0.300</span></div>
    </div>
    <div class="asi-bar-row">
        <div class="asi-bar-label">Teacher model (MiniMax-M3)</div>
        <div class="asi-bar-track"><div class="asi-bar-fill" style="width: 40%"></div><span class="asi-bar-value">0.400</span></div>
    </div>
    <div class="asi-bar-row">
        <div class="asi-bar-label"><strong>Self-corrected base agent</strong></div>
        <div class="asi-bar-track"><div class="asi-bar-fill asi-best" style="width: 56.7%"></div><span class="asi-bar-value">0.567</span></div>
    </div>
    <div class="asi-axis"><span>0</span><span>0.25</span><span>0.50</span><span>0.75</span><span>1.0</span></div>
</div>

The self-improved agent **beat its own teacher**. Half of its examples are execution-verified gold SQL that the teacher couldn't produce, which scaffolds the weaker model past the stronger one's unaided accuracy.

**Is it chance?** We re-evaluated the same 30 hard questions with and without the learned examples and ran a paired McNemar exact test: **p = 0.016** (two-sided), paired delta **+0.233**, 95% CI **[+0.08, +0.39]**. The model isn't perfectly deterministic even at temperature 0, so absolute accuracy moves by 2 or 3 questions between runs (the demo run measured +0.267, the paired test +0.233). The claim I'd stand behind is the paired delta with its interval.

## Tech stack

Python · Pydantic (typed contracts) · SQLite + Spider execution-accuracy eval · MiniMax (OpenAI-compatible API) for the base and teacher models · FastAPI + Chart.js (viewer)

## Team

A four-person team, equal contributors, one stage each:

- **Rohan**: Harness / telemetry
- **Logan Rudd**: Detector / drift detection
- **Mihir Agarwal** (me): Correction / learning
- **Yiwen**: Viewer

Logan wrote up the project from the detector's side: [loganrudd.com/agent-self-improvement](https://loganrudd.com/agent-self-improvement/). The code lives at [mihir-agarwal0211/agent-self-improvement](https://github.com/mihir-agarwal0211/agent-self-improvement), copied with full history from [the original repo](https://github.com/loganrudd/agent-self-improvement), which Logan hosts.
