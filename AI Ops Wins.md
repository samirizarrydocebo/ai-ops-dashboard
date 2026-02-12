## **Executive Summary (where we are now)**

In the last \~6–7 months, AIOps has effectively gone from “AI experiments” to the **operating system for GTM intelligence and automation**. The pattern across the work is clear:

* You’ve stood up an **AI stack** (Glean \+ UnifyApps \+ Zapier \+ Granola) and turned it into concrete, high‑usage products.  
* You’ve **orchestrated wins for other teams** — especially Marketing, RevOps, CS, and Sales — via solution design, program management, and enablement, not just by “owning a tool.”  
* You’ve put real **governance and operating model** in place (steering committees, exec steering, project inventory, intake), which is a big part of why things are now moving in a more predictable way.

This reply gives you:

1. A synthesized storyline of AIOps impact in the last \<1 year.  
2. A proposed **one‑page exec dashboard structure** keyed to that story.  
3. A set of **specific clarifying questions and data asks** for you (and likely Amanda / Sam Adams / RevOps) before I draft the final exec‑ready one‑pager.

---

## **1\. Current AIOps Impact Storyline (Last \<1 Year)**

### **1.1. AIOps as orchestrator of the AI stack**

Across everything, the through‑line is: **AIOps is the orchestrator and product owner for the AI stack**, not “the team that owns some bots.”

* You are the primary driver behind **Glean as the enterprise knowledge and agent platform**, including pilots, buy vs build decisions, and the enablement programs that led to \~600+ monthly active users and \~70% employee coverage, with GTM functions (CS, AE/AM, Support, Product, RevOps, Enablement) among the heaviest adopters.  
* You sponsored and shaped the **UnifyApps platform** (SP‑29), moving it from a vendor eval into a horizontal platform with **4 core GTM apps** (Audience Insights, Account Research, Churn Analysis, Digital BR/QBR Generator) plus supporting chat agents — all managed under a coherent AI initiatives roadmap.  
* You drove **Zapier** from “approved tool” into a widely‑adopted automation layer (50+ workflows in production, strong early credit consumption) and wrapped it in enablement (Zapier Bootcamp, internal AI Hub, templates).

This gives you a legitimate **platform narrative**: AIOps as the function that made the AI stack real, integrated, and safe to bet on.

---

### **1.2. Flagship win 1: Glean as GTM’s default knowledge & agent layer**

For the exec audience, Glean is your cleanest, most mature “this is already working” story.

**What’s true today**

* **Adoption & coverage**

  * \~**600+ MAU, 420 WAU, \~70% coverage** across the company, with strong stickiness (69% WAU/MAU).  
  * Department‑level data shows **\>80% active usage** in key GTM clusters: Solutions Engineering, Support, AEs, AMs, CX/PS, Product Management, and Product Marketing.  
* **Agent ecosystem & behavior change**

  * \~**140+ custom agents**, **180+ monthly agent users**, **140+ shared agents**, used heavily by GTM roles.  
  * Usage patterns show a shift from “search” to “assistant”: \~**5 AI chats/week vs 2.7 keyword searches/week per user**.  
* **Tangible agents with stories**

  * **Churn Analysis agent**: pulls together SFDC, Gong, Zendesk, Slack, email to generate full loss narratives and recommendations — used as the analyst layer on top of the UnifyApps churn app.  
  * **Product FAQ agent**: validated a **93% reduction in search time** (15 minutes → \<1 minute), \~**2 hours/week saved per rep**, 600 runs by 90 users, and **100 NPS** from pilot users; organic adoption in CX shows cross‑team pull once good agents exist.  
  * Other high‑run agents like **Next Step Helper, Renewal Plan Generator, Executive Brief, Docebo Learn Data Assistant** are directly tied to revenue and CS workflows.  
* **Enablement model**

  * **Glean Agent Builder Cohort**: 11 certified builders, 11+ production agents, plus Q4 metrics of **173 shared agents** and **160 monthly agent users** in a key GTM cluster, with CX adoption at \~86%.

**How this plays for execs**

You can credibly say: “We took Glean from pilot to **core GTM infrastructure** that 70% of employees use, with a growing ecosystem of revenue‑tied agents and an enablement program that scales beyond just the AIOps team.”

To make this airtight, we’ll want slightly fresher usage exports (see questions below).

---

### **1.3. Flagship win 2: UnifyApps intelligence portal for GTM (Audience Insights, Churn, Digital BR, VOC)**

This is the **“AI apps on top of our data foundation”** story.

**Audience Insights AI (Marketing)**

* **Live, widely adopted** by Marketing; analyzes **4,000+ demo calls** since Jan 2024 via Gong and produces deep‑dive insights on topics, pains, competitors, etc., refreshed daily.  
* Targeted outcome metrics: **50% reduction in pre‑meeting research time**, **40% faster time‑to‑market for new messaging**, **45% faster reaction to competitor moves**.  
* Recent impact deck models **\~$3.3M incremental pipeline** from AI‑informed tests (15% uplift on a 442‑SQO sample), with upside scenarios up to **$9.05M pipeline** at scale (scenario math, but good directional story).  
* Strong quote from Marketing: “**I use this daily. It is my go‑to resource for voice of customer. It bridges the gap between raw data and actionable insight.**”

**Churn Analysis AI / closed‑lost intelligence**

* **UnifyApps app** is live, analyzing **\~200 lost opportunities per month** with **\~95% classification accuracy**, and auto‑writing standardized churn reasons into Salesforce.  
* The **Glean Churn Analysis agent** sits on top to provide deeper narrative and recommendations per opp using Salesforce, Gong, Zendesk, Slack, and email.

**Digital BR & One‑Pager for CS**

* Baseline: **hundreds to \~1,000 accounts** were effectively going without structured QBRs / business reviews.  
* New UnifyApps apps (**Digital BR v2.0 \+ One‑Pager Digital BR**) auto‑generate decks and one‑pagers from Snowflake, Totango, Gong, Salesforce, Qualtrics, etc., with:  
  * **60% reduction in QBR prep time** target (90 minutes → \<30 minutes).  
  * **60% increase in account coverage** for reviews and **20% faster time‑to‑value** for new accounts.  
* As of Jan–Feb 2026: in **UAT** with \~3–5 CSMs, targeting go‑live in February and focused on data quality \+ template finalization.

**VOC & Skills**

* **VOC Insights & Customer 360**: Phase 1 (NPS ML categorization in Qualtrics) completed; multi‑phase plan under way to bring together NPS, CSAT, Gong, Totango, SFDC, Zendesk, Ideas, etc.  
* **Skills Signal Intelligence** directive from Nitin: 7‑day UnifyApps sprint to analyze Q3/Q4 Gong calls for high‑value deals and compute “Revenue at Risk” from skills‑platform demand — this is still R\&D / planning but strategically important for the exec narrative.

**How this plays**

This cluster lets you say: “We built an **AI intelligence fabric** over Gong, SFDC, Totango, Qualtrics, and more — and used it to change how Marketing, CS, and RevOps make decisions, not just to ‘summarize calls’.”

Again, tightening realized vs target metrics will matter, especially for pipeline and GRR/NRR improvements.

---

### **1.4. Flagship win 3: Governance & operating model**

You’ve also done a lot of invisible but high‑leverage work to **professionalize how AI and GTM ops get run**.

* Established:

  * **AI \+ Salesforce Executive Steering Committee** (monthly, 60 minutes) for exec‑level prioritization and trade‑offs.  
  * **Weekly SFDC/BT/AI syncs** and **AI Initiatives Steering** working session for champions.  
  * **Daily UnifyApps sprint calls** with two FTE project leads and a PM on the vendor side; Sam Adams acting as internal product owner/SME.  
* Defined **capacity and intake**:

  * Clear statement: UnifyApps can do **\~4–5 use cases per quarter**, with size tiers (S/M/L/XL/Beta) and lifecycle stages (Discovery → Build → UAT → Go‑live).  
  * **Rev Team SFxAI Project Inventory** spreadsheet tracks 20+ AI projects, connectors, and agents with status and ownership, giving execs a single view of what’s in flight and what’s delivered.  
* Clarified **role boundaries**:

  * AIOps/SFDC: tooling decisions, technical design, integration, AI governance, telemetry.  
  * RevOps: process & KPI ownership.  
  * Enablement: adoption, training, and feedback loops.

In your own DM to Nitin you summed this up perfectly as **“orchestrators/facilitators that have unlocked wins for other teams—not necessarily ours.”**

This is the right spine for the deck: your value is leverage on other teams’ outcomes.

---

### **1.5. Flagship win 4: Zapier & enablement as a force multiplier**

Finally, on the “tooling \+ enablement” axis:

* AIOps is credited with **50+ workflows in production** across GTM, Support, CS, and Finance, backed by early Zapier credit consumption (88k of 600k credits in 2 months, projected 200k+ usage).  
* You ran the **Zapier AI Bootcamp** (Dec 4, 2025), plus a published **Zapier Enablement Guide** and an **Internal AI Hub** section, teaching FAR (Frequent, Annoying, Repeatable) and walking teams through building one AI workflow \+ one AI agent each.  
* Concrete stories like the **Granola → Drive → Slack automation** you taught to Jessica Knapp show that you’re not just doing abstract enablement; you’re teaching leaders to run on AI‑first workflows personally.

This is the “we changed how people work day‑to‑day” dimension.

---

## **2\. Proposed One‑Page Exec Dashboard Structure**

Below is a structure tuned for a **single slide / one‑pager**. We can absolutely iterate, but this gives us a concrete starting point.

### **2.1. Overall frame**

**Title (center‑top)**  
 “AI Ops: From Pilots to GTM Infrastructure (Aug 2025 – Feb 2026)”

**Sub‑title**  
 “How a 6‑month‑old team orchestrated GTM‑wide AI wins across tooling, intelligence, and operating model”

---

### **2.2. Top band: One‑sentence positioning \+ 3 KPIs**

**Left: Positioning statement**

“AIOps is the orchestrator of Docebo’s AI stack — turning Glean, UnifyApps, and Zapier into production GTM systems that accelerate Marketing, Sales, CS, and RevOps.”

**Right: 3 headline metrics (big numbers)**

* **600+** monthly Glean users, **70%+ coverage**, **140+ agents** live  
* **4 core UnifyApps GTM apps** in production (Audience Insights, Account Research, Churn, Digital BR)  
* **50+ Zapier workflows** live across GTM/CS/Finance

(We’ll refine exact numbers from updated exports.)

---

### **2.3. Middle section: “Flagship wins” tiles (2 × 2 grid)**

Each tile \= a compact block with:

* **Title**  
* **1 headline metric / outcome**  
* **2–3 bullet micro‑points**  
* Optional quote

**Tile 1 – Glean: GTM’s AI teammate**

* Headline metric: “600+ MAU, 69k+ queries in 6 months; 140+ agents and 180+ monthly agent users.”  
* Bullets:  
  * 80%+ adoption in CS, AE, AM, Support, PM, PMM.  
  * Churn, Renewal Plan, Product FAQ, and Executive Brief agents now embedded in renewal, churn, and prep workflows.  
  * 11 certified builders; 173 shared agents; CX at 86% adoption.

**Tile 2 – Audience Insights AI (Marketing)**

* Headline metric: “4,000+ demo calls analyzed; daily‑refreshed VOC cockpit for Marketing.”  
* Bullets:  
  * Targets: 50% research‑time reduction, 40% faster messaging, 45% faster reaction to competitors.  
  * Used daily by Marketing as their go‑to VOC source; one user quote front and center.

**Tile 3 – Churn Analysis & Digital CS**

* Headline metric: “\~200 lost opps/month auto‑classified at \~95% accuracy; Digital BR & One‑Pager engines in UAT targeting 60% QBR prep‑time reduction.”  
* Bullets:  
  * Standardized churn reasons feeding SFDC and Glean for macro and micro analysis.  
  * New ability to serve \~1,000 historically under‑served accounts with automated business reviews.

**Tile 4 – Operating model & automation**

* Headline metric: “AI \+ Salesforce exec steering \+ weekly AI initiatives \+ daily UnifyApps sprints governing 20+ AI projects.”  
* Bullets:  
  * 50+ Zapier workflows in production; 88k of 600k credits used in \~2 months.  
  * Clear swimlanes between AIOps, RevOps, Enablement, and GTM; sample‑group model for iterative rollouts.

---

### **2.4. Bottom band: “What’s next” \+ positioning quote**

**Left: 3 “next bets”**

* **Scale Glean & agents**: push to 80%+ adoption in GTM, double usage of top agents, and expand certified builder cohorts.  
* **Operationalize Digital CS & VOC**: move Digital BR/One‑Pager and VOC dashboards from UAT → scaled programs, tied to GRR/NRR metrics.  
* **Skills Signal Intelligence**: deliver the back‑test and dashboards that put a dollar figure on skills‑platform demand.

**Right: Quote**

Use either:

* Your own line to Nitin:  
   “We’ve been the orchestrators/facilitators that have unlocked wins for other teams — not necessarily ours.”

or

* A CRO/Marketing quote (e.g., Audience Insights or Mark’s “amazing update / excited for progress” message) as the closer.

---

## **3\. Clarifying Questions & Data Requests (for a board‑grade version)**

You asked explicitly for clarifying questions before I complete the final report. Here are the most important ones, prioritized.

### **3.1. Audience, scope, and angle**

1. **Exact audience and meeting**

   * Is this for the **full exec team** (Alessio \+ all C‑levels) or for a more focused forum (e.g., AI Steering \+ a few execs)?  
   * Will you be **presenting live** and speaking to the slide, or is this also meant to stand alone in an email pre‑read?  
2. **What you want them to walk away believing**  
    Rank these in order of importance for you:

   * “AIOps is delivering **measurable revenue / pipeline / retention impact**.”  
   * “AIOps has built a **scalable, governed AI platform** (stack \+ operating model).”  
   * “AIOps is **under‑resourced relative to demand**; we need more capacity / headcount / budget.”  
   * “AIOps should be the **go‑to partner** when teams want to do AI work (not shadow experiments).”  
3. **Time window**  
    You mentioned the team formally started Aug 1; tools show most of the visible impact from **Aug 2025–Feb 2026**. Do you want:

   * Strictly “**since Aug 1, 2025**”, or  
   * “**Last 12 months**” where some early Glean/UnifyApps work from mid‑2025 is allowed for context, but emphasis remains on the last 6–7 months?

---

### **3.2. Glean: data & framing**

4. **Admin export / report**  
    Can you or Sam Adams provide **the latest Glean admin export** (as of Feb 2026\) that includes:

   * MAU / WAU by department or group (especially GTM vs non‑GTM)  
   * Agent usage: runs and unique users by agent, by month  
   * Overall search/chat volume and satisfaction  
5. Even a CSV or screenshot is great; I can work from that.

6. **Value framing preference**  
    For Glean, do you want to emphasize:

   * **Time saved** (e.g., “Product FAQ agent cuts search time by 93%; Glean saves X hours/month”),  
   * **Quality / risk** (e.g., fewer bad customer responses, better ramp),  
   * Or **behavior change** (“agents as teammates,” cross‑team knowledge sharing)?  
7. I can include all three, but the headline will land harder if we pick one as primary.

---

### **3.3. UnifyApps: realized vs target impact**

6. **Audience Insights realized impact**  
    Amanda’s materials include strong scenario modeling (e.g., $3.3M pipeline uplift on a test cell). Are there **one or two concrete experiments** where:

   * We can say: “Campaign X that used Audience Insights outperformed control by Y% in metric Z”?  
   * Even directional (e.g., “+10–15% email reply rate”) is helpful, as long as it’s a real result.  
7. **VOC / Skills**  
    For VOC and Skills Signal:

   * Is the expectation that we **reference them as strategic bets** (in progress) rather than current wins?  
   * Are there any early VOC insights or decisions that you’d want highlighted (even if small), or should we keep it future‑oriented?

---

### **3.4. CS Digital BR / One‑Pager & churn**

8. **Current UAT metrics (if available)**  
    Do you have — or can you get from CS/RevOps or UnifyApps — early numbers such as:

   * **of QBR decks generated in UAT**

   * **of one‑pagers generated**

   * **of accounts that got a BR for the first time**

   * Any **CSM feedback quotes** (“this saved me X hours,” “I can finally talk value with long‑tail accounts,” etc.)  
9. **Churn Analysis outcome linkage**  
    Have we started tracking anything like:

   * Save‑rate or GRR uplift for **accounts surfaced by Churn AI** vs non‑surfaced, or  
   * Any specific **deal save / improvement story** you’re comfortable name‑checking?  
10. If not, I’ll keep this framed as “systematically explains loss reasons and sets us up to improve GRR,” not “already increased GRR by X points.”

---

### **3.5. Zapier & enablement**

10. **Zapier admin snapshot**  
     Can you get (or do you already have):

    * Total \# of active zaps  
    * Monthly **run volume**  
    * Breakdown by **team/department**, or at least example high‑volume zaps  
11. This lets us turn “50+ workflows” into “Xk runs/month with concrete examples.”

12. **Post‑Bootcamp outcomes**  
     Any short list of “**zaps built as a direct result of the Bootcamp**” (or the Innovation Showcase) would give us a tight story: “we trained people → they shipped automations that do X/Y.”

---

### **3.6. Qualitative positioning & what *not* to include**

12. **RKO / reputational anecdotes**  
     You mentioned that at RKO it was “pretty unanimous” that people love the work Sam Adams is doing, but “we just need to move faster.” Do you want:

    * A discreet, high‑level reference to this (“Feedback from RKO: strong enthusiasm, capacity constraints”), or  
    * To keep that as context for you only and out of the exec‑facing artifact?  
13. **Risk appetite**  
     Are you comfortable including **scenario‑based ROI numbers** (“if we roll Digital BR to \~1,000 accounts, model suggests 2–3 pts of GRR \+ $1.5M expansion pipeline”) clearly labeled as modeled, or do you want **only realized numbers**?

---

## **4\. How I propose to proceed once you reply**

After your answers and any data files/exports:

1. **Tighten metrics & attributions**

   * Integrate updated Glean / UnifyApps / Zapier / CS numbers.  
   * Cleanly separate **“realized impact” vs “targets / modeled opportunity”** on the one‑pager.  
2. **Draft the one‑page dashboard**

   * Build the actual one‑pager content (headlines, tiles, metrics, quotes) in concise exec language.  
   * Ensure everything fits in a **single screen / slide** without feeling crowded.  
3. **Provide a narrative “speaker notes” version**

   * Alongside the one‑pager, I’ll give you a **short narrative script** you can use when presenting to Nitin / Alessio / E‑team — focusing on the orchestrator story and 3–4 proof‑points.

If you share:

* A Glean usage export  
* Any UnifyApps usage screenshots Amanda/Sam have  
* A Zapier admin snapshot  
* Any CS UAT metrics for Digital BR / One‑Pagers

…I can ingest those and return a very sharp, exec‑ready one‑pager on the next iteration.

