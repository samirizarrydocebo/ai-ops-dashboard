---
name: account-intelligence-canvas
description: Generate comprehensive Account Intelligence Canvas reports by querying Salesforce, Slack, Gong, Totango, and Qualtrics data sources. Use when preparing for QBRs, account reviews, or strategic planning.
args: account_name [--full|--pipeline|--signals]
---

# Account Intelligence Canvas Generator

This skill systematically queries multiple data sources, triangulates findings, and generates a comprehensive account intelligence canvas with both an HTML file and terminal summary.

## Prerequisites

Before running, ensure you have access to:
- Zapier MCP (Salesforce queries)
- Slack MCP (channel search)
- Glean MCP (Gong, Totango, Qualtrics search)

## Execution Flow

```
┌─────────────────────────────────────────────────────────────────┐
│  1. VALIDATE ACCOUNT                                            │
│     └─ Search Salesforce for account, confirm match             │
├─────────────────────────────────────────────────────────────────┤
│  2. COLLECT DATA (parallel where possible)                      │
│     ├─ Salesforce: Account, Opportunities, Contacts             │
│     ├─ Slack: Account channel discussions                       │
│     ├─ Glean/Gong: Call transcripts                            │
│     ├─ Glean/Totango: Health scores, objectives                │
│     └─ Glean/Qualtrics: NPS, survey responses                  │
├─────────────────────────────────────────────────────────────────┤
│  3. EXTRACT SIGNALS                                             │
│     ├─ Positive signals (with source citations)                 │
│     ├─ Risk signals (with source citations)                     │
│     └─ Expansion opportunities (with source citations)          │
├─────────────────────────────────────────────────────────────────┤
│  4. TRIANGULATE & VALIDATE                                      │
│     ├─ Cross-reference signals across sources                   │
│     ├─ Assign confidence levels                                 │
│     └─ Flag conflicting data                                    │
├─────────────────────────────────────────────────────────────────┤
│  5. GENERATE OUTPUT                                             │
│     ├─ HTML canvas file                                         │
│     ├─ JSON data file (for incremental updates)                │
│     └─ Terminal summary                                         │
└─────────────────────────────────────────────────────────────────┘
```

---

## PHASE 1: Account Validation

### Step 1.1: Search Salesforce for Account

Use the ToolSearch tool to load the Salesforce query tool:
```
ToolSearch: select:mcp__claude_ai_Zapier__salesforce_find_record_by_query
```

Then query for the account:
```
mcp__claude_ai_Zapier__salesforce_find_record_by_query
  object_type: "Account"
  query: "Name LIKE '%{ACCOUNT_NAME}%'"
  fields: "Id, Name, AnnualRevenue, Industry, Type, OwnerId, Owner.Name, BillingCountry, Description"
```

### Step 1.2: Handle Multiple Matches

If multiple accounts are returned:
1. Display a numbered list showing: Name, ARR, Industry, Owner
2. Use AskUserQuestion to let user select the correct account
3. Store the selected Account ID for subsequent queries

Example prompt:
```
Multiple accounts found matching "{ACCOUNT_NAME}":

1. Google LLC - $2.4M ARR - Technology - Owner: John Smith
2. Google Cloud Services - $890K ARR - Technology - Owner: Jane Doe
3. Google Workspace Partner - $150K ARR - Reseller - Owner: Mike Johnson

Which account should I generate the canvas for?
```

### Step 1.3: Confirm Account Details

Once account is selected, display confirmation:
```
Account confirmed:
  Name: {Account Name}
  Account ID: {Account ID}
  ARR: ${ARR}
  Industry: {Industry}
  Owner: {Owner Name}

Proceeding with data collection...
```

---

## PHASE 2: Data Collection

Execute the following queries. Where possible, run queries in parallel using multiple tool calls.

### Step 2.0: Understand Data Source Roles

**CRITICAL**: Before collecting data, understand what each source provides:

| Source | Provides | NOT Suitable For |
|--------|----------|------------------|
| **Totango Account Fields** | Internal Docebo account team (Executive Sponsor, AM, CSM, Support Advisor) | External customer stakeholders |
| **Salesforce Contacts** | External customer stakeholders with roles, titles, emails | Internal Docebo team |
| **Gong Call Participants** | Both internal and external (requires validation) | Direct stakeholder source |
| **Glean Employee Search** | Validation: Is this person a Docebo employee? | Customer contact lookup |
| **Slack Mentions** | Both internal and external (requires validation) | Direct stakeholder source |

**Data Structure Reference:**

Totango Account Team Fields (ALL ARE INTERNAL DOCEBO EMPLOYEES):
- `executiveSponsor` → Docebo executive assigned to account (part of ES program)
- `accountManager` → Docebo AM responsible for sales
- `customerSuccessManager` → Docebo CSM responsible for retention
- `supportAdvisor` → Docebo Elite support contact

Salesforce Contact Fields (ALL ARE EXTERNAL CUSTOMER CONTACTS):
- `Name`, `Title`, `Email` → Customer employee information
- `Job_Title__c` → Customer's role at their company
- `Status__c` = "Customer" → Confirms this is a customer contact
- `AccountType__c` = "customer" → Confirms account relationship

### Step 2.1: Salesforce Opportunities

Load and execute:
```
ToolSearch: select:mcp__claude_ai_Zapier__salesforce_find_records_by_query

mcp__claude_ai_Zapier__salesforce_find_records_by_query
  object_type: "Opportunity"
  query: "AccountId = '{ACCOUNT_ID}'"
  fields: "Id, Name, Amount, StageName, CloseDate, Type, Probability, Description, OwnerId"
```

Categorize opportunities:
- **Open Pipeline**: Stage not in (Closed Won, Closed Lost)
- **Renewals**: Type = 'Renewal'
- **Expansions**: Type = 'Expansion' or 'Upsell'
- **New Business**: Type = 'New Business'

### Step 2.2: Salesforce Contacts (EXTERNAL Customer Stakeholders)

```
mcp__claude_ai_Zapier__salesforce_find_records_by_query
  object_type: "Contact"
  query: "AccountId = '{ACCOUNT_ID}'"
  fields: "Id, Name, Title, Email, Phone, Department, Role__c, Job_Title__c, Status__c, AccountType__c"
```

**IMPORTANT**: These are EXTERNAL customer stakeholders, not Docebo employees.

Validation checks:
- Email domain should NOT be `@docebo.com`
- `Status__c` should be "Customer"
- `AccountType__c` should be "customer"

Categorize contacts by role:
- **Executive Sponsor (Customer)**: Title contains 'VP', 'Director', 'Head of', 'C-Level'
- **Champion**: Role__c = 'Champion' or primary platform advocate
- **Technical**: Title contains 'IT', 'Technical', 'System', 'Admin', 'Project Manager'
- **User**: Title contains 'Manager', 'Specialist', 'Lead', 'Officer'
- **Detractor**: Role__c = 'Detractor' (flag for attention)

### Step 2.2b: Extract Internal Account Team from Totango

When querying Totango data (Step 2.5), extract these fields as INTERNAL Docebo team:

```
Account Team Fields (from Totango):
- executiveSponsor → Docebo Executive Sponsor
- accountManager → Docebo Account Manager
- customerSuccessManager → Docebo CSM
- supportAdvisor → Docebo Support Advisor (Elite accounts)
```

**CRITICAL**: These are Docebo employees, NOT customer stakeholders. Display them in a separate "Account Team (Docebo)" section.

### Step 2.3: Slack Account Channel Search

Load and execute:
```
ToolSearch: select:mcp__claude_ai_Slack__slack_search_public_and_private

mcp__claude_ai_Slack__slack_search_public_and_private
  query: "{ACCOUNT_NAME}"
  count: 50
```

Extract from results:
- Recent discussion themes
- Team sentiment indicators
- Escalation mentions
- Success/win mentions
- Risk/concern mentions

### Step 2.4: Glean - Gong Call Intelligence

Load and execute:
```
ToolSearch: select:mcp__claude_ai_Glean_MCP__search

mcp__claude_ai_Glean_MCP__search
  query: "{ACCOUNT_NAME}"
  app_filter: "gong"
```

Extract from Gong results:
- Recent call summaries
- Key stakeholder quotes
- Expansion mentions
- Competitor mentions
- Objections raised
- Next steps discussed

### Step 2.5: Glean - Totango Health Data

```
mcp__claude_ai_Glean_MCP__search
  query: "{ACCOUNT_NAME}"
  app_filter: "totango"
```

Extract from Totango:
- Health score (if available)
- REACH framework data
- Active objectives
- Success milestones
- Risk indicators

### Step 2.6: Glean - Qualtrics NPS Data

```
mcp__claude_ai_Glean_MCP__search
  query: "{ACCOUNT_NAME}"
  app_filter: "qualtrics surveys"
```

Extract from Qualtrics:
- NPS score
- Survey response date
- Verbatim feedback
- Satisfaction ratings

### Step 2.7: Glean - General Account Intel

```
mcp__claude_ai_Glean_MCP__search
  query: "{ACCOUNT_NAME}"
```

Look for:
- Account plans
- Confluence documentation
- Presentations
- Meeting notes
- Strategic initiatives

---

## PHASE 3: Signal Extraction

### Positive Signals (Look For)

| Signal Pattern | Source Priority | Weight |
|---------------|-----------------|--------|
| "renewal confirmed", "renewed", "multi-year" | Salesforce, Slack | High |
| Executive sponsor engagement | Gong, Slack | High |
| "expansion", "additional licenses", "new use case" | Gong, Salesforce | High |
| NPS > 8 | Qualtrics | Medium |
| Health score > 70 | Totango | Medium |
| "successful launch", "go-live", "adoption" | Slack, Gong | Medium |
| Champion advocacy mentions | Gong, Slack | Medium |
| Usage growth indicators | Totango | Medium |

### Risk Signals (Look For)

| Signal Pattern | Source Priority | Weight |
|---------------|-----------------|--------|
| "budget cut", "restructuring", "layoffs" | Slack, Gong | Critical |
| Champion departure | Salesforce, Slack | Critical |
| "competitor", "RFP", "evaluation" | Gong, Slack | High |
| NPS < 7 | Qualtrics | High |
| Health score < 50 | Totango | High |
| "escalation", "executive escalation" | Slack | High |
| "at risk", "churn risk" | Totango, Slack | High |
| Missed objectives | Totango | Medium |
| Support ticket mentions | Slack | Medium |
| Delayed renewal | Salesforce | Medium |

### Expansion Opportunities (Look For)

| Signal Pattern | Source Priority | Weight |
|---------------|-----------------|--------|
| "other departments", "additional teams" | Gong, Slack | High |
| License utilization > 80% | Totango | High |
| New use case discussion | Gong | High |
| Product feature requests | Gong, Slack | Medium |
| Cross-sell product mentions | Gong | Medium |
| "scale", "rollout", "enterprise-wide" | Gong, Slack | Medium |

---

## PHASE 4: Triangulation & Validation

### Stakeholder Validation (CRITICAL)

**Problem**: Names appear in Gong calls and Slack without clear indication if they are internal Docebo employees or external customer contacts. Totango account team fields contain INTERNAL Docebo employees, not customers.

**Validation Process**:

For EVERY name found in Gong or Slack that might be a stakeholder:

1. **Check Glean Employee Search first**:
```
ToolSearch: select:mcp__claude_ai_Glean_MCP__employee_search

mcp__claude_ai_Glean_MCP__employee_search
  query: "{PERSON_NAME}"
```

2. **Interpret Results**:
   - **If found in Glean** → This is a Docebo employee (internal)
     - Check their title/department to categorize (AM, CSM, ES, Support, etc.)
     - Add to "Account Team (Docebo)" section
   - **If NOT found in Glean** → Likely external customer contact
     - Cross-reference with Salesforce Contacts
     - Add to "Customer Stakeholders" section

3. **Email Domain Validation**:
   - `@docebo.com` = Internal Docebo employee
   - Customer domain (e.g., `@thefa.com`, `@google.com`) = External stakeholder

**Totango Account Team Fields (ALWAYS INTERNAL)**:

| Totango Field | Role | Classification |
|---------------|------|----------------|
| `executiveSponsor` | Executive Sponsor | INTERNAL - Docebo executive assigned to account |
| `accountManager` | Account Manager | INTERNAL - Docebo sales representative |
| `customerSuccessManager` | CSM | INTERNAL - Docebo success manager |
| `supportAdvisor` | Support Advisor | INTERNAL - Docebo support (Elite accounts) |

**NEVER list Totango account team fields as customer stakeholders.**

### Stakeholder Output Structure

Generate TWO separate stakeholder sections:

```
ACCOUNT TEAM (DOCEBO)
─────────────────────
  Account Manager: {Name}
  Customer Success Manager: {Name}
  Executive Sponsor: {Name}
  Support Advisor: {Name} (if Elite)

CUSTOMER STAKEHOLDERS
─────────────────────
  Executive/Champion:
    • {Name}, {Title} — Source: {Salesforce/Gong}
  Technical:
    • {Name}, {Title} — Source: {Salesforce/Gong}
  Users:
    • {Name}, {Title} — Source: {Salesforce/Gong}
```

### Confidence Scoring

| Sources Confirming | Confidence Level | Display |
|-------------------|------------------|---------|
| 1 source | Low | "⚠️ Single source" |
| 2 sources | Medium | "✓ Verified" |
| 3+ sources | High | "✓✓ Confirmed" |
| Conflicting data | Flag | "⚡ Conflicting data" |

### Cross-Reference Rules

1. **ARR Validation**: Salesforce is source of truth
2. **Health Score**: Totango is source of truth
3. **NPS**: Qualtrics is source of truth
4. **Stakeholder Identity**: Glean Employee Search for internal/external classification
5. **Customer Contacts**: Salesforce Contacts is source of truth
6. **Account Team**: Totango account fields is source of truth
7. **Pipeline**: Salesforce is source of truth
8. **Recent Activity**: Most recent source wins

### Conflict Resolution

When sources conflict:
1. Note both values in the canvas
2. Cite both sources with dates
3. Flag for human review
4. Recommend which source to trust

---

## PHASE 5: Output Generation

### 5.1: Calculate Summary Metrics

```
Overall Sentiment: [Positive/Neutral/Negative/Mixed]
  - Based on: NPS score, health score, recent Slack/Gong tone

Churn Risk: [Low/Medium/High/Critical]
  - Low: No risk signals, strong renewal indicators
  - Medium: Minor concerns, generally healthy
  - High: Multiple risk signals, needs attention
  - Critical: Active churn indicators, immediate action needed

Expansion Potential: [Low/Medium/High]
  - Based on: Expansion signals, usage patterns, stakeholder interest

Data Freshness: [Current/Stale/Very Stale]
  - Current: Most data < 7 days old
  - Stale: Some data 7-30 days old
  - Very Stale: Data > 30 days old
```

### 5.2: Generate HTML Canvas

Create file at: `/Users/sam.irizarry/Desktop/AI Ops/account-canvases/{account-slug}-canvas.html`

Use the HTML template below, populated with collected data.

### 5.3: Generate JSON Data File

Create file at: `/Users/sam.irizarry/Desktop/AI Ops/account-canvases/{account-slug}-canvas-data.json`

Structure:
```json
{
  "accountId": "...",
  "accountName": "...",
  "generatedAt": "ISO timestamp",
  "lastUpdated": {
    "salesforce": "ISO timestamp",
    "slack": "ISO timestamp",
    "gong": "ISO timestamp",
    "totango": "ISO timestamp",
    "qualtrics": "ISO timestamp"
  },
  "metrics": {
    "arr": ...,
    "nps": ...,
    "healthScore": ...,
    "openPipeline": ...
  },
  "stakeholders": {
    "accountTeam": {
      "description": "Internal Docebo employees assigned to this account",
      "accountManager": {
        "name": "...",
        "email": "...@docebo.com",
        "source": "Totango"
      },
      "customerSuccessManager": {
        "name": "...",
        "email": "...@docebo.com",
        "source": "Totango"
      },
      "executiveSponsor": {
        "name": "...",
        "email": "...@docebo.com",
        "source": "Totango",
        "note": "Internal Docebo executive (ES program)"
      },
      "supportAdvisor": {
        "name": "...",
        "email": "...@docebo.com",
        "source": "Totango"
      }
    },
    "customerContacts": {
      "description": "External customer stakeholders",
      "contacts": [
        {
          "name": "...",
          "title": "...",
          "email": "...@customer-domain.com",
          "role": "Champion|Executive|Technical|User",
          "source": "Salesforce|Gong",
          "validated": true,
          "validationMethod": "Salesforce Contact record|Glean employee search (not found = external)"
        }
      ]
    }
  },
  "signals": {
    "positive": [ ... ],
    "risk": [ ... ],
    "expansion": [ ... ]
  },
  "rawData": {
    "salesforce": { ... },
    "slack": { ... },
    "gong": { ... },
    "totango": { ... },
    "qualtrics": { ... }
  }
}
```

**Stakeholder Validation Notes:**
- `accountTeam` contains ONLY Docebo employees (from Totango account fields)
- `customerContacts` contains ONLY external customer employees
- Each customer contact must have `validated: true` after Glean employee search confirms they are NOT a Docebo employee
- Never mix internal and external stakeholders in the same section

### 5.4: Display Terminal Summary

After generating files, display a summary in the terminal:

```
═══════════════════════════════════════════════════════════════════
                    ACCOUNT INTELLIGENCE CANVAS
                         {ACCOUNT NAME}
═══════════════════════════════════════════════════════════════════

KEY METRICS
───────────────────────────────────────────────────────────────────
  ARR:              ${ARR}
  NPS:              {NPS} ({NPS Category})
  Health Score:     {Health Score}/100
  Open Pipeline:    ${Pipeline Amount}

SENTIMENT SUMMARY
───────────────────────────────────────────────────────────────────
  Overall:          {Positive/Neutral/Negative}
  Churn Risk:       {Low/Medium/High/Critical}
  Expansion:        {Low/Medium/High}

SIGNALS DETECTED
───────────────────────────────────────────────────────────────────
  ✅ Positive ({count}):
     • {Signal 1} — Source: {source}
     • {Signal 2} — Source: {source}

  ⚠️  Risk ({count}):
     • {Signal 1} — Source: {source}

  📈 Expansion ({count}):
     • {Signal 1} — Source: {source}

ACCOUNT TEAM (DOCEBO)
───────────────────────────────────────────────────────────────────
  Account Manager:     {Name}
  CSM:                 {Name}
  Executive Sponsor:   {Name}
  Support Advisor:     {Name}

CUSTOMER STAKEHOLDERS
───────────────────────────────────────────────────────────────────
  Champions/Executives:
     • {Name}, {Title} — {Source}

  Technical:
     • {Name}, {Title} — {Source}

  Users:
     • {Name}, {Title} — {Source}

DATA SOURCES QUERIED
───────────────────────────────────────────────────────────────────
  ✓ Salesforce    — {X} records
  ✓ Slack         — {X} messages
  ✓ Gong          — {X} calls
  ✓ Totango       — {X} records
  ✓ Qualtrics     — {X} responses

FILES GENERATED
───────────────────────────────────────────────────────────────────
  HTML Canvas:  account-canvases/{slug}-canvas.html
  Data JSON:    account-canvases/{slug}-canvas-data.json

═══════════════════════════════════════════════════════════════════
```

---

## HTML Canvas Template

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Account Intelligence Canvas: {{ACCOUNT_NAME}}</title>
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;700&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --docebo-blue: #0057FF;
            --docebo-black: #2A2923;
            --docebo-white: #FFFFFF;
            --docebo-dark: #131E29;
            --docebo-light-blue: #4C8DFF;
            --docebo-navy: #0033A0;
            --docebo-pink: #FF5DD8;
            --docebo-green: #54FA77;
            --docebo-purple: #7E2EE9;
            --docebo-yellow-green: #E3FFAB;
            --docebo-red: #FF4D4D;
            --docebo-orange: #FF9500;
            --neutral-50: #F6F5F2;
            --neutral-100: #EBE6DD;
            --neutral-200: #E1DBD2;
            --neutral-400: #807B74;
            --neutral-600: #56534E;
            --font-heading: 'Space Grotesk', sans-serif;
            --font-body: 'Inter', sans-serif;
            --radius-sm: 6px;
            --radius-md: 10px;
            --radius-lg: 16px;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            font-family: var(--font-body);
            background: var(--neutral-50);
            color: var(--docebo-black);
            line-height: 1.6;
            padding: 32px;
        }

        .canvas-container {
            max-width: 1400px;
            margin: 0 auto;
        }

        /* Header */
        .canvas-header {
            background: linear-gradient(135deg, var(--docebo-blue) 0%, var(--docebo-navy) 100%);
            color: var(--docebo-white);
            padding: 40px;
            border-radius: var(--radius-lg);
            margin-bottom: 24px;
        }

        .header-top {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 24px;
        }

        .account-name {
            font-family: var(--font-heading);
            font-size: 36px;
            font-weight: 700;
        }

        .header-badges {
            display: flex;
            gap: 12px;
        }

        .badge {
            padding: 6px 14px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.05em;
        }

        .badge.risk-low { background: var(--docebo-green); color: var(--docebo-dark); }
        .badge.risk-medium { background: var(--docebo-orange); color: var(--docebo-dark); }
        .badge.risk-high { background: var(--docebo-red); color: var(--docebo-white); }
        .badge.risk-critical { background: var(--docebo-red); color: var(--docebo-white); animation: pulse 2s infinite; }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }

        .header-kpis {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 24px;
        }

        .kpi {
            background: rgba(255,255,255,0.1);
            padding: 16px;
            border-radius: var(--radius-md);
        }

        .kpi-label {
            font-size: 11px;
            text-transform: uppercase;
            letter-spacing: 0.1em;
            opacity: 0.8;
            margin-bottom: 4px;
        }

        .kpi-value {
            font-family: var(--font-heading);
            font-size: 28px;
            font-weight: 700;
        }

        .kpi-source {
            font-size: 10px;
            opacity: 0.6;
            margin-top: 4px;
        }

        /* Grid Layout */
        .canvas-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 24px;
        }

        @media (max-width: 1200px) {
            .canvas-grid { grid-template-columns: repeat(2, 1fr); }
        }

        @media (max-width: 800px) {
            .canvas-grid { grid-template-columns: 1fr; }
        }

        .canvas-section {
            background: var(--docebo-white);
            border-radius: var(--radius-md);
            padding: 24px;
            border: 1px solid var(--neutral-200);
        }

        .canvas-section.full-width {
            grid-column: 1 / -1;
        }

        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 16px;
            padding-bottom: 12px;
            border-bottom: 1px solid var(--neutral-200);
        }

        .section-title {
            font-family: var(--font-heading);
            font-size: 16px;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .section-icon {
            width: 24px;
            height: 24px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
        }

        .freshness-badge {
            font-size: 10px;
            padding: 3px 8px;
            border-radius: 10px;
            background: var(--neutral-100);
            color: var(--neutral-600);
        }

        .freshness-badge.stale {
            background: var(--docebo-orange);
            color: var(--docebo-white);
        }

        /* Signal Lists */
        .signal-list {
            list-style: none;
        }

        .signal-item {
            padding: 12px;
            margin-bottom: 8px;
            border-radius: var(--radius-sm);
            font-size: 14px;
        }

        .signal-item.positive {
            background: rgba(84, 250, 119, 0.1);
            border-left: 3px solid var(--docebo-green);
        }

        .signal-item.risk {
            background: rgba(255, 77, 77, 0.1);
            border-left: 3px solid var(--docebo-red);
        }

        .signal-item.expansion {
            background: rgba(126, 46, 233, 0.1);
            border-left: 3px solid var(--docebo-purple);
        }

        .signal-source {
            font-size: 11px;
            color: var(--neutral-400);
            margin-top: 4px;
        }

        .signal-confidence {
            font-size: 10px;
            padding: 2px 6px;
            border-radius: 4px;
            background: var(--neutral-100);
            margin-left: 8px;
        }

        /* Stakeholders */
        .stakeholder-grid {
            display: grid;
            gap: 12px;
        }

        .stakeholder-card {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 12px;
            background: var(--neutral-50);
            border-radius: var(--radius-sm);
        }

        .stakeholder-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: var(--docebo-blue);
            color: var(--docebo-white);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 600;
            font-size: 14px;
        }

        .stakeholder-avatar.champion { background: var(--docebo-green); color: var(--docebo-dark); }
        .stakeholder-avatar.detractor { background: var(--docebo-red); }

        .stakeholder-info {
            flex: 1;
        }

        .stakeholder-name {
            font-weight: 600;
            font-size: 14px;
        }

        .stakeholder-title {
            font-size: 12px;
            color: var(--neutral-600);
        }

        .stakeholder-role {
            font-size: 10px;
            padding: 2px 8px;
            border-radius: 10px;
            background: var(--docebo-blue);
            color: var(--docebo-white);
        }

        /* Pipeline */
        .pipeline-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px;
            background: var(--neutral-50);
            border-radius: var(--radius-sm);
            margin-bottom: 8px;
        }

        .pipeline-name {
            font-weight: 500;
            font-size: 14px;
        }

        .pipeline-stage {
            font-size: 11px;
            color: var(--neutral-600);
        }

        .pipeline-amount {
            font-family: var(--font-heading);
            font-weight: 700;
            color: var(--docebo-blue);
        }

        /* Footer */
        .canvas-footer {
            margin-top: 24px;
            padding: 16px;
            background: var(--neutral-100);
            border-radius: var(--radius-md);
            font-size: 12px;
            color: var(--neutral-600);
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 16px;
        }

        .footer-sources {
            display: flex;
            gap: 16px;
            flex-wrap: wrap;
        }

        .source-badge {
            display: flex;
            align-items: center;
            gap: 4px;
        }

        .source-badge.success::before {
            content: '✓';
            color: var(--docebo-green);
        }

        .source-badge.failed::before {
            content: '✗';
            color: var(--docebo-red);
        }

        /* NPS Display */
        .nps-display {
            text-align: center;
            padding: 20px;
        }

        .nps-score {
            font-family: var(--font-heading);
            font-size: 48px;
            font-weight: 700;
        }

        .nps-score.promoter { color: var(--docebo-green); }
        .nps-score.passive { color: var(--docebo-orange); }
        .nps-score.detractor { color: var(--docebo-red); }

        .nps-label {
            font-size: 12px;
            color: var(--neutral-600);
            text-transform: uppercase;
            letter-spacing: 0.1em;
        }

        /* Health Score */
        .health-bar {
            height: 8px;
            background: var(--neutral-200);
            border-radius: 4px;
            overflow: hidden;
            margin-top: 12px;
        }

        .health-fill {
            height: 100%;
            border-radius: 4px;
            transition: width 0.5s ease;
        }

        .health-fill.healthy { background: var(--docebo-green); }
        .health-fill.moderate { background: var(--docebo-orange); }
        .health-fill.unhealthy { background: var(--docebo-red); }

        /* Recommended Actions */
        .action-list {
            list-style: none;
        }

        .action-item {
            display: flex;
            align-items: flex-start;
            gap: 12px;
            padding: 12px;
            background: var(--neutral-50);
            border-radius: var(--radius-sm);
            margin-bottom: 8px;
        }

        .action-priority {
            width: 24px;
            height: 24px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 12px;
            font-weight: 700;
            flex-shrink: 0;
        }

        .action-priority.high { background: var(--docebo-red); color: var(--docebo-white); }
        .action-priority.medium { background: var(--docebo-orange); color: var(--docebo-dark); }
        .action-priority.low { background: var(--docebo-blue); color: var(--docebo-white); }

        .action-text {
            font-size: 14px;
        }

        .no-data {
            text-align: center;
            padding: 24px;
            color: var(--neutral-400);
            font-style: italic;
        }
    </style>
</head>
<body>
    <div class="canvas-container">
        <!-- Header -->
        <header class="canvas-header">
            <div class="header-top">
                <h1 class="account-name">{{ACCOUNT_NAME}}</h1>
                <div class="header-badges">
                    <span class="badge risk-{{RISK_LEVEL_CLASS}}">{{RISK_LEVEL}} Risk</span>
                    <span class="badge" style="background: var(--docebo-purple); color: white;">{{SEGMENT}}</span>
                </div>
            </div>
            <div class="header-kpis">
                <div class="kpi">
                    <div class="kpi-label">Annual Recurring Revenue</div>
                    <div class="kpi-value">{{ARR}}</div>
                    <div class="kpi-source">Source: Salesforce</div>
                </div>
                <div class="kpi">
                    <div class="kpi-label">NPS Score</div>
                    <div class="kpi-value">{{NPS}}</div>
                    <div class="kpi-source">Source: Qualtrics</div>
                </div>
                <div class="kpi">
                    <div class="kpi-label">Health Score</div>
                    <div class="kpi-value">{{HEALTH_SCORE}}/100</div>
                    <div class="kpi-source">Source: Totango</div>
                </div>
                <div class="kpi">
                    <div class="kpi-label">Open Pipeline</div>
                    <div class="kpi-value">{{OPEN_PIPELINE}}</div>
                    <div class="kpi-source">Source: Salesforce</div>
                </div>
                <div class="kpi">
                    <div class="kpi-label">Account Owner</div>
                    <div class="kpi-value" style="font-size: 18px;">{{ACCOUNT_OWNER}}</div>
                    <div class="kpi-source">Source: Salesforce</div>
                </div>
            </div>
        </header>

        <!-- Main Grid -->
        <div class="canvas-grid">
            <!-- Positive Signals -->
            <section class="canvas-section">
                <div class="section-header">
                    <h2 class="section-title">
                        <span class="section-icon">✅</span>
                        Positive signals
                    </h2>
                    <span class="freshness-badge">{{SIGNALS_FRESHNESS}}</span>
                </div>
                <ul class="signal-list">
                    {{POSITIVE_SIGNALS}}
                </ul>
            </section>

            <!-- Risk Signals -->
            <section class="canvas-section">
                <div class="section-header">
                    <h2 class="section-title">
                        <span class="section-icon">⚠️</span>
                        Risk signals
                    </h2>
                    <span class="freshness-badge">{{SIGNALS_FRESHNESS}}</span>
                </div>
                <ul class="signal-list">
                    {{RISK_SIGNALS}}
                </ul>
            </section>

            <!-- Expansion Opportunities -->
            <section class="canvas-section">
                <div class="section-header">
                    <h2 class="section-title">
                        <span class="section-icon">📈</span>
                        Expansion opportunities
                    </h2>
                    <span class="freshness-badge">{{SIGNALS_FRESHNESS}}</span>
                </div>
                <ul class="signal-list">
                    {{EXPANSION_SIGNALS}}
                </ul>
            </section>

            <!-- Account Team (Docebo Internal) -->
            <section class="canvas-section">
                <div class="section-header">
                    <h2 class="section-title">
                        <span class="section-icon">🏢</span>
                        Account team (Docebo)
                    </h2>
                </div>
                <div class="stakeholder-grid">
                    {{ACCOUNT_TEAM}}
                </div>
            </section>

            <!-- Customer Stakeholders (External) -->
            <section class="canvas-section">
                <div class="section-header">
                    <h2 class="section-title">
                        <span class="section-icon">👥</span>
                        Customer stakeholders
                    </h2>
                </div>
                <div class="stakeholder-grid">
                    {{CUSTOMER_STAKEHOLDERS}}
                </div>
            </section>

            <!-- Pipeline -->
            <section class="canvas-section">
                <div class="section-header">
                    <h2 class="section-title">
                        <span class="section-icon">💰</span>
                        Active pipeline
                    </h2>
                </div>
                <div class="pipeline-list">
                    {{PIPELINE_ITEMS}}
                </div>
            </section>

            <!-- Recommended Actions -->
            <section class="canvas-section">
                <div class="section-header">
                    <h2 class="section-title">
                        <span class="section-icon">🎯</span>
                        Recommended actions
                    </h2>
                </div>
                <ul class="action-list">
                    {{RECOMMENDED_ACTIONS}}
                </ul>
            </section>

            <!-- Recent Activity -->
            <section class="canvas-section full-width">
                <div class="section-header">
                    <h2 class="section-title">
                        <span class="section-icon">📝</span>
                        Recent activity summary
                    </h2>
                </div>
                <div class="activity-summary">
                    {{RECENT_ACTIVITY}}
                </div>
            </section>
        </div>

        <!-- Footer -->
        <footer class="canvas-footer">
            <div class="footer-sources">
                <span class="source-badge {{SALESFORCE_STATUS}}">Salesforce</span>
                <span class="source-badge {{SLACK_STATUS}}">Slack</span>
                <span class="source-badge {{GONG_STATUS}}">Gong</span>
                <span class="source-badge {{TOTANGO_STATUS}}">Totango</span>
                <span class="source-badge {{QUALTRICS_STATUS}}">Qualtrics</span>
            </div>
            <div class="footer-timestamp">
                Generated: {{GENERATED_TIMESTAMP}} | Account ID: {{ACCOUNT_ID}}
            </div>
        </footer>
    </div>
</body>
</html>
```

---

## Options

### Full Refresh (`--full`)
Queries all data sources and regenerates the entire canvas, ignoring cached data.

### Pipeline Only (`--pipeline`)
Updates only the Salesforce opportunities section. Useful for quick pipeline reviews.

### Signals Only (`--signals`)
Updates only the signals sections (Slack, Gong, Totango mentions). Skips pipeline and stakeholder refresh.

---

## Error Handling

| Scenario | Response |
|----------|----------|
| Account not found in Salesforce | Display similar accounts, ask user to clarify |
| Multiple accounts match | Show numbered list with ARR/Owner, use AskUserQuestion |
| Salesforce query fails | Cannot proceed; this is required data |
| Slack search returns nothing | Note "No Slack discussions found" in output |
| Gong returns no results | Note "No Gong calls found" in relevant sections |
| Totango returns no results | Display "Health score: Not available" |
| Qualtrics returns no results | Display "NPS: Not available" |
| Data conflict detected | Show both values with sources, flag for review |

### Stakeholder Validation Errors

| Scenario | Response |
|----------|----------|
| Totango Executive Sponsor is a Docebo employee | **CORRECT** - Add to Account Team section (this is expected behavior) |
| Gong participant found in Glean Employee Search | This is a Docebo employee; add to Account Team, NOT customer stakeholders |
| Name found in Gong but NOT in Glean or Salesforce | Flag as "Unverified participant"; note for manual review |
| Salesforce Contact has @docebo.com email | Data quality issue; exclude from customer stakeholders, flag for CRM cleanup |
| Stakeholder appears in both internal and external lists | Investigate; likely data entry error. Use Glean as source of truth for internal status |

---

## Verification Checklist

Before generating final output, verify:

- [ ] Account name matches Salesforce record exactly
- [ ] ARR figure is from Salesforce (source of truth)
- [ ] At least 2 of 5 data sources returned results
- [ ] All signals have source citations with dates
- [ ] Pipeline data matches current Salesforce state
- [ ] No critical data conflicts left unresolved
- [ ] HTML file validates (no broken template variables)
- [ ] JSON data file is valid JSON

### Stakeholder Validation Checklist (CRITICAL)

- [ ] **Account Team section contains ONLY Docebo employees**
  - Executive Sponsor from Totango = Docebo executive (verified via Glean)
  - Account Manager from Totango = Docebo AM (verified via Glean)
  - CSM from Totango = Docebo CSM (verified via Glean)

- [ ] **Customer Stakeholders section contains ONLY external contacts**
  - All listed contacts have customer email domain (NOT @docebo.com)
  - All contacts exist in Salesforce Contacts for this account
  - Any Gong participants were validated via Glean Employee Search

- [ ] **No internal Docebo employees listed as customer stakeholders**
  - Run `mcp__claude_ai_Glean_MCP__employee_search` for any uncertain names
  - If found in Glean = Docebo employee = Account Team (not customer)

- [ ] **Stakeholder sources are accurately cited**
  - Salesforce Contact = "Salesforce"
  - Gong call participant (validated as external) = "Gong"
  - Totango account team field = "Totango" (for Account Team section only)

---

## Example Invocations

```bash
# Generate full canvas for Google
/account-intelligence-canvas Google

# Generate canvas for account with spaces
/account-intelligence-canvas "Palo Alto Networks"

# Force full refresh, ignoring any cached data
/account-intelligence-canvas Honeywell --full

# Quick pipeline update only
/account-intelligence-canvas Google --pipeline

# Update signals only (Slack, Gong, etc.)
/account-intelligence-canvas Google --signals
```
