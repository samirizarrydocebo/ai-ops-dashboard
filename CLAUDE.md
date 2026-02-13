# AI Ops Dashboard - Claude Code Instructions

## Project Overview

This repository contains the **AI Operations Dashboard** for Docebo, showcasing the AI Ops team's impact from August 2025 to February 2026. It's a single-page HTML application deployed via GitHub Pages.

**Live URL:** https://samirizarrydocebo.github.io/ai-ops-dashboard/

## Repository Structure

```
AI Ops/
├── AI-Ops-Dashboard.html    # Main dashboard (primary file to edit)
├── index.html               # GitHub Pages entry point (synced copy)
├── CLAUDE.md                # This file
├── account-intelligence-canvas.skill.md  # Account canvas generator skill
├── buyer-signal-canvas.skill.md # Buyer signal triangulation canvas skill
├── docebo-brand-audit.skill.md  # Brand compliance audit skill
├── docebo-brand-system.skill    # Brand system reference (ZIP)
├── .gitignore
├── account-canvases/        # Generated account intelligence canvases
│   ├── {account}-canvas.html               # Base HTML canvas
│   ├── {account}-buyer-signals-canvas.html # Buyer signal triangulation canvas
│   └── {account}-canvas-data.json          # Raw data for incremental updates
├── docs/                    # Source documentation and research
│   ├── AI Ops Wins.md
│   ├── UnifyApps at Docebo...pdf
│   ├── Glean usage image and data/
│   └── ...
└── docebo-brand-system-extracted/
    └── docebo-brand-system/
        └── SKILL.md         # Comprehensive Docebo brand guidelines
```

## Development Workflow

### Editing the Dashboard

1. **Always edit `AI-Ops-Dashboard.html`** - this is the source of truth
2. **Sync changes to `index.html`** - copy the entire file content
3. **Commit and push to main** - GitHub Pages auto-deploys

```bash
# After making changes:
cp AI-Ops-Dashboard.html index.html
git add AI-Ops-Dashboard.html index.html
git commit -m "Description of changes"
git push origin main
```

### File Sync Requirement

**Critical:** Both `AI-Ops-Dashboard.html` and `index.html` must always be identical. GitHub Pages serves `index.html`, but the descriptive filename is used for development clarity.

## Technical Architecture

### Single-File Application

The entire dashboard is contained in one HTML file with embedded CSS and JavaScript. This includes:

- **CSS custom properties** for Docebo brand colors
- **Tab navigation** via `showPage()` function
- **Modal system** for detailed content popups
- **Responsive grid layouts**

### Tab Navigation

```javascript
function showPage(pageId) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
    document.getElementById(pageId).classList.add('active');
    document.querySelector(`.nav-tab[onclick*="${pageId}"]`).classList.add('active');
    window.scrollTo(0, 0);
}
```

**Current tabs:** Overview, Pipeline, Glean platform, UnifyApps, Governance, Team

### Modal Pattern

```html
<!-- Trigger -->
<span class="modal-trigger" onclick="openModal('modal-id')">Learn more</span>

<!-- Modal -->
<div id="modal-id" class="modal-overlay" onclick="closeModal('modal-id')">
    <div class="modal-content" onclick="event.stopPropagation()">
        <button class="modal-close" onclick="closeModal('modal-id')">×</button>
        <!-- Content -->
    </div>
</div>
```

## Docebo Brand System

### Required Reading

Before making visual changes, review: `docebo-brand-system-extracted/docebo-brand-system/SKILL.md`

### Core Colors (Phoenix Palette)

```css
:root {
    --docebo-blue: #0057FF;      /* Primary brand color */
    --docebo-black: #2A2923;     /* Text color */
    --docebo-white: #FFFFFF;
    --docebo-dark: #131E29;      /* Navigation background */
    --docebo-navy: #0033A0;      /* Gradients */
    --docebo-pink: #FF5DD8;      /* Accent */
    --docebo-green: #54FA77;     /* Success/positive metrics */
    --docebo-purple: #7E2EE9;    /* Pipeline/horizon projects */
    --docebo-yellow-green: #E3FFAB;  /* Highlights */
}
```

### Typography

- **Headings:** Space Grotesk (400, 500, 700)
- **Body:** Inter (400, 500, 600, 700)

```css
--font-heading: 'Space Grotesk', sans-serif;
--font-body: 'Inter', sans-serif;
```

### Voice Guidelines

- **Bold, not arrogant** - Confident leadership without hyperbole
- **Professional, not stiff** - Human and engaging
- **Data-driven** - Always include methodology and sources
- **Active voice** - "We built" not "It was built"

### Writing Rules (Strict)

- **No em dashes (—)** - Use semicolons, commas, or periods instead
- **Banned AI-speak words** - "leverage", "delve", "navigate", "realm", "embark", "utilize", "synergy", "robust"
- **Sentence case only** - Never Title Case for headings
- **Oxford comma** - Always use it

## Adding New Content

### New Metric Card

```html
<div class="stat-card">
    <div class="stat-number">600+</div>
    <div class="stat-label">Monthly active users</div>
    <div class="stat-sublabel">~70% of employees</div>
</div>
```

### New Project Card (with modal)

```html
<div class="project-card clickable-card" onclick="openModal('project-modal')">
    <div class="project-status status-live">Live</div>
    <h3>Project Name</h3>
    <p>Brief description of the project impact.</p>
    <div class="project-meta">
        <span>Owner: Name</span>
        <span class="modal-trigger">View methodology →</span>
    </div>
</div>
```

### New Tab

1. Add nav button:
```html
<button class="nav-tab" onclick="showPage('newtab')">New Tab</button>
```

2. Add page section:
```html
<div id="newtab" class="page">
    <!-- Tab content -->
</div>
```

## Data Sources

### Primary Research Tools

- **Glean MCP** - Search internal Docebo documentation via `mcp__claude_ai_Glean_MCP__search`
- **Slack MCP** - Get team profile photos via `mcp__claude_ai_Slack__slack_search_users`
- **Local docs/** folder - Contains exported documentation and metrics

### Key Metrics Sources

| Metric | Source |
|--------|--------|
| Glean MAU/WAU | AI Ops Wins.md, Glean dashboard screenshots |
| UnifyApps apps | UnifyApps at Docebo PDF, internal roadmap |
| Accuracy claims | Must specify which application (e.g., "Churn Analysis AI: ~95%") |

## Brand Audit

Run `docebo-brand-audit.skill.md` to check compliance:
- Colors: Phoenix palette only, no arbitrary hex values
- Typography: Space Grotesk headings, Inter body
- Voice: No em dashes, no AI-speak words
- Accessibility: Focus states, alt text, contrast ratios

## Account Intelligence Canvas

Generate comprehensive account intelligence reports using `account-intelligence-canvas.skill.md`.

### Usage

```bash
# Generate full canvas for an account
/account-intelligence-canvas Google

# Account names with spaces
/account-intelligence-canvas "Palo Alto Networks"

# Options
/account-intelligence-canvas Honeywell --full      # Force full refresh
/account-intelligence-canvas Google --pipeline     # Update pipeline only
/account-intelligence-canvas Google --signals      # Update signals only
```

### Data Sources Queried

| Source | Data Retrieved |
|--------|----------------|
| Salesforce | Account details, ARR, opportunities, contacts |
| Slack | Account channel discussions, team signals |
| Gong (via Glean) | Call transcripts, stakeholder quotes |
| Totango (via Glean) | Health scores, objectives, REACH data |
| Qualtrics (via Glean) | NPS scores, survey responses |

### Output Files

Generated canvases are saved to `account-canvases/`:
- `{account-slug}-canvas.html` - Visual HTML canvas
- `{account-slug}-canvas-data.json` - Raw data for incremental updates

### Signal Categories

- **Positive signals**: Renewal confirmations, champion engagement, expansion mentions
- **Risk signals**: Budget cuts, champion departures, competitor mentions, low NPS
- **Expansion opportunities**: New use cases, department expansion, high utilization

## Buyer Signal Triangulation Canvas

Generate buyer signal canvases with expansion, upsell, and cross-sell scoring using `buyer-signal-canvas.skill.md`. Extends the base account canvas with FIRE propensity scoring, REACH framework, whitespace analysis, and corporate family cross-sell mapping.

### Usage

```bash
# Full buyer signal canvas
/buyer-signal-canvas Google

# Options
/buyer-signal-canvas Google --full           # Full refresh
/buyer-signal-canvas Google --signals        # Update signals only
/buyer-signal-canvas Google --whitespace     # Update whitespace + cross-sell
/buyer-signal-canvas Google --cross-sell     # Corporate family mapping only
```

### Scoring Models

| Model | Purpose | Scale |
|-------|---------|-------|
| FIRE Score | Propensity to expand | 0-100 (Fit + Intent + Recency + Engagement) |
| REACH Score | Expansion readiness (CS to AM handoff) | 1-5 (Relationships, Engagement, Actions, Customer Value, Horizons) |
| Signal Confidence | Triangulation strength | 35-95% (based on confirming source count) |

### Output (5-tab HTML)

1. **Overview**: FIRE gauge, REACH grid, signals with source badges
2. **Buyer signal triangulation**: Confidence-scored signals, 3-source rule
3. **Whitespace + cross-sell**: Product gaps, corporate family tree, TAM sizing
4. **Pipeline + team**: Deal types (upsell/expansion/renewal), stakeholder annotations
5. **Expansion playbook**: Upsell, cross-sell, retention plays with GTM owner mapping

## Common Tasks

### Update a Metric

1. Find the metric in `AI-Ops-Dashboard.html`
2. Update the value and any methodology modal
3. Sync to `index.html`
4. Commit with source citation

### Add a Team Member

Team section uses this pattern:
```html
<div class="team-member">
    <div class="member-avatar">SI</div>
    <div class="member-info">
        <h4>Sam Irizarry</h4>
        <p>Director, AI Operations & Business Technology</p>
    </div>
</div>
```

### Add a Timeline Event

```html
<div class="timeline-item">
    <div class="timeline-dot"></div>
    <div class="timeline-date">Month YYYY</div>
    <div class="timeline-content">
        <strong>Event Title</strong>
        <p>Description of milestone.</p>
    </div>
</div>
```

## Quality Standards

### Before Committing

- [ ] All metrics have methodology documentation (modal or inline)
- [ ] Brand colors used consistently (no arbitrary hex values)
- [ ] `index.html` synced with `AI-Ops-Dashboard.html`
- [ ] No broken modal links
- [ ] Responsive layout tested

### Metric Accuracy

- Always cite the source document
- Include date of data collection
- Specify scope (e.g., "Enterprise segment" vs "All users")
- Use `~` prefix for approximations

## Git Workflow

```bash
# Standard commit
git add AI-Ops-Dashboard.html index.html
git commit -m "Add [feature]: [brief description]"
git push origin main

# Deployment is automatic via GitHub Pages
```

## Notes

- **No build process** - Edit HTML directly
- **No dependencies** - Only Google Fonts CDN
- **Single branch** - All work on `main`
- **Auto-deploy** - Push triggers GitHub Pages update
- **Skill files** - `.skill` = ZIP archive, `.skill.md` = plain markdown
