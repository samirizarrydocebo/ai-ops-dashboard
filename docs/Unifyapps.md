# UnifyApps at Docebo: from experiment to GTM operating system

**In under nine months, Docebo's AI Operations team transformed UnifyApps from an unpaid pilot into a production platform powering six live GTM intelligence applications, with four more in final testing.** The initiative has already delivered measurable impact — **$2M in forecasted incremental ARR** from Audience Insights alone, **~200 lost opportunities auto-classified monthly** at 95% accuracy through Churn Analysis AI, and a modeled **$15.4M in annual productivity value** across the broader AI stack. With the MSA finalized in January 2026, a formal governance structure now in place, and platform migration to Docebo's own cloud underway, UnifyApps has moved from vendor evaluation to a foundational layer of Docebo's go-to-market intelligence infrastructure.

This report synthesizes data from internal steering committee minutes, daily sync notes, weekly status reports, budget documents, PRDs, and executive strategy decks spanning August 2025 through February 2026.

---

## The strategic bet: why UnifyApps and why now

Docebo's AI Operations team, led by Director Sam Irizarry, identified a critical gap in the company's technology stack: **40–50% of seller time was consumed by manual administrative tasks**, and **$5M+ in sales tools sat underutilized** across fragmented systems. The team needed a platform capable of building complex, multi-system applications that could unify data from Salesforce, Gong, Snowflake, Zendesk, Totango, Qualtrics, and Slack into actionable intelligence.

UnifyApps was selected as the "high-complexity lane" in a deliberate two-lane AI strategy. **Lane 1 (Platform AI)** uses UnifyApps for multi-system, bespoke applications requiring deep data integration — the kind of apps that no single tool could handle alone. **Lane 2 (Self-serve AI)** leverages Glean (600+ monthly active users, 140+ custom agents) and Zapier (50+ workflows in production) for lighter automation. The principle is clean: "UnifyApps = few, complex, shared apps; everything else should live in tools you already use."

UnifyApps itself is a well-capitalized enterprise AI startup — **$81M in total funding**, a **$250M valuation** at its October 2025 Series B, and Sprinklr founder Ragy Thomas serving as Co-CEO. The platform provides 700+ enterprise connectors, multi-LLM support, and a no-code/low-code builder purpose-built for AI from inception. Its differentiator against legacy iPaaS tools like Workato or MuleSoft is this AI-native architecture, combining data unification, workflow automation, app building, and agentic AI in a single platform.

Notably, **UnifyApps performed nine months of unpaid work** before the MSA was finalized in mid-January 2026. The contract — valued at approximately **$150K/year for the enterprise license** plus ~$130–150K in contractor and infrastructure costs (total direct spend: **$280–300K annually**) — was the last hurdle cleared, with liability cap negotiations resolving at $1M for confidentiality breaches given Docebo's status as a public company handling sensitive financial data.

---

## Six live applications delivering real impact today

As of the Week 2 status report (January 14, 2026), the overall UnifyApps project status is **GREEN** with **six use cases live**, four in UAT, one in build, and one in discovery. Here is what each live application does and what it has delivered.

### Audience Insights AI — the crown jewel

This marketing intelligence engine is the strongest ROI story in the portfolio. It analyzes **4,000+ demo calls** recorded since January 2024 via Gong, producing a daily-refreshed voice-of-customer cockpit that surfaces customer pain points, competitor mentions, messaging effectiveness, and market signals. The Marketing team uses it as their primary research tool. One marketing stakeholder stated: *"I use this daily. It is my go-to resource for voice of customer. It bridges the gap between raw data and actionable insight."*

The impact modeling is compelling. Silvia Valencia presented to the E-team a forecast of **$2M in incremental ARR** (representing 20% of annual new business ARR) and **$3M in incremental pipeline within six months**. A detailed impact deck modeled **$3.3M in incremental pipeline** from AI-informed messaging tests based on a 15% uplift across a 442-SQO sample, with upside scenarios reaching **$9.05M at scale**. Additionally, **$5M in pipeline opportunities** has been attributed to Audience Insights in connection with the Skills initiative. Target efficiency gains include a 50% reduction in pre-meeting research time, 40% faster time-to-market for new messaging, and 45% faster reaction to competitor moves. The app was adopted into Q4 2025 OKRs and is now evolving toward embedded-in-work delivery through Slack notifications with action buttons and Salesforce embedding.

### Churn Analysis AI — standardizing loss intelligence at scale

Deployed on **September 15, 2025** after a month-long validation phase, this application automatically triggers when opportunities are marked closed-lost in Salesforce. It pulls data from four to six sources per analysis (Salesforce, Gong, Snowflake, Zendesk, Slack, email) and classifies churn reasons with **~95% accuracy**, auto-writing standardized reasons back into Salesforce. It processes **~200 lost opportunities per month** — covering renewals, upsells, and new business — eliminating reliance on inconsistent manual close/lost notes. A Glean Churn Analysis agent layers on top for deeper narrative and recommendations. V1 testing in August 2025 was described as "highly successful" with strong accuracy and user satisfaction. A feedback mechanism (thumbs up/down) tracks quality continuously.

### Leadership Engagement Tracker, Account Research, Market Research, and VOC 360 V1

The remaining live applications round out the portfolio. The **Leadership Engagement Tracker** is fully operational. **Account Research** went live in Q3 2025 but was placed on strategic pause in September after user feedback that insights were "not detailed enough" and a 15-minute processing time blocked adoption — it is being rebuilt into a unified "Dynamic Playbook Builder" with automated triggers. **Market Research** shipped as an MVP. **External Voice of Customer 360 V1** went live on December 24, 2025, completing Phase 1 NPS ML categorization, with CEO Alessio requesting verbatim quote features now being scoped for the migration rebuild.

---

## Four applications approaching launch in Q1 2026

### Digital Business Review — scaling QBR coverage 10x

The Digital BR and its companion One-Pager are the highest-impact applications in UAT, currently being tested with 3–5 CSMs and targeting a February 2026 go-live. The business case is straightforward: **~1,000 unassigned commercial and foundational accounts** currently receive no structured business reviews because CSMs spend **60–90 minutes** manually prepping each one. The Digital BR auto-generates QBR decks by pulling from Salesforce, Gong, Snowflake, Totango, and Qualtrics data. Target impact includes a **60% reduction in QBR prep time** (to under 30 minutes), a **60% increase in account coverage**, and a **20% faster time-to-value** for new accounts. At scale, the model suggests **2–3 points of GRR improvement** and **$1.5M in expansion pipeline**. Current testing shows 50% prep time reduction already achieved, though data accuracy remains a work-in-progress — V2 accuracy improved over V1's 38% baseline but has not yet crossed the 50% threshold consistently. The team is focused on data quality and template finalization before broader rollout.

### Competitive Intelligence Dashboard and VOC 360

The **Competitive Intelligence Dashboard** received 11 rounds of feedback (all addressed) and awaits final sign-off for January 2026 go-live. The **VOC 360** full version received 32 feedback items with 28 addressed and is being rebuilt during the cloud migration to incorporate E-team feedback.

---

## Two high-value applications in active development

### Cross-functional account handoff automation

This is arguably the most strategically important initiative in the pipeline, directly addressing the finding that **reps spend ~50% of their time on business analyst tasks** — manual data entry, account research, and context switching across fragmented tools. The vision encompasses **six handoff agents** spanning the full customer lifecycle: Marketing→BD, BD→AE, AE→SC, AE→PS, PS→CSM, and CSM→AM.

The **AE-to-PS Handoff Agent** is furthest along, with an MVP completed and Show & Tell delivered on January 10, 2026. It executes an 11-step automated workflow: searching Salesforce, reading Gong transcripts, pulling Google Drive artifacts and Slack threads, then synthesizing everything into a structured Implementation Handoff document covering contract/commercials, stakeholder maps, timelines, technical scope, data migration, security, risks, and commitments. The output auto-generates a Google Doc saved to customer project folders. Four to five output variations have been tested with the PS champion. The BD→AE Handoff Brief has comprehensive prompts documented. Three agents are ready for validation as of February 11, 2026.

Projected impact is substantial. The GTM Handoff Automation line in the 2026 budget models **$6.2M in annual productivity value** (14–20 hours returned per week × 150 users × $55/hour). The accompanying UAIP PRD targets a **20% reduction in Customer Acquisition Cost**, with specific efficiency targets including SOW creation dropping from 30 minutes to 5 minutes (83% reduction), RFP responses from 40 hours/week to 12 (70% reduction), and call preparation from 15 minutes to 3 (80% reduction). Handoff SLAs are defined: BD→AE within 8 business hours, AE→PS within 24 hours, PS→CSM within 48 hours, CSM→AM within 30 days.

### Solution Blueprint Generation Agent

Targeting the 60-person Solutions Consulting and Architecture team (28 SCs + 32 SAs), this agent automates creation of the detailed solution blueprint presentations that currently take multiple days to produce as 100+ page documents. The BRD was completed in January 2026, with backend configuration running through January 31 and frontend configuration through February 7. **Target go-live is March 7, 2026**, with a projected **90% reduction in first-draft creation time** and a 25% reduction in overall blueprint turnaround time.

---

## The financial picture: $280K investment against $15.4M in modeled value

The 2026 AI budget request totals **$1.54M–$1.77M** (net $1.24M–$1.45M after $300K in tool retirement savings), with UnifyApps representing a focused investment within this envelope.

| Component | Annual Cost |
|---|---|
| UnifyApps Enterprise License (unlimited users/apps) | $150K |
| UnifyApps contractors (2 FTEs) | $50K |
| AWS + Anthropic infrastructure | $80–100K |
| **Total UnifyApps direct spend** | **$280–300K** |

Against this investment, the productivity value model calculates **$15.4M annually** across the full AI stack, with UnifyApps GTM Handoff Automation alone contributing **$6.2M**. The broader UAIP business case models a **$400–500K annual investment** (including 4 FTE team expansion) delivering a **payback period of 8 months** and **3-year ROI of 300%+**. Tool consolidation savings — Pingboard, Totango, and Tableau functionality shifting into UnifyApps and Glean — contribute approximately **$300K/year** in direct savings. The overall portfolio targets a **10x+ ROI multiple**.

It is important to note that these are modeled projections, not validated actuals. The Audience Insights pipeline numbers ($3.3M–$9.05M) are scenario-based, and the productivity value calculations use estimated time savings and hourly rates. Finance validation of these models has not been completed. However, the Audience Insights presentation to the E-team received notably fewer ROI challenges than typical, suggesting executive confidence in the directional accuracy.

---

## Governance matured rapidly in January 2026

A formal three-tier governance structure was established in January 2026, reflecting the initiative's transition from experimental to operational:

- **Monthly SF & AI Executive Steering Committee** (first meeting January 14, 2026): Attended by CIO Nitin Chopra, CRO Mark Kosoglow, Senior Director IT Marco Bettineschi, and the AI Ops leads. Owns prioritization, trade-offs, and capacity guardrails. Makes quarterly decisions on which 2–3 UnifyApps use cases to invest in per quarter.
- **Weekly AI Initiative Steering Committee** (inaugurated January 16, 2026): Cross-functional group including representatives from Marketing, CS, Sales Enablement, and RevOps. Manages project status, blockers, and alignment.
- **Daily UnifyApps Sprint Calls** (ongoing since mid-2025): Samuel Adams serves as internal product owner/SME, running 7:00 AM EST syncs with the full UnifyApps development team.

Capacity planning follows t-shirt sizing: Small (4–5 weeks), Medium (5–7 weeks), Large (8–9 weeks), XL (10+ weeks). **Realistic quarterly throughput is approximately 4–5 use cases** — roughly one Large, three Medium, and one Small — translating to **~20 use cases per year** at full capacity. A formal intake process with a 2-day SLA and consultative assessment (determining whether a request belongs in UnifyApps, Glean, or Zapier) prevents scope creep and ensures the highest-value work gets prioritized.

---

## Challenges confronted and lessons emerging

The initiative has not been without friction, and acknowledging these challenges honestly is important for strategic planning.

**Data quality remains the critical bottleneck.** The Digital BR's accuracy staying below 50% through V2 testing illustrates that AI applications are only as good as their underlying data. Megan Eckhardt raised concerns that launching with poor data quality could damage user trust — a valid risk that the team is actively addressing through Salesforce hygiene improvements and quality thresholds (~80% data quality target).

**Executive alignment on AI tool strategy is still evolving.** CRO Mark Kosoglow candidly stated at the January 14 steering committee: *"I feel kind of paralyzed with AI here right now"* — citing multiple platforms producing inconsistent results. He also pushed for faster execution: *"We go way too f---ing slow."* This tension between speed and coherence is healthy but requires continued governance attention.

**Technical blockers persist.** Snowflake intermittent access errors (every 2–3 days), IAM permission constraints preventing admin roles for UnifyApps users, and unresolved LLM API key management and cost tracking all create operational friction. The platform migration to Docebo's AWS environment — approved January 30, 2026 and beginning in February — will help resolve some of these issues but introduces its own validation complexity as each application requires individual testing for functionality, data completeness, and integration connections.

**Adoption beyond power users requires deliberate design.** Silvia Valencia's observation that "beautiful dashboards with amazing insights often die there" unless they drive specific user actions led to a strategic shift: evolving apps from standalone dashboards to embedded-in-work experiences with Slack notifications, Salesforce integration, and action buttons. The Account Research agent's pause — triggered by a 15-minute processing time that killed adoption despite quality output — reinforced that **user experience is as important as intelligence quality**.

**The shift from exploration to justification is real.** As Valencia noted, 2025 was "explore freely" while 2026 demands "justify everything." The team is adapting by delivering proof in "little snack pieces" to build executive trust incrementally rather than waiting for comprehensive ROI validation.

---

## What comes next: a platform at an inflection point

The UnifyApps initiative at Docebo stands at a genuine inflection point. The AI Ops team has gone from what Sam Irizarry describes as "AI experiments" to the **"operating system for GTM intelligence and automation"** in roughly six months. Six applications are live and producing value. The contract is signed. Governance is formalized. The cloud migration will give Docebo full control of the environment.

Three strategic questions will define the next phase. First, **the centralized vs. embedded AI team model**: CIO Nitin Chopra raised in February 2026 whether the current centralized AI Ops team should evolve toward embedded AI specialists within each functional team. This architectural decision will fundamentally shape how fast UnifyApps capabilities scale across the organization. Second, **the 2–3 use case per quarter constraint** means prioritization discipline is paramount — the steering committee's quarterly choices will determine whether UnifyApps impact stays contained to early adopters or expands across the full GTM organization. Third, **the competitive tool landscape is shifting fast**: team members have noted that tools like Lovable could bypass UnifyApps for simpler internal applications, requiring continued clarity on where UnifyApps uniquely adds value versus lighter alternatives.

The bottom line for Docebo's leadership is this: a $280–300K annual investment has produced a production AI platform with six live applications, a governance model, and a pipeline of high-value use cases with modeled impact in the tens of millions. The early returns — particularly Audience Insights' $2M ARR forecast and Churn Analysis' automated classification of 200+ monthly lost opportunities — validate the strategic bet. The challenge now is not whether UnifyApps works, but whether Docebo can execute fast enough to capture the full value of what has been built.