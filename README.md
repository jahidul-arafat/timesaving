# DGTP e-Services — Time-Saving Strategy Meeting
### Design & Development of Selected e-Services via Multiple Channels including an Online Portal
**Implementation of an Interoperability Platform with Six Key Government Registries**

---

> **Presented by:** Application Integration Expert, Orange bd  
> **Client:** eSXM Digital Leadership Team & NRPB — Sint Maarten  
> **Format:** Interactive single-file HTML presentation  
> **Duration:** 60 minutes (45 min presentation + 15 min Q&A)  
> **Platform:** Microsoft Azure (sole cloud provider)

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Quick Start](#2-quick-start)
3. [File Structure](#3-file-structure)
4. [Sections & Navigation](#4-sections--navigation)
5. [Interactive Features](#5-interactive-features)
6. [Nine Governing Principles](#6-nine-governing-principles)
7. [The Six Registries](#7-the-six-registries)
8. [Five Shared Services](#8-five-shared-services)
9. [CI/CD Pipeline](#9-cicd-pipeline)
10. [Measures of Success](#10-measures-of-success)
11. [Access Credentials](#11-access-credentials)
12. [Colour Theme & Design](#12-colour-theme--design)
13. [JavaScript Modules](#13-javascript-modules)
14. [Presenter Script](#14-presenter-script)
15. [Customer Feedback Log](#15-customer-feedback-log)
16. [Adding New Content](#16-adding-new-content)
17. [Known Constraints](#17-known-constraints)
18. [Commit History](#18-commit-history)

---

## 1. Project Overview

This is a **fully interactive, single-file HTML presentation** built for the Sint Maarten DGTP (Digital Government Transformation Project) Time-Saving Strategy Meeting. It replaces traditional PowerPoint slides with a living, animated, navigable document that stakeholders can explore during and after the meeting.

### What it covers

| Area | Detail |
|------|--------|
| **Programme scope** | e-Services portal + interoperability platform for Sint Maarten |
| **Six registries** | Civil, Business, Address, TaxPayer, Business License, Land |
| **Five shared services** | Notifications, Identity (SSO), Document Generation, Search, Payment |
| **Nine principles** | The governing delivery commitments — each with animated flowchart |
| **AI strategy** | Claude CLI via OpenRouter, GitHub Copilot, Azure OpenAI, Human-in-the-Loop |
| **CI/CD pipeline** | Ten-stage animated SVG with hover tooltips on every element |
| **Success metrics** | Five KPIs tracked automatically via Azure DevOps Analytics |
| **FAQ** | 27 questions across 7 categories (password protected) |
| **Feedback log** | Progressive changelog of all stakeholder-driven changes (password protected) |

### Key design decisions

- **No build system** — pure HTML, CSS, and vanilla JavaScript. Open `index.html` directly in any modern browser.
- **No external CDN dependencies** — all code is self-contained. Works offline.
- **Single file entry point** — everything is served from `index.html`. JavaScript files are loaded in the correct order at the bottom of `<body>`.
- **Dark gradient blue theme** throughout, matching a professional government digital programme aesthetic.

---

## 2. Quick Start

```bash
# Clone or unzip the project
unzip dgtp-presentation.zip
cd dgtp-presentation

# Open directly in browser (no server needed)
open index.html          # macOS
start index.html         # Windows
xdg-open index.html      # Linux
```

> **Recommended browser:** Google Chrome or Microsoft Edge (latest).  
> Firefox works. Safari works. Internet Explorer is not supported.

### For presentations

1. Open `index.html` in Chrome
2. Press **F11** for fullscreen (hides browser chrome)
3. Set zoom to **90%** for best fit on a projector (Ctrl/Cmd + `-`)
4. Keep this README or the [Presenter Script](#14-presenter-script) on a second device

---

## 3. File Structure

```
dgtp-presentation/
│
├── index.html                 ← Main entry point (open this)
│
├── css/
│   ├── main.css               ← Global theme, layout, hero, nav, typography
│   └── figures.css            ← Component styles: modals, flowcharts, badges,
│                                 agenda, FAQ gate, changelog gate, KPI section
│
├── js/
│   ├── figures.js             ← ⚠️ MUST LOAD FIRST — shared modal system
│   │                             (openModal, closeModal, mkpi, mtags, mdesc)
│   ├── core.js                ← Scroll progress, reveal animations, counters,
│   │                             nav active state, tooltips
│   ├── agenda.js              ← Meeting agenda — 6 items, expandable, section links
│   ├── challenges.js          ← Traditional Challenges D-shape figure,
│   │                             Nine Principles panel, all flowcharts,
│   │                             break badge sound, challenge flow SVGs
│   ├── pipeline.js            ← CI/CD pipeline animated SVG, 10 stages,
│   │                             5 environment lanes, 4 strip cards
│   ├── kpi.js                 ← Measures of Success — 5 circular metrics,
│   │                             dedicated flowcharts per metric
│   ├── app.js                 ← Review & Sign-Off Rubric table, status cycling,
│   │                             progress ring, approve/reset
│   ├── faq.js                 ← FAQ — 27 questions, 7 categories, live search
│   │                             (does NOT auto-run — called after auth)
│   ├── changelog.js           ← Customer Feedback Addressed log — 20 entries,
│   │                             7 categories (does NOT auto-run — called after auth)
│   └── legend.js              ← Floating glossary FAB — 66 terms, 7 categories,
│                                 drag to reposition, Ctrl+G toggle
│
└── assets/
    ├── logo-esxm.png          ← eSXM / NRPB logo (displayed in nav)
    ├── logo-orange.png        ← Orange bd logo (displayed in nav)
    ├── figure1_cicd.png       ← Static reference image (not displayed in presentation)
    ├── figure2_architecture.png
    └── figure3_timeline.png
```

### Script load order (critical)

The scripts **must** load in this exact order. `figures.js` defines `openModal`, `mkpi`, `mtags`, and `mdesc` — every other file depends on these being in global scope first.

```html
<script src="js/figures.js"></script>   <!-- 1. Shared modal helpers -->
<script src="js/core.js"></script>       <!-- 2. Scroll/reveal/nav -->
<script src="js/agenda.js"></script>     <!-- 3. Meeting agenda -->
<script src="js/challenges.js"></script> <!-- 4. Challenges + Principles -->
<script src="js/pipeline.js"></script>   <!-- 5. CI/CD pipeline -->
<script src="js/kpi.js"></script>        <!-- 6. Success metrics -->
<script src="js/app.js"></script>        <!-- 7. Rubric table -->
<script src="js/changelog.js"></script>  <!-- 8. Feedback log -->
<script src="js/faq.js"></script>        <!-- 9. FAQ -->
<script src="js/legend.js"></script>     <!-- 10. Glossary FAB -->
```

---

## 4. Sections & Navigation

The presentation has **8 sections** accessible via the top navigation bar:

| Nav Label | Section ID | Content |
|-----------|------------|---------|
| Overview | `#hero` | Project title, animated hero, six registries, hero stats |
| Agenda | `#agenda` | 6 agenda items, expandable, timed, with section hyperlinks |
| Challenges | `#challenges` | Interactive D-shape figure + Nine Principles panel |
| Principles | `#principles` | Nine clickable animated principle cards |
| CI/CD | `#pipeline` | 10-stage animated pipeline SVG |
| Success | `#kpis` | Five success metric circles + individual flowcharts |
| Review | `#rubric` | Sign-off rubric table with cycling status badges |
| FAQ | `#faq` | 🔒 Password protected — see [credentials](#11-access-credentials) |
| Feedback | `#changelog` | 🔒 Password protected — see [credentials](#11-access-credentials) |

---

## 5. Interactive Features

### Hover tooltips
Every node, circle, arrow endpoint, and card in every SVG flowchart has a hover tooltip in **plain, non-technical English**. Tooltips use the Web Audio tooltip system (`showFlowTip` / `hideFlowTip`) defined in `challenges.js`.

### Clickable modals
All principle cards, challenge nodes, pipeline stages, environment lanes, KPI circles, and challenge flow nodes open a detail modal. The modal system is in `figures.js`.

**Modal width controls** — every modal has **S / M / L / XL** buttons in the header:

| Button | Width |
|--------|-------|
| S | 480px |
| M | 728px (default) |
| L | 960px |
| XL | 1200px (or 94vw) |

### Break badges on challenge flows
Every red failure arrow in the Traditional Challenges flowcharts has a **red ✕ badge** at its midpoint. Clicking plays a two-tone warning beep (Web Audio API, no external files) and shakes the badge. Arrows pointing *toward* DGTP solution nodes are green and have no badge.

### Floating Glossary FAB
Bottom-right corner. 58px circular button, 50% opacity at rest, full opacity on hover.

- **Ctrl+G** — toggle open/close from anywhere
- **`/`** — focus search when open
- **Drag** to reposition anywhere on screen
- 66 abbreviations across 7 categories (Azure Services, Security, DevOps, Architecture, Testing, Programme, Protocols)

### Hero animations
- **Typewriter** — "Design & Development of `[word]` e-Services" cycles through: faster, smarter, citizen-first, AI-powered, secure, interoperable, cloud-native, automated, transparent, trusted
- **Particle network** — 55 floating dots with connecting lines (Canvas 2D)
- **Glowing orbs** — three animated blurred radial gradients drifting behind content
- **Staggered entrance** — all hero elements fade up in sequence on load

---

## 6. Nine Governing Principles

Each principle card opens an animated flowchart modal. The data is in `PRINCIPLES_VIZ` array in `challenges.js`.

| # | Principle | Colour | Challenges Solved |
|---|-----------|--------|-------------------|
| 1 | Shift Left | `#0078D4` | Fragmented Systems, Manual Validation, Regulatory Complexity |
| 2 | Automate Everything | `#005A9E` | Manual Validation, Sequential Development |
| 3 | Standardize Patterns | `#003087` | Fragmented Systems, Legacy Integration |
| 4 | Reuse Before Build | `#107C10` | Fragmented Systems, Legacy Integration |
| 5 | Parallel Execution | `#6B4FA8` | Multi-Stakeholder Coordination, Sequential Development |
| 6 | Incremental Delivery | `#0078D4` | Sequential Development |
| 7 | Governance by Design | `#C55A00` | Multi-Stakeholder Coordination, Regulatory Complexity |
| 8 | Zero-Trust Security | `#107C10` | Regulatory Complexity, Legacy Integration |
| 9 | AI-Accelerated Delivery | `#8A2BE2` | Manual Validation, Coordination, Sequential Dev, Regulatory, Legacy |

### Principle 9 — AI-Accelerated Delivery
Specific AI tools in the flowchart:
- **Claude CLI via OpenRouter** — agentic code review, draft test generation
- **GitHub Copilot** — inline code generation (30–55% productivity gain)
- **Azure OpenAI** — requirement-to-code draft, specification analysis
- **Azure AI Services** — search, document understanding at service level
- **Human-in-the-Loop gate** (amber) — every AI output requires explicit human approval before proceeding. No AI output reaches citizens without human review.

---

## 7. The Six Registries

| Registry | Icon | Primary Services |
|----------|------|-----------------|
| Civil Registry | 🏛️ | Identity, civil records, vital statistics |
| Business Registry | 💼 | Business entity registration, status, renewals |
| Address Registry | 📍 | Official address lookup, validation, standardisation |
| TaxPayer Registry | 🧾 | Taxpayer accounts, registration, certificate services |
| Business License Registry | 📋 | Licence applications, renewals, status |
| Land Registry | 🏠 | Property ownership, title records, searches |

> **Note:** Vehicle Registry, Health Registry, and Education Registry are **not** in scope for this programme.

---

## 8. Five Shared Services

Built once via the **Reuse Before Build** principle. All six registries consume all five through **Azure Service Bus** as the shared integration backbone.

| Service | Icon | Technology | Purpose |
|---------|------|------------|---------|
| Notifications | 🔔 | Azure Communication Services | Email/SMS alerts across all registries |
| Identity (SSO) | 🔑 | Microsoft Entra External ID | Single sign-on for all registry services |
| Document Generation | 📄 | Shared Document Service | Certificates, licences, receipts, official letters as digital outputs |
| Search | 🔍 | Azure AI Search | Cross-registry search from a single interface |
| Payment Service | 💳 | Payment Service | Fee collection across all registry transactions |

> **Document Generation is an output service** — it generates official documents as the end result of a completed service transaction. It is **not** a document scanning or OCR service.

---

## 9. CI/CD Pipeline

Ten-stage animated SVG in `pipeline.js`. Every element has a hover tooltip and click-to-expand modal.

| Stage | Badge | Description |
|-------|-------|-------------|
| Code Commit | Auto | PR with 2-reviewer approval, linked work item |
| Build | Auto | YAML pipeline, Maven/npm/Gradle, < 8 min |
| SAST & Scan | Security | Defender for DevOps, secret detection, SCA |
| Container Build | Auto | Docker → Azure Container Registry, Trivy scan |
| Deploy Dev | Auto | AKS Helm chart, App Config + Key Vault injection |
| QA Gate | Gate | 80% coverage enforced, Playwright E2E, Postman Newman |
| Load Test | Gate | Azure Load Testing — 200 users, P95 < 2s |
| UAT Approval | **Human** | Business owner, 48-hour SLA, recorded in pipeline |
| Security Gate | Security | Defender posture + OWASP ZAP DAST, dual sign-off |
| Production | **CAB** | Blue/Green AKS, Azure Monitor rollback, zero downtime |

**Two human approval gates:** UAT (business owner) and Production (CAB/Steering Committee). Everything else is automated.

The pipeline SVG also shows:
- **5 environment lanes** — DEV, QA, UAT, PRE-PROD, PROD (each clickable)
- **4 foundation strip cards** — IaC, Container Registry, Observability, Security Posture (each clickable)
- **Inline flow animation** — clicking any stage renders its 5-step sub-flow in the lower panel

---

## 10. Measures of Success

Five KPIs tracked automatically via Azure DevOps Analytics and Azure Monitor. Data in `kpi.js`.

| Metric | Target | Measured By |
|--------|--------|-------------|
| Deploy Frequency | ≥ 1 per day | Azure DevOps Analytics |
| Lead Time | < 24 hours | Azure Pipelines timeline |
| Change Failure Rate | < 5% | Azure Monitor + rollback events |
| Recovery Time (MTTR) | < 1 hour | Azure Monitor incident duration |
| Test Coverage | ≥ 80% | Azure Test Plans coverage gate |

Each circle click opens a dedicated animated flowchart showing exactly how that metric is achieved, with hover tooltips on every step.

---

## 11. Access Credentials

Two sections of the presentation are password protected.

| Section | Username | Password |
|---------|----------|----------|
| FAQ | `orange` | `faq` |
| Customer Feedback Addressed | `orange` | `orange2244` |

Credentials are stored as Base64-encoded strings in the HTML. This is obfuscation, not cryptographic security — it is sufficient to prevent casual browsing during a presentation.

> **For the presenter:** Both credentials are visible in the [Presenter Script PDF](#14-presenter-script). Do not display this README on the main presentation screen.

---

## 12. Colour Theme & Design

**Dark Gradient Blue** — defined as CSS custom properties in `css/main.css`:

```css
:root {
  --navy:        #0A2744;   /* Primary dark navy */
  --navy-dark:   #061A30;   /* Deeper navy (hero gradient start) */
  --navy-light:  #0F3A60;   /* Mid navy */
  --azure:       #1A6FBE;   /* Accent blue (buttons, links, active states) */
  --azure-light: #2E8FE0;   /* Lighter azure */
  --azure-pale:  #E8F2FC;   /* Background tint */
  --azure-tint:  #F3F8FE;   /* Very pale background */
  --green:       #107C10;   /* Success / solution */
  --amber:       #C55A00;   /* Warning / human gates */
  --red:         #A4262C;   /* Error / failure / break badges */
}
```

**Hero gradient:** `linear-gradient(160deg, #061A30 0%, #0F3A60 50%, #1A6FBE 100%)`

**Typography:** Arial/Helvetica (sans) · Georgia/Times New Roman (serif for italic hero title elements)

---

## 13. JavaScript Modules

### `figures.js` — Shared Modal System
Defines: `openModal(icon, title, sub, body)`, `closeModal()`, `setModalWidth(size)`, `mdesc(text)`, `mkpi(items)`, `mtags(arr)`

**Must load first.** All other modules call `openModal` — if this file is missing or loads late, every clickable element will throw `ReferenceError: openModal is not defined`.

### `challenges.js` — Challenges & Principles
Contains:
- `CHALLENGES` — 6 challenge data objects with flowcharts (`CHALLENGE_FLOWS`)
- `PRINCIPLES_BRIEF` — 9 principle summary objects (icon, label, colour, solves)
- `PRINCIPLES_VIZ` — 9 animated flowchart definitions (nodes, arrows, labels, metrics)
- `PRINCIPLE_DETAILS_BRIEF` — 9 title/sub/tools entries
- `buildChallengesFigure()` — renders the D-shape SVG
- `buildChallengeFlowSVG(flow, color, idx)` — builds challenge flowchart SVGs
- `buildFlowSVG(flow, color, principleIdx)` — builds principle flowchart SVGs
- `openChallenge(id)` — opens challenge detail modal
- `openPrincipleDetail(i)` — opens principle detail modal
- `playBreakSound()` — Web Audio beep on ✕ badge click
- `showFlowTip(event, el)` / `hideFlowTip()` — hover tooltip system

### `pipeline.js` — CI/CD Pipeline
Contains:
- `PIPELINE_STAGES` — 10 stage objects (each with `flow` sub-steps and `tip`)
- `PIPELINE_ENVS` — 5 environment lane objects
- `PIPELINE_STRIPS` — 4 foundation strip card objects
- `buildPipelineSVG()` — renders the full pipeline SVG
- `renderInlineFlow(stage)` — animates the 5-step sub-flow in the lower panel
- `openPipelineStage(id)`, `openPipelineEnv(id)`, `openPipelineStrip(i)`

### `kpi.js` — Measures of Success
Contains:
- `SUCCESS_METRICS` — 5 metric objects (each with dedicated `flow` flowchart)
- `buildKPISection()` — renders the circular metrics overview SVG
- `kpiBuildFlowSVG(flow, color, idx)` — builds metric flowchart SVGs
- `openKPIDetail(id)` — opens metric detail modal

### `faq.js` — FAQ
- `FAQ_DATA` — 27 questions across 7 categories
- `buildFAQ()` — renders the FAQ list (exposed as `window.buildFAQ`, not auto-called)
- `toggleFAQ(id)`, `filterFAQ(val)`

### `changelog.js` — Customer Feedback Log
- `CHANGELOG` — 20 entries with feedback quote, change description, section, impact
- `buildChangelog()` — renders the log (exposed as `window.buildChangelog`, not auto-called)
- `toggleChangelog(id)`, `filterChangelog(val)`

### `legend.js` — Floating Glossary
- `GLOSSARY` — 66 terms across 7 categories
- Drag to reposition, live search, auto-highlight on modal open
- Ctrl+G to toggle, `/` to focus search, Escape to close

---

## 14. Presenter Script

A complete word-for-word presenter script is provided as a separate file:

| File | Description |
|------|-------------|
| `presenter_script.tex` | LaTeX source file |
| `presenter_script.pdf` | Compiled PDF (print this for the meeting) |

The script includes:
- Pre-meeting checklist (8 items)
- All 6 agenda items with `SCRIPT:`, `ACTION:`, `PAUSE:`, `TRANSITION:` callouts
- Specific click instructions (which nodes, which cards, which pipeline stages)
- FAQ unlock moment with credentials
- Sign-off walkthrough at 09:55
- Q&A management guide
- Key messages table for common stakeholder challenges

> To recompile the PDF after editing the `.tex` file:
> ```bash
> pdflatex presenter_script.tex
> pdflatex presenter_script.tex   # run twice for TOC
> ```

---

## 15. Customer Feedback Log

Located at `#changelog` (nav: "Feedback"). Password protected — see [credentials](#11-access-credentials).

**20 entries** covering every significant change made based on stakeholder feedback, grouped by category:

| Category | Changes |
|----------|---------|
| Scope Accuracy | Registry names corrected; Document Generation replaces OCR |
| Architecture | Payment Service added as 5th shared service |
| Clarity | Challenge names replace numbers; all registries named in full |
| Accuracy | 8-month timeline references removed throughout |
| Structure | Agenda aligned to actual sections; redundant sections removed |
| Ownership | Orange bd team ownership clarified throughout |
| Visual Design | Animated hero, flowchart modals, wider windows |
| Interaction | Break badges with sound, modal width controls |
| Content | AI principle added, Measures of Success section added |
| Feature | FAQ and Changelog password protection |

To add a new entry, append an object to the `CHANGELOG` array in `changelog.js`:

```javascript
{
  id: 'cl-21',
  date: 'Session 2 Review',
  category: 'Category Name',
  icon: '🔧',
  color: '#0078D4',
  feedback: `"The exact words the stakeholder said."`,
  change: `What was changed and where.`,
  section: 'Section name',
  impact: 'Critical' // or 'High' or 'Medium'
}
```

---

## 16. Adding New Content

### Add a new principle
1. Add an entry to `PRINCIPLES_BRIEF` in `challenges.js`
2. Add an entry to `PRINCIPLES_VIZ` with `nodes`, `arrows`, `labels`, and `metrics`
3. Add an entry to `PRINCIPLE_DETAILS_BRIEF` with `title`, `sub`, `tools`
4. Add a new principle card in `index.html` with `onclick="openPrincipleDetail(N)"` where N is the 0-based index
5. Increase SVG height in `buildChallengesFigure()` if needed

### Add a new FAQ question
Add an object to the appropriate `items` array inside `FAQ_DATA` in `faq.js`:
```javascript
{
  q: 'Your question here?',
  a: 'Full answer here.',
  tags: ['Tag1', 'Tag2']
}
```

### Change the typewriter words
Edit the `WORDS` array in the inline `<script>` block at the bottom of `index.html`:
```javascript
const WORDS = ['faster', 'smarter', 'citizen-first', ...];
```

### Change modal width defaults
Edit `MODAL_WIDTHS` in `figures.js`:
```javascript
const MODAL_WIDTHS = { S:'480px', M:'728px', L:'960px', XL:'min(1200px,94vw)' };
```

---

## 17. Known Constraints

| Constraint | Detail |
|------------|--------|
| **File:// security warning** | When opened from disk, anchor links (`href="#section"`) show a harmless browser security notice in the console. Does not affect functionality. |
| **No persistent state** | Rubric status badges are saved to `sessionStorage` — they reset when the tab is closed. |
| **Audio requires user gesture** | Web Audio beep sounds (break badges, gate unlock/error) require a prior user interaction due to browser autoplay policy. Any click before the sound fires is sufficient. |
| **No server required** | The presentation is entirely self-contained. No Node.js, no npm, no build step. |
| **Internet not required** | All code is local. The only network requests are if a browser extension interferes. |
| **Print/PDF export** | Use Chrome's Print → Save as PDF with background graphics enabled for a reasonable printout. Interactive elements will not function in PDF. |

---

## 18. Commit History

```
commit 0f43715
Author: Application Integration Expert <appintegration@orangebd.com>
Date:   [Session date]

feat: DGTP e-Services Time-Saving Strategy Presentation

- Nine Governing Principles with animated flowcharts and hover tooltips
- Traditional Government Delivery Challenges interactive D-shape figure
- Six correct Sint Maarten registries: Civil, Business, Address, TaxPayer,
  Business License, Land Registry
- CI/CD Pipeline animated SVG with 10 stages, environments, and strip cards
- Measures of Success with five animated metric flowcharts
- AI-Accelerated Delivery principle: Claude CLI / OpenRouter / Azure OpenAI
- Human-in-the-Loop gate on all AI outputs
- FAQ section with gate (orange/faq)
- Customer Feedback Addressed section with gate (orange/orange2244)
- Review & Sign-Off Rubric with cycling status badges
- Reuse Before Build: 5 shared services + Azure Service Bus backbone
- Document Generation as document output service (not OCR)
- Hero: typewriter animation, floating particles, glowing orbs
- Dark gradient blue theme throughout
- Red break badges with beep sound on traditional failure path arrows
- Floating glossary FAB with 66 terms across 7 categories
- Presenter script in LaTeX (.tex) and compiled PDF
- S/M/L/XL modal width controls
- All delivery timeline references removed (TBD)
- Orange bd team ownership clarified throughout

Co-authored-by: Claude <claude@anthropic.com>
```

---

## Licence & Confidentiality

This presentation is **confidential** and intended solely for the Sint Maarten DGTP programme stakeholders. Do not distribute outside the eSXM Digital Leadership Team, NRPB, and Orange bd programme team.

---

*Orange bd — Application Integration Expert — Sint Maarten DGTP e-Services Programme*
