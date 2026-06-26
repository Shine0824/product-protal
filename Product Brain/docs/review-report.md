# Product Brain — Review Report

**Date:** 2026-06-22
**Reviewed by:** Claude Code
**Source documents:** `1. vision.html`, `2. user.html`, `3. journey.html`, `4. architecture.html`, `5. decision.html`
**Additional context:** Prototype HTML pages, `app-flow-preview.html`, `猪实验管理系统设计.md`

---

## Executive Summary

The Product Brain defines **Experiment R&D Platform** (实验研发平台) — a dual-platform (Web + App) swine experiment management system for PhD researchers, farm managers, and technicians. The vision and role analysis are well-structured. However, significant gaps exist: the PhD/CEO persona — the primary decision-maker — has no documented user journeys; the architecture document is far sparser than what the prototype already implements; and the "智能" (intelligent) positioning lacks concrete feature definition. Below are findings across 7 evaluation areas, classified by severity.

---

## 1. Product Vision Alignment

### Finding 1.1 — "智能" positioning lacks concrete definition (P1)

The vision describes the platform as an "智能养殖实验平台" (intelligent breeding experiment platform). However, the documented capabilities — data recording, batch import, threshold-based alerts, report generation — describe a digital data management platform, not an intelligent one. The product promises "intelligence" but no document specifies what that means in practice.

**What to clarify:** Is the intelligence in automated data summaries? Predictive alerts? Smart data validation during entry? Without a concrete definition of what "智能" delivers, the vision statement over-promises relative to documented features.

### Finding 1.2 — Core value per role is well-articulated (P2)

The vision maps value clearly to each user tier:
- **CEO**: experiment data as assets → replicable → commercialized
- **PhD**: progress oversight, data accumulation, conclusions for commercialization
- **Farm manager**: daily data review and pig experiment status
- **Technician**: electronic multi-dimensional data recording

This is logically sound and provides a solid foundation for feature prioritization.

### Finding 1.3 — "Won't do" boundary needs timeline context (P2)

Excluding advanced statistics (significance testing) is a reasonable MVP scope decision. However, for a platform targeting PhD researchers, this is a foundational need. The exclusion should note when this boundary might be revisited, or what alternative workflow (e.g., data export for external analysis) bridges the gap.

---

## 2. User Journey Alignment

### Finding 2.1 — PhD/CEO journeys are completely missing (P0)

The journey document (`3. journey.html`) covers four flows:

1. 日常数据手工记录 (manual daily data entry)
2. 日常数据自动同步 (auto data sync)
3. 日常数据批量导入 (batch data import)
4. 异常数据推送 (anomaly data push)

All four are oriented toward the **technician/farm-manager** personas doing data entry and review. The PhD/CEO persona — whose core needs are experiment group comparison, conclusion review, cross-experiment trend analysis, and progress oversight — has **zero documented user journeys**. This is the persona most likely to drive platform adoption and purchasing decisions.

### Finding 2.2 — Experiment lifecycle flows are missing (P0)

The `猪实验管理系统设计.md` and prototype define a complete lifecycle:

```
Create experiment → Grouping → Stage execution → Stage review/approval
→ Stage comparison → Stage merge → ... → Final merge → Close → Report
```

The journey document captures only the "daily recording" middle step. Missing journeys:
- Experiment creation & configuration (博士 creates experiment, defines stages)
- Experiment grouping (场长 uploads group assignment of pigs to treatment/control groups)
- Stage-end submission & approval (场长 submits, 博士 approves or requests revision)
- Stage comparison & merge analysis (博士 reviews cross-stage data)
- Final conclusion & report generation (博士 generates and exports experiment report)
- Cross-experiment comparison (博士 compares results across experiments)

### Finding 2.3 — Journey format has redundancy (P1)

"日常数据手工记录" and "日常数据自动同步" are nearly identical flows (select experiment → select record type → enter or review data). They could be consolidated into a single flow with branching for manual vs. auto-sync entry modes, reducing duplication and maintenance burden.

### Finding 2.4 — No error or exception paths (P1)

None of the journeys include failure states:
- What happens when batch import validation fails?
- What if data sync from an external feed is incomplete or corrupted?
- What if a stage cannot be submitted because mandatory data is missing?
- What if approval is rejected — how does the farm manager see and address the feedback?

---

## 3. Information Architecture

### Finding 3.1 — Architecture document significantly lags behind prototype (P1)

`4. architecture.html` defines a minimal flat structure:

```
Experiment R&D Platform (Web)
├── Overview (Experiments Status, Experiments Alerts)
└── Analysis (Analysis Report)

Experiment R&D Platform (APP)
├── Experiment Management
└── Workbench (Data Entry, Data Analysis, Data Alert)
```

The actual Web prototype (`00-Experiment_overview.html`) reveals a much richer 3-level hierarchy:

```
实验研发
├── 知识库
├── 项目管理
├── 实验场
├── 猪实验数据
│   ├── 实验概览 (experiment list table, stat cards, anomaly alerts)
│   └── 报表分析 (summary cards, charts, report tables, 8 report types)
└── 家禽实验数据
```

The architecture document should be updated to reflect what has already been built.

### Finding 3.2 — Web vs. App capability boundaries are unclear (P1)

The architecture lists Web and App modules separately but doesn't define:
- Which operations are **exclusive** to each platform
- Which data is **shared** between platforms
- Whether App modules are a **subset** of Web or serve different use cases
- Any **offline** capability for the App (farm environments may have poor connectivity)

The design spec (`猪实验管理系统设计.md`) does include a partial Web/App responsibility table, but this has not been incorporated into the Product Brain architecture.

### Finding 3.3 — Cross-cutting concerns are omitted (P1)

The architecture doesn't address:
- User authentication & role-based access control (despite 3+ user roles)
- Notification system (push notifications, in-app alerts)
- Data import/export pipeline (template download, validation, error reporting)
- Audit logging (who changed what and when — critical for experiment integrity)

The design spec discusses all of these; the architecture document should incorporate them.

### Finding 3.4 — Stage state machine is well-designed (P2)

The design spec defines a clear stage state machine: 待开始 → 进行中 → 待审核 → 已结束 → 已归档, with defined transitions. This is a strong architectural decision that should be promoted into the Product Brain architecture document.

---

## 4. Dashboard Design

### Finding 4.1 — Dashboard exists in prototype but not in Product Brain docs (P0)

Decision-001 correctly states "首页采用实验概览，而非具体单一实验记录" with sound rationale: management needs to see all experiments at a glance, and data entry is accessible through drill-down.

The Web prototype implements this well:
- **4 stat cards**: experiment count, avg record completeness, anomaly records, today's new records
- **Experiment list table**: code, building/unit, growth stage, location, phases, current progress, status, anomaly level, record completeness (with progress bar), report access dropdown
- **Anomaly alert table**: time, experiment, pen, anomaly type, description, action link

However, the Product Brain documents contain **zero dashboard specification** — no KPI definitions, no layout decisions, no design rationale. The dashboard is the first thing stakeholders see; its design should be a documented product decision, not just code.

### Finding 4.2 — Role-based dashboard views are undefined (P1)

The vision defines 4 user roles with distinct concerns, but there is no discussion of whether:
- The CEO sees a different top-level view than a PhD researcher
- Farm managers see only their assigned farms/experiments
- Technicians land directly on the data entry screen instead of the overview

### Finding 4.3 — Record completeness metric lacks documented logic (P2)

The prototype shows "记录完整度" as a percentage, which is a strong data-quality KPI. However, its calculation logic (which fields count toward completeness? is it per-day or per-stage?) is not documented.

---

## 5. Intelligent Features Design

### Finding 5.1 — Platform intelligence is referenced but not specified (P1)

The vision positions the platform as "智能" (intelligent), and the architecture includes "Data Alert" and "Analysis Report" modules. The intelligent promise appears to be delivered through:

- **Data alerts**: threshold-based anomaly detection (e.g., sudden mortality increase, abnormal feed consumption)
- **Automated reports**: pre-built report templates (daily, stage, experiment summary, death/cull, diarrhea, medicine/vaccine, environment, weight)
- **Experiment analysis**: stage comparison, stage merging, cross-stage trends

However, none of these are documented as explicit "intelligent" capabilities with defined behavior. The alert logic (thresholds, rules, severity levels) is not specified. The report templates are referenced in the prototype dropdown but their content and generation logic are not described.

### Finding 5.2 — Anomaly detection is rule-based, logic is undocumented (P1)

The journey describes "异常数据推送" as: discover issue → view reports → optionally add notes → track improvement. This is a human review workflow triggered by rules. The prototype shows an "异常等级" (anomaly level) column and an alert table with types and descriptions. However:
- What rules trigger each anomaly type?
- What defines severity levels?
- Is there a learning mechanism (e.g., adjusting thresholds based on historical patterns)?

### Finding 5.3 — Report automation is the strongest intelligent feature but under-documented (P2)

The prototype's report dropdown lists 8 report types (daily, stage, experiment summary, death/cull detail, diarrhea detail, medicine/vaccine detail, environment detail, weight detail). This is a substantial automation capability — turning raw records into formatted reports — but its design is not discussed in any Product Brain document.

---

## 6. Navigation Design

### Finding 6.1 — Web navigation is implemented but not documented (P1)

The Web prototype has a well-structured sidebar navigation with breadcrumbs (实验研发 › 猪实验数据 › 实验概览). This structure — including the presence of "家禽实验数据" (poultry experiment data, suggesting future scope) — should be documented with rationale in the architecture or a dedicated navigation spec.

### Finding 6.2 — App navigation model conflicts with architecture doc (P1)

The `app-flow-preview.html` shows a linear mobile flow: 首页 → 实验详情 → 日常记录 → 阶段结束 → 阶段确认 → 实验结束 → 报表. The Product Brain architecture lists different App modules: Experiment Management, Workbench (Data Entry, Analysis, Alert). These two models don't reconcile — the flow preview suggests a task-oriented sequential app; the architecture suggests a module-based app. Which is correct?

### Finding 6.3 — Decision-001 is sound but only covers the homepage (P2)

The decision to use experiment overview as the landing page is well-reasoned. However, it's the only navigation decision documented. Decisions about secondary navigation, mobile navigation structure, and drill-down paths are absent.

---

## 7. Business Value Communication

### Finding 7.1 — Value is described qualitatively, lacks quantification (P1)

The vision describes value in prose but provides no:
- Estimated time savings vs. current Excel workflow
- Data quality improvement targets
- Experiment throughput increase potential
- ROI justification for platform investment

For a demo to business stakeholders (CEO, head of R&D), quantified value would be expected.

### Finding 7.2 — Data asset value chain is mentioned but not explained (P2)

The vision mentions "数据资产化 → 可复制推广 → 商业化" as the CEO-level value chain. This is a compelling narrative but is stated in one sentence without elaboration on how the platform enables each step.

### Finding 7.3 — No competitive context (P2)

The current workflow (Excel-based manual process) is the implicit baseline, but this is not made explicit. There is no comparison to alternatives (generic LIMS, other ag-tech platforms, or doing nothing) that would help justify the platform investment.

---

## Summary of Findings

### P0 — Must Fix Before Demo

| # | Finding | Area |
|---|---------|------|
| 2.1 | PhD/CEO user journeys are completely missing | Journey |
| 2.2 | Experiment lifecycle flows (create, group, review, close, report) are missing | Journey |
| 4.1 | Dashboard specification is only in prototype code, not in product docs | Dashboard |

### P1 — Should Improve

| # | Finding | Area |
|---|---------|------|
| 1.1 | "智能" positioning lacks concrete feature definition | Vision |
| 3.1 | Architecture doc significantly lags behind prototype implementation | Architecture |
| 3.2 | Web vs. App capability boundaries are not defined | Architecture |
| 3.3 | Cross-cutting concerns (RBAC, notifications, audit, import/export) not in architecture | Architecture |
| 5.1 | Platform intelligence is referenced but not specified | Intelligent Features |
| 5.2 | Anomaly detection rules and severity logic are undocumented | Intelligent Features |
| 6.1 | Web navigation hierarchy exists in code but not in docs | Navigation |
| 6.2 | App navigation model conflicts between architecture doc and flow preview | Navigation |
| 2.3 | Duplicate journey flows could be consolidated | Journey |
| 2.4 | No error or exception paths in any user journey | Journey |
| 7.1 | Business value lacks quantification; no ROI or efficiency metrics | Business Value |

### P2 — Future Enhancement

| # | Finding | Area |
|---|---------|------|
| 1.2 | Core value per role is well-articulated (no action needed) | Vision |
| 1.3 | "Won't do" boundary should include timeline for revisiting advanced stats | Vision |
| 3.4 | Stage state machine is well-designed; should be in architecture doc | Architecture |
| 4.3 | Record completeness metric needs documented calculation logic | Dashboard |
| 5.3 | Report automation is the strongest intelligent feature but under-documented | Intelligent Features |
| 6.3 | Decision-001 is sound but only covers homepage navigation | Navigation |
| 7.2 | Data asset value chain needs elaboration for CEO pitch | Business Value |
| 7.3 | Competitive context (Excel baseline vs. platform) should be explicit | Business Value |

---

## Recommended Actions Before Demo

1. **Document the PhD journey end-to-end** — this is the primary user persona. The flow should cover: login → experiment overview → drill into specific experiment → review stage comparison → consume reports → export/share conclusions. This is the journey that sells the platform.

2. **Document the experiment lifecycle** — incorporate the stage state machine and lifecycle flows from `猪实验管理系统设计.md` into the Product Brain. The prototype already implements this flow; the docs need to catch up.

3. **Promote the dashboard design into product documentation** — capture the KPI cards, experiment list columns, alert table design, and the rationale behind each as explicit product decisions. The prototype is done; the Product Brain should explain why it looks the way it does.

4. **Define what "智能" means concretely** — specify which features deliver the "intelligent" promise (automated reports? alerts? data validation?) and document their behavior so the positioning matches the product.

5. **Update the architecture document** to reflect the actual prototype structure — sidebar hierarchy, page inventory, report types, and cross-cutting services. The code is ahead of the docs; close the gap.
