# AI Operations Team Deep Dive

This document summarizes **who is in Docebo’s AI Operations team**, **what we do**, **what we work on**, and **how we operate**, based on recent strategy and steering conversations with **Nitin Chopra** and **Marco Bettineschi**, plus ongoing working sessions across AI, Salesforce, and RevOps.

---

## 1\. Who is in the AI Operations team

### Core team

- **Sam Irizarry – Director, AI Operations & Business Technology**  
    
  - Leads the combined **AI Operations \+ Salesforce** organization (8+ people) after the role change agreed with Nitin and Marco in Nov 2025\.  
  - Accountable for:  
    - AI strategy, governance, and tooling stack (Glean, Unify Apps, Claude, Zapier, etc.).  
    - Salesforce platform direction and major GTM initiatives (Sales Stages, Revenue Cloud evaluation, 365 Talents integration, CPQ/RevCloud, etc.).  
    - Executive alignment and steering forums (SF & AI Monthly Steering Committee; CRO presentations; software committee work).  
  - Acts as the primary bridge between **OPS–IT**, **RevOps**, **Sales leadership**, and **Product** on AI-enabled projects.


- **Samuel Adams – AI Operations Lead (IC)**  
    
  - Day‑to‑day **technical lead** for AI Ops: designs and builds agents, applications, and workflows across **Unify Apps, Glean, Salesforce, Zapier, AWS, and MCPs**.  
  - Owns:  
    - The **AI Ops operating model** (project intake, T‑shirt sizing, communication cadence, lifecycle management) as presented in the SF & AI Steering Committee and CRO presentations.  
    - Complex builds: handoff agents, audience insights dashboards, forecasting and BDR management automations, Prism/skills‑related pilots, etc.  
    - Partner management with Unify Apps and Glean (e.g., Prism private beta, Unify Apps platform evaluation, AWS deployment).


- **Giuseppe Bonanno – AI Engineer / Solution Engineer**  
    
  - Joined recently as the **AI Solution Engineer** to:  
    - Build **simple and medium‑complexity applications and interfaces** (especially in Unify Apps and web stacks like Vercel/Next.js).  
    - Develop **script and skill libraries** (AgentForce scripts, MCPs, prompt “skills” for Claude/Glean) that agents can call.  
    - Help design and implement the **enterprise skills library** and dashboards (e.g., ticket dashboards backed by Postgres \+ MCP, skills‑based agents for OKRs and insights).  
  - Expected to become a core builder and multiplier for AI Ops by end of 2026, in parallel with Sam Adams’ focus on complex agents and orchestration.

### Extended collaborators

While not “in” AI Ops, a few leaders are tightly coupled with the team’s strategy and operating model:

- **Nitin Chopra** – executive sponsor; sets direction, probes team identity and scope, and challenges speed, ROI, and organizational model (central vs. embedded AI).  
- **Marco Bettineschi** – partner for Salesforce and corporate IT; co‑owns many cross‑functional initiatives (Revenue Cloud, 365 Talents, sandbox strategy, staffing and org design).

---

## 2\. What is our mission

Across multiple “AI Operations Charter” and steering meetings, the emerging **mission** for AI Ops is:

**Operate as Docebo’s AI enablement engine – staying on the bleeding edge of AI tools, co‑designing and building high‑impact solutions with business teams, and owning the lifecycle and governance of AI agents and applications that drive revenue growth and efficiency.**

Nitin framed this explicitly as a **three‑pillar model** for AI Ops:

1. **Bleeding‑edge market awareness & opinionated guidance**  
     
   - Track the fast‑moving AI landscape (Claude, Gemini, Glean, Unify Apps, Vibe, MCPs, etc.) and **form strong, informed opinions** about:  
     - Which tools we trust.  
     - Where they fit (and don’t) in Docebo’s ecosystem.  
     - When to pivot based on market shifts.  
   - Translate that into **concrete recommendations** for leadership and teams.

   

2. **Solution consulting & force multiplication**  
     
   - Work directly with teams (Sales, CS, RevOps, Marketing, Finance, etc.) to:  
     - Identify **3–4 high‑value problems** per group.  
     - Co‑design AI‑enabled workflows and applications.  
     - Get them into **production**, not just prototypes.  
   - The model is explicitly **consultative**, not a ticket‑factory: AI Ops helps teams see what is possible, scope, and then either build or coach others to build.

   

3. **AI agent & application lifecycle management**  
     
   - Own the **end‑to‑end lifecycle** for strategic agents and apps:  
     - Intake → design → build → UAT → rollout → monitoring → iteration/deprecation.  
   - Provide **governance** around:  
     - Which agents are “AI Ops approved”.  
     - Quality thresholds, testing, and sign‑off.  
     - Where and how agents are exposed (Salesforce, Slack, Glean, Unify Apps, etc.).

This is deliberately **anchored to business outcomes**, not “cool AI demos”: revenue, churn/retention, cost reduction, and speed of execution are the main lenses used in executive and steering discussions.

---

## 3\. What we work on (key workstreams)

### 3.1 Agents, apps, and workflows

Recent and ongoing builds include:

- **Handoff agents** (AE→PS, BD→AE, CSM handoff)  
    
  - Built on **Unify Apps** with deep integration into Salesforce, Gong, Totango, and shared folders.  
  - Aim: reduce the “reps as business analysts” problem (manual research and note‑taking), improve handoff quality, and tie to **churn mitigation and escalation reduction**.


- **Audience Insights and revenue‑facing agents**  
    
  - Examples like the **Audience Insights Dashboard** that contributed to \~$5M in Skills pipeline, and new cohorts for marketing insights and sales enablement.


- **Salesforce‑embedded agents**  
    
  - Experiments embedding agents directly in **Salesforce UIs** (vs. separate Unify Apps frontends) to reduce context switching – starting with Amanda’s audience insights agent and similar cases.


- **Forecasting and manager‑level automation**  
    
  - Partnering with GTM leaders (e.g., Jonathan Mayer) on:  
    - Automating Python/Jupyter‑based **forecasting** workflows with LLM‑generated narratives and Slack delivery.  
    - A BDR management system (“Granola loop”) that structures manager observation cycles and uses AI to surface performance themes and coaching actions.


- **Customer health, churn, and expansion**  
    
  - Collaboration with Glean on **Prism (private beta)** to build:  
    - Churn and renewal health views.  
    - Upsell/expansion opportunity signals.  
    - REACH‑style customer health scoring that blends Gong, Zendesk, Salesforce, Slack, and usage data.

### 3.2 Skills, knowledge, and search

The Feb 11 AI Ops sync re‑centered the roadmap around **enterprise skills and knowledge**, rather than one‑off apps:

- **Enterprise skills library**  
    
  - Build a set of **core, reusable AI “skills”** (prompt \+ logic packages) such as:  
    - Enterprise Search tuned to Docebo’s stack and values.  
    - Brand‑guidelines skill for marketing.  
    - Skills that chain multiple steps (e.g., “run health report”, “summarize risk drivers”, “draft outreach”).  
  - Goal: users invoke powerful workflows via simple commands, without being expert prompt engineers.


- **Domain hand‑off model**  
    
  - AI Ops builds the **first 4–10 generic skills**, then **transitions ownership** conceptually to domain experts (e.g., brand, CS, product) who obsess over content and accuracy, while AI Ops maintains underlying infrastructure and patterns.

### 3.3 Platform and architecture work

AI Ops also owns or heavily influences **platform‑level decisions** about where AI lives:

- **Unify Apps platform assessment**  
    
  - Six‑month window to decide **what belongs on Unify Apps**, what doesn’t, and what a “world without Unify Apps” looks like, given the \~$370K+ investment and renewal timeline.  
  - Evaluate:  
    - Migration paths (data, automations, apps).  
    - Alternatives (Cloud Code, Base44 AI, custom stacks on AWS/GCP).  
    - Value vs. cost vs. capacity trade‑offs.


- **Deployment platforms and boundaries**  
    
  - Active debates (and upcoming security sessions) around:  
    - When to use **Supabase / Vercel** vs. internal **AWS/Google Cloud**.  
    - What tools belong under **AI Ops** vs. general infrastructure (e.g., are Supabase/Vercel “AI tools” or just platforms?).


- **AWS deployment and security**  
    
  - Working with security to finalize the permission set for Unify Apps’ AWS deployment so future apps don’t need repeated deep‑dive security reviews.

---

## 4\. How we operate

### 4.1 Intake, sizing, and capacity

From the Jan 14 SF & AI Steering Committee and AI Ops charter discussions, the team is standardizing around:

- **Structured intake**  
    
  - Ops/RevOps and business leads are the **front door** for AI work.  
  - Requests must include:  
    - Business problem and impact hypothesis.  
    - Data sources involved.  
    - Target users and workflows.  
    - Acceptance criteria / sign‑off owners.


- **T‑shirt sizing**  
    
  - AI Ops uses **Small / Medium / Large / XL** with indicative timelines (e.g., \~4–5 weeks, 6–7 weeks, 8–9 weeks, 10+ weeks, depending on complexity and data readiness).  
  - Helps executives compare “one big thing vs. several small things” when prioritizing.


- **Capacity transparency**  
    
  - Small core team (effectively 1–2 full‑time builders \+ contractors), so:  
    - Major initiatives (e.g., handoff agents, Prism pilots, skills library) are explicitly carved into **quarterly capacity** (4–5 use cases per quarter in early model).  
    - Weekly/Monthly steering meetings revisit priorities based on in‑flight load.

### 4.2 Governance, lifecycle, and quality

To avoid “polished turds” and tool sprawl, governance patterns include:

- **Agent lifecycle gates**  
    
  - Clear stages: **discovery → design → build → UAT → pilot → production → review/deprecation.**  
  - Named **sign‑off owners** for UAT and production, with explicit quality thresholds (e.g., acceptable accuracy bands, data coverage) before go‑live.


- **AI Hub and certification**  
    
  - A **Glean‑based AI Hub** catalogs approved agents and tools with:  
    - What they do.  
    - Who owns them.  
    - Data they touch.  
    - Who can use them and how.  
  - Glean cohort program and internal review determine which agents get “AI Ops approved” status.


- **Tool governance and sprawl control**  
    
  - Steering conversations highlighted paralysis from too many tools (Glean agents, Unify Apps, Zapier, Gemini, etc.) and inconsistent answers.  
  - AI Ops is expected to:  
    - Define **which tools are “core” vs. experimental**.  
    - Incrementally **consolidate** (e.g., where Granola can replace other meeting tools, or where Prism replaces ad‑hoc analysis).

### 4.3 Forums and cadence

Key operating forums:

- **SF & AI Monthly Steering Committee**  
    
  - Attendees: Sam, Nitin, Marco, RevOps, Sales, Samuel Adams, and others.  
  - Purpose: portfolio view of **Salesforce \+ AI** work, trade‑off decisions, and process alignment (e.g., intake discipline, embedded vs. centralized AI, deployment choices).


- **Weekly Friday ticket/roadmap reviews**  
    
  - Look at in‑flight work (Sales Stages, agents, 365, etc.) and new tickets against priorities.  
  - Decide whether new requests **enter the roadmap** or are redirected.


- **AI Ops team syncs**  
    
  - Focused on **strategy and backlog** for Sam, Samuel, and Giuseppe: Unify Apps assessment, skills library, deployment boundaries, AI FinOps/cost tracking, etc.

---

## 5\. Themes from AI strategy conversations with Nitin & Marco

Across the AI Ops Charter meetings and steering sessions, a few recurring strategic tensions show up:

1. **Speed vs. quality**  
     
   - Nitin pushes hard on speed – e.g., Unify Apps work taking 3–4 months when business expects 2‑week cycles.  
   - Giuseppe and Sam highlight the cost of shipping unvalidated agents that erode trust; they argue for time to validate, train, and measure.  
   - Outcome: multi‑tool strategy (Zapier/Glean for **fast** experiments; Unify Apps for **heavyweight** systems) plus clearer quality gates.

   

2. **Centralized vs. embedded AI**  
     
   - Question: should AI Ops remain a **central team**, or should AI specialists be embedded in each function (Marketing, CS, RevOps, etc.)?  
   - Megan and Nitin have both raised matrix‑org pros/cons; current direction keeps **AI Ops central** but expects strong partnerships and “champions” in each function.

   

3. **Where AI lives (platform choices)**  
     
   - Debates around:  
     - **Salesforce \+ Slack** as primary surfaces vs. separate Unify Apps UIs.  
     - Supabase/Vercel vs. internal clouds for app hosting.  
   - Default direction: meet users in **Salesforce and Slack** where possible, keeping Unify Apps/others as back‑end orchestration when needed.

   

4. **Measurement and ROI**  
     
   - Recognized difficulty of proving ROI at the bleeding edge (you often **must implement** before you can quantify benefits).  
   - Still, there’s strong pressure to:  
     - Tie work to specific KPIs (pipeline, churn, time‑saved).  
     - Avoid scattered, one‑off experiments not connected to top‑level company objectives.

---

## 6\. Short summary / elevator pitch

- **Team:** Small, senior core – Sam (Director), Samuel (technical lead), Giuseppe (solution engineer) – extended by contractors and platform partners.  
- **Mission:** Be Docebo’s AI enablement engine – on the bleeding edge, co‑designing high‑impact solutions with the business, and owning the lifecycle and governance of strategic AI agents and applications.  
- **Work:** Handoff agents, customer health and expansion insights, skills/knowledge infrastructure, forecasting and manager‑level automation, and platform decisions (Unify Apps, Prism, AWS/Supabase/Vercel/Salesforce).  
- **Operating model:** Structured intake and sizing, monthly steering, weekly ticket/roadmap reviews, strong governance over tools and agents, and a constant balancing act between speed and quality in a rapidly shifting AI market.

*Written with Glean Assistant*  
