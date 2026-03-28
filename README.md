# Report Tiering Framework

**A governance standard for enterprise dashboard quality, ownership, and operational support.**

---

## The Problem This Solves

Most analytics organizations have the same unspoken problem: every dashboard gets treated equally, regardless of who looks at it, what decisions it drives, or how much damage a data error causes.

You know what happens next. The executive dashboard breaks on a Friday afternoon and nobody has an SLA to fix it. Self-service reports get over-engineered with pipelines they don't need. Analysts spend more time firefighting data trust issues than doing actual analysis. Leadership stops trusting the numbers, not because the data is wrong, but because there's no visible system making sure it's right.

A tiering framework fixes this by matching the investment level to the business impact. It answers a simple question: *"What level of quality should this dashboard have, and who's responsible when it breaks?"*

---

## How to Use This Framework

This document is meant to be a starting point, not a rigid spec.

**If you're a director or VP** evaluating whether your org needs this: start with [The Problem This Solves](#the-problem-this-solves) and [Why Tiering Works](#why-tiering-works). The taxonomy and tier definitions will tell you whether this maps to your pain points.

**If you're an analytics lead** who's going to implement this: the [Dashboard Types](#dashboard-types), [Tier Definitions](#tier-definitions--standards), and [Adoption Playbook](#adoption-playbook) sections are your working reference. Fork this document and customize the standards for your tooling and team structure.

---

## Dashboard Types

Before assigning tiers, establish a shared vocabulary for what kinds of dashboards your organization builds. Most enterprise dashboards fall into five categories:

| Type | Business Outcome | Typical Audience | Key Attributes |
|:-----|:-----------------|:-----------------|:---------------|
| **Strategic** | Measure business health against targeted KPIs. Drive long-term decisions. | Senior leadership (Dir+) | High-level metrics · Highly aggregated · Limited filtering · Guided, curated experience |
| **Operational** | Track day-to-day performance of a product or business area. | Senior & mid management (Mgr+) | Product-level metrics · Moderate aggregation · Subject-matter filtering · Multiple dimensions for slicing |
| **Tactical** | Track progress toward short-term goals and departmental initiatives. Bridge strategy and execution. | Mid management & analysts | Subject-matter metrics · Detailed but scoped data · Highly interactive filtering · Performance vs. targets |
| **Analytical** | Dig into historical and current data to find trends, patterns, and predictive insights. | Analysts & data scientists | Deep, detailed datasets · Heavy interactivity · Multiple filters and segmentation options · Drill-down capabilities |
| **Transactional** | Manage day-to-day operational activities at the record level. Typically in-app reporting within systems of record (e.g., ServiceNow, Workday, ERP platforms). May feed ML models. | Varies (often operations teams) | Row-level detail · Minimal interaction · Near real-time or real-time refresh · Built into the source system |

**Why this taxonomy matters:** Without it, the word "dashboard" means something different to every stakeholder. A VP asking for a "dashboard" expects a strategic view. An analyst building a "dashboard" is thinking analytical. These mismatched expectations are where trust erodes.

---

## Tier Definitions & Standards

Three tiers. That's it. The simplicity is on purpose, and it's why this framework actually gets adopted.

The logic: **Tier 0** is earned. You only qualify if your dashboard meets the requirements for mission-critical reporting. **Tier 2** is reserved for in-app, system-of-record reporting artifacts, the dashboards and reports built into platforms like ServiceNow, Workday, or your ERP system. **Tier 1 is everything else.** It's the catch-all, and that's by design. No edge cases, no sub-tiers, no one arguing about whether they're a 1a or a 1b.

Leaders can understand it in two minutes. Teams can self-classify without a committee. That's the whole point.

### Tier Overview

| | Tier 0: Mission Critical | Tier 1: Standard (Catch-All) | Tier 2: In-App / System of Record |
|:---|:---|:---|:---|
| **Dashboard Types** | Strategic, Operational | Strategic, Operational, Analytical, Tactical | Transactional |
| **Core Criteria** | Executive-facing. Measures performance against established, "golden" KPIs. Benchmarking against targets/forecast strongly recommended. Must meet all Tier 0 standards below or it defaults to Tier 1. | Everything that isn't Tier 0 or Tier 2. Any dashboard format. Benchmarking recommended but not required. | In-app reporting artifacts within systems of record (ServiceNow, Workday, ERP, ITSM, etc.). Tabular, row-level detail. Expected to be real-time or near real-time. |
| **Who It's For** | C-suite, SVPs, VPs making resource allocation and strategy decisions | Managers, analysts, and cross-functional teams running day-to-day operations | Operations teams managing transactional workflows within the source system |

### Detailed Standards by Tier

| Standard | Tier 0 | Tier 1 | Tier 2 |
|:---------|:-------|:-------|:-------|
| **Data Pipeline** | Must be built on centralized, data-engineering-owned tables with established SLAs | Can use DE-owned tables or analyst-owned pipelines (spreadsheets, ad hoc sources acceptable) | Owned by the system-of-record team |
| **CI/CD (Continuous Integration / Continuous Deployment)** | Strongly recommended | Recommended but not required | N/A |
| **Dashboard Ownership** | Owned by a centralized analytics or BI team | Developed by centralized teams or individual analysts | System-owning team |
| **Metric Ownership** | Analysts or centralized data team with formal definitions | Analysts | N/A |
| **SLA** | Set individually per dashboard | Analyst owner can set a refresh schedule (no formal SLA) | Real-time or near real-time (system-level SLA) |
| **Operational Support** | Integrated into organizational incident management process. On-call support required. | Report owner notified via team channels (Slack, Jira, etc.). Pipeline bugs follow standard data triage. | Integrated into organizational incident management. On-call support required. |
| **Data Quality Monitoring** | Data quality checks owned by centralized data engineering | Quality monitoring on DE-owned pipelines only | N/A |
| **BI Platform** | Enterprise-grade platforms with governance controls | Enterprise, self-service, or lightweight platforms | In-app, custom-built applications |
| **Dashboard Template** | Must follow standardized templates with documented look-and-feel guidelines | Recommended to follow standardized templates, but not required | N/A |
| **Dashboard Documentation** | Requires both a user guide and technical documentation | User guide or technical documentation recommended, but not required | Requires a user guide or technical documentation |
| **Metric Documentation** | All metrics documented with ownership, approved definitions, and published to a central data catalog | Metrics documented with ownership and approved definitions recommended, but not required | N/A |
| **Business Logic** | Computed upstream from the BI layer (preferably in version-controlled data models) | Computing business logic upstream from the BI layer is recommended, but not required | N/A |

---

## Why Tiering Works

### The Self-Enforcing Quality Mechanism

The most important design decision in this framework is what happens when a team *wants* Tier 0 designation but doesn't want to meet the requirements.

**They don't get it.** They default to Tier 1.

Quality becomes self-enforcing without a governance police force. Teams that want the prestige and operational support of Tier 0 (and they do, because it means executive visibility and incident management coverage) have to earn it by meeting the standard. No exceptions, no negotiations.

You end up with a pull model. You're not chasing teams to comply. They come to you asking what they need to do to qualify.

### What Changes When You Implement This

**Before tiering:**
- Every broken dashboard is an emergency (because there's no way to prioritize)
- Analysts spend cycles supporting reports that nobody uses at the exec level
- Data engineering can't allocate resources because every request is "urgent"
- No shared vocabulary for what "production-quality" means

**After tiering:**
- Incident response maps to business impact (Tier 0 pages on-call; Tier 1 sends a Slack message)
- Resource allocation becomes rational. Tier 0 gets DE-owned pipelines; Tier 1 can use analyst tables.
- Teams self-select their tier based on what they're willing to invest
- Quality expectations are written down, not assumed

---

## Adoption Playbook

Building the framework is the easy part. Getting cross-functional sign-off is where most governance efforts die. Here's what actually works:

### 1. Start with What Already Exists

Don't invent from scratch. If your best dashboards already follow implicit standards (reliable pipelines, consistent design, documented metrics) then codify what's already working. The framework should describe your best practices, not aspirational ones nobody follows.

### 2. Get Buy-In Through Inclusion, Not Mandate

Present the draft to analytics leaders individually, not in a large group. Large meetings create politics. One-on-one conversations create co-authors. When someone suggests a change and you incorporate it, they now own part of the framework. Repeat across business groups until you have broad sign-off.

**Target: sign-off from analytics leaders across every major business unit.** This prevents the framework from being dismissed as "one team's opinion."

### 3. Anchor to Templates

Standards written in the abstract are easy to ignore. A working template is hard to argue with. Build at least two reference templates:

- **Strategic Dashboard Template** for Tier 0/1 strategic views
- **Operational Dashboard Template** for Tier 0/1 operational views

Link these directly in the framework documentation. When someone asks "what does Tier 0 look like?" you point them to a working example, not a spec document.

### 4. Make It Official

If your organization has a formal architecture decision process (ADR, RFC, ITAD, or equivalent), route the framework through it. A "best practice" that lives in someone's wiki is optional. A "standard" that's been ratified gets referenced in onboarding, included in reviews, and cited when teams push back.

### 5. Let It Breathe

The framework should be a living document. Your BI platform stack will change. New tools will show up. Teams will restructure. Update the tier definitions when that happens. Version it. Treat it like a product, not a policy memo.

---

## Customization Guide

This framework is meant to be forked. Here's what usually needs to change per organization:

| Element | What to Customize |
|:--------|:------------------|
| **Dashboard Types** | Add or merge types to match your portfolio. Some orgs don't distinguish Tactical from Analytical. Others add "Embedded" for customer-facing analytics. |
| **Tier Count** | Three tiers is the sweet spot for most orgs. Resist the urge to add more. Leaders can understand this in under two minutes, and that matters more than covering every edge case. Smaller teams may only need two (Critical / Standard). Adding a Tier 3 for ad hoc or sandbox reports is possible but rarely necessary since Tier 1 already serves as the catch-all. |
| **BI Platform Row** | Replace with your actual platform stack. The principle holds regardless of tooling: higher tiers should use platforms with stronger governance controls. |
| **Pipeline Standards** | Map to your actual data infrastructure. "DE-owned tables" might be "dbt models in production" or "Airflow DAGs with monitoring" in your context. |
| **Operational Support** | Map to your incident management tooling (PagerDuty, Opsgenie, ServiceNow, etc.) and escalation paths. |
| **Metric Documentation** | Reference your data catalog or governance tool (Atlan, Alation, DataHub, Collibra, etc.). |

---

## License

This framework is released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). You are free to share and adapt it for any purpose with attribution.

---

*Created by Bronson Elliott · [LinkedIn](https://www.linkedin.com/in/bronsonelliott) · [Learning Out Loud on Substack](https://bronsonelliott.substack.com)*
