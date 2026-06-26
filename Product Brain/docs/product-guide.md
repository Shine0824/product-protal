# Experiment R&D Platform — Product Guide / 实验研发平台 — 产品指南

**Version / 版本:** 1.0
**Date / 日期:** 2026-06-22
**Status / 状态:** Prototype Phase / 原型阶段

---

## 1. Product Overview / 产品概览

### 1.1 What Is It? / 产品简介

**EN:** Experiment R&D Platform (实验研发平台) is a dual-platform (Web + App) intelligent experiment management system purpose-built for livestock enterprises. It replaces the current Excel-based manual workflow with standardized digital data collection, automated analysis, and end-to-end experiment lifecycle management.

**ZH:** 实验研发平台是一个双端（Web + App）智能实验管理系统，专为养殖企业打造。它以标准化的数字化数据采集、自动化分析和全流程实验生命周期管理，取代了当前基于 Excel 的手工作业方式。

### 1.2 Product Positioning / 产品定位

**EN:** An intelligent breeding experiment platform for livestock enterprises. It enables PhD-level researchers, farm managers, and on-site technicians to record experimental data, generate data alerts, produce data summaries for each experiment stage, and perform experimental group analysis.

**ZH:** 面向养殖企业的智能养殖实验平台，帮助实验类博士、场长和场内技术员记录实验数据、生成数据预警、产出各实验环节的数据总结，并进行实验组分析。

### 1.3 Platform at a Glance / 平台概览

| Dimension / 维度 | Web Platform / Web端 | App / 移动端 |
|-----------|-------------|-----|
| Primary users / 主要用户 | PhD researchers, CEO / 博士、CEO | Farm managers, technicians / 场长、技术员 |
| Core scenarios / 核心场景 | Experiment oversight, analysis, report generation / 实验监管、分析、报表生成 | Daily data recording, alerts review / 日常数据记录、预警查看 |
| Device context / 设备环境 | Desktop, large screen / 桌面端、大屏 | Mobile, in-farm operation / 移动端、场内操作 |
| Key advantage / 核心优势 | Rich data analysis, multi-experiment comparison / 丰富的数据分析、多实验对比 | Portability, on-site convenience / 便携性、现场便捷 |

### 1.4 Core Principles / 核心原则

**EN:**
- **Standardization over flexibility** — structured forms with validation, not free-form Excel
- **Overview-first navigation** — management sees all experiments at a glance; data entry is drill-down
- **Dual-platform, role-split** — App for recording (场长/技术员), Web for managing/analyzing (博士/CEO)
- **Not a standalone data entry tool** — the platform integrates recording into the full experiment workflow, not as an isolated utility

**ZH:**
- **标准化优于灵活性** — 结构化的带校验表单，而非自由格式的 Excel
- **概览优先的导航** — 管理层一览所有实验；数据录入通过下钻进入
- **双端分工、角色分离** — App 负责记录（场长/技术员），Web 负责管理/分析（博士/CEO）
- **不做单独的录入系统** — 平台将数据录入融入完整实验流程，而非孤立工具

---

## 2. Business Challenges / 业务挑战

### 2.1 Current State: Excel-Driven Workflow / 现状：Excel 驱动的工作流

**EN:** Livestock experiment management today relies on Excel files manually passed between PhD researchers (designing experiments remotely) and farm staff (executing and recording on-site). This creates five core problems:

**ZH:** 当前养殖实验管理依赖 Excel 文件在博士（远程设计实验）和现场人员（执行并记录）之间手工流转，由此产生五个核心痛点：

| # | Challenge / 挑战 | Impact / 影响 |
|---|-----------|--------|
| 1 | **Data collection is not standardized / 数据采集不规范** | No unified templates; fields filled arbitrarily; same indicator recorded in incompatible formats across farms / 缺乏统一模板，字段填写随意，同一指标在不同场区存在多种记录方式 |
| 2 | **Data is not real-time / 数据实时性差** | Excel files circulate offline; PhD researchers cannot access latest data promptly, delaying decisions / Excel 文件离线流转，博士无法及时获取最新数据，影响决策效率 |
| 3 | **Data analysis is inefficient / 数据分析低效** | Manual Excel aggregation is time-consuming and error-prone; no rapid report generation or visualization / 依赖手工汇总，分析耗时且易出错，无法快速生成报表和可视化 |
| 4 | **Data traceability is difficult / 数据溯源困难** | Version chaos; modification history is untracked; root cause analysis is near-impossible / 版本混乱，修改记录难以追踪，问题排查时无法快速定位原因 |
| 5 | **Process collaboration is fragmented / 流程协同不畅** | Task assignment and progress tracking rely on offline communication (phone/WeChat); no unified task management or status sync / 任务分配和进度跟踪依赖线下沟通（电话/微信），缺乏统一的任务管理和状态同步 |

### 2.2 Validation Logic / 验证逻辑

**EN:** Each challenge maps to a verifiable outcome:

**ZH:** 每个挑战对应一个可验证的结果：

| Challenge / 挑战 | If... / 如果... | Then... / 那么... |
|-----------|-------|---------|
| Non-standard collection / 采集不规范 | System provides standardized form templates with mandatory field validation / 系统提供标准化表单模板且强制必填字段 | Data format is uniform / 数据格式统一 |
| Poor real-time access / 实时性差 | Farm manager submits data, PhD can view instantly / 场长提交数据后博士可即时查看 | Data timeliness is achieved / 数据实时性达标 |
| Inefficient analysis / 分析低效 | System auto-generates preset reports and visualizations / 系统自动生成预设报表和可视化图表 | Analysis efficiency improves / 分析效率提升 |
| Difficult traceability / 溯源困难 | Every record includes operator, timestamp, modification history / 每条记录包含操作人、时间、修改历史 | Full traceability is established / 可追溯 |
| Fragmented collaboration / 协同不畅 | Task status syncs in real-time with notification support / 任务状态实时同步且支持消息通知 | Collaboration efficiency improves / 协同效率提升 |

---

## 3. Target Users / 目标用户

### 3.1 User Roles Overview / 用户角色概览

```
博士/CEO  ──  Strategic oversight, experiment comparison, conclusions / 战略监管、实验对比、结论
    │
场长     ──  Data quality monitoring, trend review, daily oversight / 数据质量监控、趋势审查、日常监管
    │
技术员   ──  Daily data recording, on-site execution / 日常数据记录、现场执行
```

### 3.2 Technician (技术员)

**EN:** On-site operator performing daily data recording in the farm.

**ZH:** 现场操作人员，负责场内日常数据记录。

| Dimension / 维度 | Detail / 详情 |
|-----------|--------|
| Primary concern / 主要关注 | Daily recording efficiency and convenience / 日常记录效率与便捷性 |
| Data recorded / 记录数据 | Daily death/cull count & reasons, feed consumption, mortality, environmental controls, vaccines/medications, diarrhea tracking / 日死淘数量及原因、饲料耗用、死淘、环控、药品疫苗、腹泻 |
| Platform / 使用平台 | App (primary), on-site mobile operation / App 为主，现场移动操作 |
| Key need / 核心需求 | Fast, simple data entry with minimal taps; field-appropriate convenience, not a standalone data entry system / 快速简洁的数据录入，最少点击操作；符合场区便捷性，而非独立录入系统 |

### 3.3 Farm Manager (场长)

**EN:** Middle management responsible for data quality and operational oversight at a specific farm.

**ZH:** 中层管理人员，负责具体场区的数据质量和运营监管。

| Dimension / 维度 | Detail / 详情 |
|-----------|--------|
| Primary concern / 主要关注 | Data quality, trends, and alerts / 数据质量、趋势及预警 |
| Data monitored / 监控数据 | Death/cull quantity & causes, feed intake, environmental controls, vaccines/medications, pig weight & head count / 死淘数量及原因、采食量、环控、药品疫苗、猪只重量及头数 |
| Platform / 使用平台 | App (daily review) + Web (detailed analysis) / App（日常查看）+ Web（详细分析） |
| Key need / 核心需求 | Daily audit (稽核) of data completeness and accuracy; early warning of anomalies / 每日稽核数据完整性与准确性；异常提前预警 |

### 3.4 PhD Researcher & CEO (博士及CEO)

**EN:** Strategic decision-makers — PhD researchers design experiments and analyze results; CEO views experiment assets from a business perspective.

**ZH:** 战略决策者 — 博士设计实验并分析结果；CEO 从商业角度审视实验资产。

| Dimension / 维度 | Detail / 详情 |
|-----------|--------|
| Primary concern / 主要关注 | Experiment comparison, conclusions, progress, anomalies / 实验对比、实验结论、各实验进度、实验异常 |
| Data consumed / 消费数据 | Experiment group data comparison, experiment conclusions, individual experiment progress, experiment anomalies, cross-experiment horizontal comparison / 实验组数据对比、实验结论、各实验进度、实验异常、各实验横向对比 |
| Platform / 使用平台 | Web (primary), App (status checks) / Web 为主，App 查看状态 |
| Key need / 核心需求 | Deep analysis capability; data asset-ification for commercialization and replication / 深度分析能力；数据资产化用于商业化和可复制推广 |

---

## 4. Functional Architecture / 功能架构

### 4.1 System Overview / 系统总览

```
┌─────────────────────────────────────────────────────────┐
│              Experiment R&D Platform                     │
│              实验研发平台                                  │
├────────────────────────┬────────────────────────────────┤
│     Web Platform        │         App                    │
│     Web端               │         移动端                  │
│  (博士/CEO primary)     │  (场长/技术员 primary)          │
├────────────────────────┼────────────────────────────────┤
│                        │                                │
│  Overview / 概览        │  Experiment Overview / 实验概览 │
│  ├─ Experiments Status │  (experiment list + status)    │
│  │  (auto process per  │                                │
│  │   experiment step)  │  Workbench / 工作台             │
│  │  实验状态(每步骤自动) │  ├─ Data Entry / 数据录入       │
│  └─ Experiments Alerts │  ├─ Data Analysis / 数据分析    │
│     实验预警             │  └─ Data Alert / 数据预警       │
│                        │                                │
│  Analysis / 分析        │                                │
│  └─ Analysis Report    │                                │
│     分析报表             │                                │
└────────────────────────┴────────────────────────────────┘
```

### 4.2 Web Platform Modules / Web端模块

**Overview — Experiments Status / 概览 — 实验状态**
- Experiment list table with columns: experiment code, building/unit, growth stage, location, experiment phases, current progress, status, anomaly level, record completeness (with progress bar), report access dropdown / 实验列表：实验编号、栋舍-单元、生长阶段、猪场地点、实验阶段、当前进度、状态、异常等级、记录完整度（含进度条）、报表下拉菜单
- Stat cards: total experiments, average record completeness, anomaly data records, today's new records / 统计卡片：实验总数、平均记录完整度、异常数据记录、今日新增记录
- Filter/search by experiment code, farm location, experiment status / 按实验编号、实验场、实验状态筛选
- Automated tracking of each experiment step's process / 自动追踪每步实验流程

**Overview — Experiments Alerts / 概览 — 实验预警**
- Alert table: time, experiment, pen, anomaly type, description, action link / 预警表格：预警时间、实验编号、栏位、异常类型、异常描述、操作
- Severity classification (anomaly level per experiment) / 严重程度分级
- Drill-down to detailed reports from alert entries / 从预警条目下钻至详细报表

**Analysis — Analysis Report / 分析 — 分析报表**
- Summary stat cards: daily death/cull count, current stock count, daily feed amount (kg), average temperature (°C), diarrhea head count / 汇总统计卡片：当日死淘数、当日存栏数、日下料量(kg)、平均温度(℃)、腹泻头数
- Interactive charts (line charts for date-based trends, bar charts for group comparisons) / 交互式图表（日期趋势折线图、分组对比柱状图）
- 8 report types accessible per experiment / 每个实验可访问 8 种报表：
  - Daily report (日报表)
  - Stage report (阶段报表)
  - Experiment summary report (实验总结表)
  - Death/cull detail report (死淘明细表)
  - Diarrhea detail report (腹泻明细表)
  - Medicine/vaccine detail report (药品疫苗明细表)
  - Environmental control detail report (环控明细表)
  - Weight detail report (称重明细表)

### 4.3 App Modules / 移动端模块

**Experiment Overview / 实验概览**
- Experiment list with search, status filtering / 实验列表，支持搜索和状态筛选
- Experiment detail view (basic info, progress statistics) / 实验详情（基本信息、进度统计）
- Entry point for new experiment creation / 新建实验入口

**Workbench — Data Entry / 工作台 — 数据录入**
- Standardized forms per data type: death/cull, feed intake, environmental controls, medicine/vaccine, diarrhea, weight / 按数据类型标准化表单：死淘、采食、环控、药品疫苗、腹泻、称重
- Field validation (type constraints, mandatory fields, range checks) / 字段校验（类型限制、必填项、合理范围检查）
- Support for manual entry, auto-sync from external feeds, and batch Excel import / 支持手工录入、外部数据自动同步、Excel 批量导入

**Workbench — Data Analysis / 工作台 — 数据分析**
- Mobile-optimized data views / 移动端优化的数据视图
- Stage-level and experiment-level summaries / 阶段级别和实验级别汇总

**Workbench — Data Alert / 工作台 — 数据预警**
- Push notifications for anomaly detection / 异常检测推送通知
- Alert review with drill-down to relevant reports / 预警查看与下钻至相关报表
- Improvement note annotation and tracking / 改善建议备注与跟踪

### 4.4 Cross-Cutting Services / 横切服务

| Service / 服务 | Description / 说明 |
|---------|-------------|
| Authentication & RBAC / 认证与权限 | Role-based access: 博士 (full access), 场长 (farm-scoped), 技术员 (recording-focused) / 基于角色的访问控制：博士（全部权限）、场长（场区范围）、技术员（记录为主） |
| Real-time sync / 实时同步 | App data instantly synced to cloud; Web refreshed in real-time / App 数据即时上传云端；Web 端实时刷新 |
| Notification system / 通知系统 | Push notifications for data submissions, approvals, anomalies / 数据提交、审核、异常的推送通知 |
| Data import/export / 数据导入导出 | Excel template download → data fill → upload with validation; export to Excel/PDF / Excel 模板下载 → 数据填写 → 带校验上传；导出 Excel/PDF |
| Audit logging / 审计日志 | Every record: operator, timestamp, data source (manual/auto), modification history / 每条记录：操作人、时间戳、数据来源（手工/自动）、修改历史 |

### 4.5 Web Platform Navigation Structure / Web端导航结构

```
实验研发
├── 知识库 (Knowledge Base)
├── 项目管理 (Project Management)
├── 实验场 (Farms)
├── 猪实验数据 (Swine Experiment Data)
│   ├── 实验概览 (default landing / 默认首页)
│   └── 报表分析 (Report Analysis)
└── 家禽实验数据 (Poultry Experiment Data - future / 未来扩展)
```

Breadcrumb navigation / 面包屑导航: 实验研发 › 猪实验数据 › 实验概览

---

## 5. Core User Journey / 核心用户旅程

### 5.1 End-to-End Experiment Lifecycle / 端到端实验生命周期

```
┌──────────────┐    ┌──────────────┐    ┌──────────────────┐
│ 1. New       │───▶│ 2. Experiment│───▶│ 3. Stage Init    │
│ Experiment   │    │ Grouping     │    │ (待开始→进行中)   │
│ 新建实验      │    │ 实验分组      │    │ 阶段初始化        │
│ (博士/Web)   │    │ (场长上传)    │    └────────┬─────────┘
└──────────────┘    └──────────────┘             │
                                                 ▼
┌──────────────┐    ┌──────────────┐    ┌──────────────────┐
│ 6. Stage     │◀───│ 5. Stage     │◀───│ 4. Daily         │
│ Data Review  │    │ End Submit   │    │ Recording        │
│ 阶段数据审核  │    │ 阶段结束提交   │    │ 日常巡栏记录       │
│ (博士/Web)   │    │ (场长)       │    │ (场长,技术员/App) │
└──────┬───────┘    └──────────────┘    └──────────────────┘
       │
       ├── Approved / 通过 ──▶ Stage Status / 阶段状态: 已结束
       │                    │
       │                    ▼
       │         ┌──────────────────┐
       │         │ 7. Stage         │
       │         │ Comparison/Merge │
       │         │ 阶段对比/合并      │
       │         │ (博士/Web)       │
       │         └────────┬─────────┘
       │                  │
       │         ┌────────▼─────────┐
       │         │ 8. Next Stage?   │
       │         │ 下一阶段?         │
       │         │ Yes → back to 3  │
       │         │ No  → Final Merge│
       │         │ 是→回到第3步       │
       │         │ 否→最终合并        │
       │         └────────┬─────────┘
       │                  │
       └── Rejected / 驳回 ──▶ Data Correction / 数据修正 (场长) → back to 4
                          │
                          ▼
                  ┌──────────────┐    ┌──────────────┐
                  │ 9. Close-out │───▶│ 10. Generate │
                  │ Confirmation │    │ Report       │
                  │ 结栏确认       │    │ 生成报告      │
                  │ (博士)       │    │ (博士/Web)   │
                  └──────────────┘    └──────────────┘
```

### 5.2 Stage State Machine / 阶段状态机

```
待开始 ──(启动阶段/Start Stage)──▶ 进行中 ──(提交结束/Submit End)──▶ 待审核
  (Pending)      │                (In Progress)                    (Pending Review)
   ▲              │                                                   │
   │              │                      ┌────────────────────────────┴────────┐
   │              │                      ▼                                      ▼
   │              └──(审核不通过/Reject)──┘                              (审核通过/Approve)
   │                                                                              │
   │                                                                              ▼
   └───────────────────(启动下一阶段/Start Next Stage)────────────────── 已结束 (Completed)
                                                                              │
                                                                     (无下一阶段/No Next Stage)
                                                                              │
                                                                              ▼
                                                                        已归档 (Archived)
```

### 5.3 High-Level User Flow / 顶层用户流程

```
login → experiment overview / new experiment → drill into specific experiment
登录 → 实验概览 / 新建实验 → 进入具体实验
→ experiment recording process → stage review → stage comparison → ... → final report
→ 实验记录流程 → 阶段审核 → 阶段对比 → ... → 最终报告
```

### 5.4 Daily Data Entry Journeys (App) / 日常数据录入旅程（移动端）

**Manual Entry / 手工录入:**
Select experiment → Select record type → Enter data into standardized form
选择实验 → 点击记录类型 → 录入数据到标准化表单

**Auto Sync / 自动同步:**
Select experiment → Select record type → Review synced data → Correct anomalies if needed
选择实验 → 点击记录类型 → 查看同步数据 → 若异常，修改数据

**Batch Import / 批量导入:**
Select experiment → Select record type → Download template / Upload data → Complete form, upload
选择实验 → 点击记录类型 → 点击下载上传模板 / 点击上传数据 → 完成数据填写，上传数据

**Anomaly Push / 异常推送:**
System detects issue → User views anomaly indicator report → Optionally add improvement notes → Track improvement outcome
发现问题 → 查看异常指标对应报表 → 可选，备注改善建议 → 跟踪改善结果

---

## 6. Module Descriptions / 模块描述

### 6.1 Experiment Overview (Web — Landing Page) / 实验概览（Web端首页）

**Decision / 决策:** Homepage uses experiment overview, not a single-experiment record view. (Decision-001, 2026-06-22)
首页采用实验概览，而非具体单一实验记录。（Decision-001, 2026-06-22）

**Rationale / 原因:**
1. Management needs to see all experiment progress and anomalies upon login / 管理层进入系统后首先需要看到全部实验进度及异常
2. Data recording is a basic maintenance function, accessible through experiment progress drill-down / 数据记录作为基础的数据维护入口，可通过试验进度进入

**Components / 组件:**
- **4 stat cards** at top: total experiments, average record completeness (%), anomaly data records, today's new records — each with trend indicator / 顶部 4 张统计卡片：实验总数、平均记录完整度(%)、异常数据记录、今日新增记录——各附趋势指标
- **Experiment list table**: sortable, filterable table with columns for code, building/unit, growth stage, location, phases, current progress, status, anomaly level, completeness (progress bar), and a report access dropdown with 8 report types / 实验列表：可排序、可筛选表格，包含实验编号、栋舍-单元、生长阶段、地点、阶段、当前进度、状态、异常等级、完整度（进度条）、8 种报表下拉菜单
- **Anomaly alert table**: time, experiment, pen, anomaly type, description, drill-down action / 异常预警表：时间、实验、栏位、异常类型、描述、下钻操作
- **Search/filter bar**: experiment code (text), farm location (dropdown), experiment status (dropdown) / 搜索筛选栏：实验编号（文本）、实验场（下拉）、实验状态（下拉）

### 6.2 Data Entry (App — Primary) / 数据录入（移动端 — 主要）

**Purpose / 目的:** Standardized on-site data collection by farm managers and technicians. / 场长和技术员进行标准化的现场数据采集。

**Data types supported / 支持的数据类型:**
- Death/cull daily record (数量, 重量, 性别, 原因, 天数, 累计) / 死淘日记录
- Feed intake (饲喂量 by pen) / 采食记录
- Environmental controls (temperature, humidity, etc.) / 环控记录
- Medicine/vaccine administration / 药品疫苗记录
- Diarrhea tracking / 腹泻记录
- Weight measurement / 称重记录

**Validation rules / 校验规则:**
- Field type enforcement (number, select, date) / 字段类型限制（数字/选择/日期）
- Mandatory field checking / 强制校验必填项
- Reasonable range validation (e.g., weight plausible range) / 合理范围校验（如体重合理区间）
- Chronological order validation / 时间顺序校验

**Design principle / 设计原则:** Not a standalone data entry system — integrated into the experiment workflow with farm-appropriate convenience. / 不做单独的录入系统——将录入融入实验流程，符合场区便捷性。

### 6.3 Analysis & Reports (Web — Primary) / 分析与报表（Web端 — 主要）

**Purpose / 目的:** Automated report generation from raw experiment data, eliminating manual Excel aggregation. / 从原始实验数据自动生成报表，消除手工 Excel 汇总。

**Report types (8 pre-built) / 报表类型（8种预置）:**
1. 日报表 (Daily report)
2. 阶段报表 (Stage report)
3. 实验总结表 (Experiment summary)
4. 死淘明细表 (Death/cull detail)
5. 腹泻明细表 (Diarrhea detail)
6. 药品疫苗明细表 (Medicine/vaccine detail)
7. 环控明细表 (Environment detail)
8. 称重明细表 (Weight detail)

**Analysis capabilities / 分析能力:**
- **Stage comparison / 阶段对比**: Compare treatment groups within the same stage / 对比同一阶段内不同处理组
- **Stage merge / 阶段合并**: Aggregate data across completed stages / 汇总已完成阶段的数据
- **Cross-experiment comparison / 跨实验对比**: Compare results across different experiments / 对比不同实验的结果
- **Final merge / 最终合并**: Complete dataset aggregation at experiment end / 实验结束时完整数据集汇总
- **Export / 导出**: Excel (further analysis / 进一步分析), PDF (sharing/archival / 分享/存档)

### 6.4 Alerts & Anomaly Detection (Dual-Platform) / 预警与异常检测（双端）

**Purpose / 目的:** Proactive identification of data anomalies with severity classification. / 主动识别数据异常并进行严重程度分级。

**Alert types / 预警类型:** Abnormal mortality spikes, feed intake deviations, environmental control outliers, weight anomalies, diarrhea outbreaks / 死淘异常飙升、采食量偏差、环控异常、体重异常、腹泻爆发

**Workflow / 工作流:** System detects → Pushes alert → User reviews relevant report → Optionally annotates improvement suggestions → Tracks improvement outcomes / 系统检测 → 推送预警 → 用户查看相关报表 → 可选备注改善建议 → 跟踪改善结果

**Severity levels / 严重等级:** Classified per experiment (displayed as anomaly level column in the experiment list) / 按实验分级（在实验列表中显示为异常等级列）

### 6.5 Experiment Lifecycle Management / 实验生命周期管理

**Experiment creation (博士/Web) / 实验创建:**
- Experiment code (unique ID, e.g., SWINE-NUR-XY-001-2026) / 实验编号（唯一标识）
- Growth stage selection (保育, 育肥, 保育到育肥) / 生长阶段选择
- Farm location assignment / 实验场分配
- Phase/stage configuration / 阶段配置

**Experiment grouping (场长 uploads) / 实验分组:**
- Treatment group assignment to building/unit/pens / 处理组分配至栋-单元-栏位
- Initial pig count per group / 每组初始猪只数量
- Group confirmation workflow / 分组确认流程

**Stage management / 阶段管理:**
- Multi-stage experiment support with independent stage lifecycle / 支持多阶段实验，每阶段独立生命周期
- Stage-end submission by farm manager / 场长提交阶段结束
- Stage data review and approval by PhD / 博士审核阶段数据
- Stage comparison and merge analysis / 阶段对比与合并分析
- Final close-out confirmation and archival / 最终结栏确认与归档

---

## 7. Business Value / 商业价值

### 7.1 Value by Role / 按角色划分的价值

| Role / 角色 | Value Delivered / 交付价值 |
|------|-----------------|
| **CEO** | Experiment data transformed into enterprise assets (数据资产化); enables replication of successful experiments across farms (可复制推广); accelerates path to commercialization (商业化) / 实验数据转化为企业资产；支持成功实验跨场复制推广；加速商业化进程 |
| **PhD Researcher / 博士** | Complete visibility into experiment progress; accumulated experiment data and conclusions ready for commercialization; automated reporting replaces manual Excel work / 全面掌控实验进度；沉淀实验数据及结论用于商业化；自动报表取代手工 Excel |
| **Farm Manager / 场长** | Daily audit (稽核) capability; data quality monitoring with trend visibility; early warning system for operational anomalies / 每日稽核能力；数据质量监控及趋势可见性；运营异常提前预警 |
| **Technician / 技术员** | Electronic recording replaces paper/Excel; standardized forms reduce errors; on-site mobile convenience / 电子记录取代纸质/Excel；标准化表单减少错误；现场移动便捷 |

### 7.2 Key Metrics (Target) / 关键指标（目标）

| Metric / 指标 | Current (Excel) / 现状 | Target (Platform) / 目标 |
|--------|-----------------|-------------------|
| Data recording standardization / 数据记录标准化 | No unified template / 无统一模板 | 100% structured forms with validation / 100% 结构化带校验表单 |
| Data availability latency / 数据可用延迟 | Days (file transfer) / 天级（文件传输） | Real-time (instant sync) / 实时（即时同步） |
| Report generation time / 报表生成时间 | Hours (manual aggregation) / 小时级（手工汇总） | Minutes (auto-generated) / 分钟级（自动生成） |
| Data traceability / 数据可追溯性 | None (version chaos) / 无（版本混乱） | Full audit trail per record / 每条记录完整审计轨迹 |
| Experiment oversight / 实验监管 | Per-experiment phone calls / 逐个实验电话沟通 | Single dashboard, all experiments / 单一仪表盘，所有实验 |

### 7.3 Competitive Context / 竞争背景

**EN:** Current baseline: Excel files manually passed between PhD researchers and farm staff. This is the status quo being replaced. Platform differentiator: Purpose-built for livestock experiment management — not a generic LIMS or form tool. Integrates the full experiment lifecycle (design → recording → approval → analysis → archival) with role-appropriate interfaces on Web and App.

**ZH:** 当前基线：Excel 文件在博士和现场人员之间手工流转。这是正在被替代的现状。平台差异点：专为养殖实验管理打造——不是通用 LIMS 或表单工具。集成完整实验生命周期（设计→记录→审核→分析→归档），在 Web 和 App 上提供适配各角色的界面。

---

## 8. Data Sources / 数据来源

### 8.1 Data Collection Methods / 数据采集方式

| Method / 方式 | Description / 描述 | Primary User / 主要用户 |
|--------|-------------|--------------|
| **Manual entry (App) / 手工录入** | Standardized forms filled on-site / 现场填写标准化表单 | 技术员, 场长 |
| **Auto sync / 自动同步** | Data ingested from external farm systems/feeds / 从外部场区系统/数据源接入 | System / 系统 |
| **Batch import (Web) / 批量导入** | Excel template download → fill → upload with validation / Excel 模板下载→填写→带校验上传 | 博士, 场长 |

### 8.2 Data Domains / 数据域

| Domain / 域 | Key Fields / 关键字段 | Collection Frequency / 采集频率 |
|--------|-----------|---------------------|
| Death/Cull / 死淘 | Count, weight, gender, reason, days, cumulative totals / 数量、重量、性别、原因、天数、累计 | Daily / 每日 |
| Feed Intake / 采食 | Feed amount (kg) per pen / 每栏饲喂量(kg) | Daily / 每日 |
| Environmental Control / 环控 | Temperature (°C), humidity, ventilation / 温度(℃)、湿度、通风 | Daily / 每日 |
| Medicine/Vaccine / 药品疫苗 | Type, dosage, administration date, batch / 类型、剂量、给药日期、批次 | Per event / 按事件 |
| Diarrhea / 腹泻 | Head count, severity, duration / 头数、严重程度、持续时间 | Daily / 每日 |
| Weight / 称重 | Individual/group weight measurement / 个体/群体称重 | Per stage milestone / 每阶段节点 |
| Experiment Metadata / 实验元数据 | Code, location, growth stage, phases, groups / 编号、地点、生长阶段、阶段、分组 | Per experiment / 每实验 |

### 8.3 Data Integrity / 数据完整性

**EN:**
- Every record tagged with: operator ID, timestamp, data source (manual/auto/import)
- Modification history preserved with version comparison
- Stage-level data completeness validation before stage-end approval
- Field-level validation rules at point of entry

**ZH:**
- 每条记录标记：操作人 ID、时间戳、数据来源（手工/自动/导入）
- 修改历史保留，支持版本对比
- 阶段结束审核前的阶段级数据完整性校验
- 录入时的字段级校验规则

---

## 9. Intelligent Capabilities / 智能能力

### 9.1 What "智能" (Intelligent) Means / "智能"的含义

**EN:** The platform is positioned as an "智能养殖实验平台." The intelligence is delivered through automation and rule-based systems — not machine learning in the current scope. Advanced statistical analysis (significance testing, AI prediction models) is explicitly out of MVP scope.

**ZH:** 平台定位为"智能养殖实验平台"。智能通过自动化和规则驱动系统实现——当前范围内不包含机器学习。高级统计分析（显著性检验、AI 预测模型）明确不在 MVP 范围内。

### 9.2 Current Intelligent Features / 当前智能功能

**Automated Data Alerts / 自动化数据预警**
- Rule-based anomaly detection across all data domains / 跨所有数据域的规则驱动异常检测
- Severity classification with alert prioritization / 严重程度分级与预警优先级
- Push notification to relevant roles / 向相关角色推送通知
- Closed-loop tracking: detect → review → annotate → improve → verify / 闭环跟踪：检测→审查→备注→改善→验证

**Automated Report Generation / 自动化报表生成**
- 8 pre-built report templates auto-populated from raw data / 8 种预置报表模板，从原始数据自动填充
- Stage summary reports generated on stage completion / 阶段完成时自动生成阶段汇总报告
- Experiment summary report on experiment completion / 实验完成时自动生成实验总结报告
- Charts and visualizations auto-generated (line, bar, comparison) / 自动生成图表和可视化（折线图、柱状图、对比图）

**Experiment Process Automation / 实验流程自动化**
- Automatic tracking of each experiment step's process / 自动追踪每步实验流程
- Stage state machine with automatic status transitions / 阶段状态机自动状态转换
- Data completeness scoring (记录完整度 %) calculated automatically / 自动计算数据完整度评分

**Stage Analysis Automation / 阶段分析自动化**
- Stage data merge across groups / 跨组阶段数据合并
- Cross-stage data aggregation / 跨阶段数据汇总
- Treatment group comparison within stages / 阶段内处理组对比

### 9.3 Future Intelligent Capabilities (Post-MVP) / 未来智能能力（MVP之后）

- Predictive anomaly detection (pattern-based, beyond threshold rules) / 预测性异常检测（基于模式，超越阈值规则）
- AI-generated experiment stage summaries and conclusions / AI 生成实验阶段总结和结论
- Natural language query for experiment data / 实验数据自然语言查询
- Intelligent data quality suggestions during entry / 录入时智能数据质量建议
- Advanced statistical analysis (significance testing, regression) / 高级统计分析（显著性检验、回归分析）
- AI prediction models for growth/health outcomes / 生长/健康结果 AI 预测模型

---

## 10. Roadmap / 路线图

### Phase 1 — Core MVP (Current) / 第一阶段 — 核心 MVP（当前）

| Feature / 功能 | Priority / 优先级 | Status / 状态 |
|---------|----------|--------|
| Standardized data collection forms (App) / 标准化数据采集表单 | P0 | Prototype / 原型 |
| Real-time data sync (App ↔ Cloud ↔ Web) / 实时数据同步 | P0 | Prototype / 原型 |
| Role-based access control / 角色权限控制 | P0 | Planned / 规划中 |
| Experiment overview dashboard (Web) / 实验概览仪表盘 | P0 | Prototype / 原型 |
| Daily data recording workflows (App) / 日常数据记录流程 | P0 | Prototype / 原型 |
| Batch Excel import (Web) / Excel 批量导入 | P1 | Planned / 规划中 |
| Basic anomaly alerts (rule-based) / 基础异常预警（规则驱动） | P1 | Prototype / 原型 |

### Phase 2 — Analysis & Traceability / 第二阶段 — 分析与溯源

| Feature / 功能 | Priority / 优先级 | Status / 状态 |
|---------|----------|--------|
| 8 pre-built report types (Web) / 8种预置报表 | P1 | Prototype / 原型 |
| Stage comparison & merge analysis / 阶段对比与合并分析 | P1 | Planned / 规划中 |
| Full audit logging & traceability / 完整审计日志与溯源 | P1 | Planned / 规划中 |
| Data version comparison / 数据版本对比 | P1 | Planned / 规划中 |
| Stage-end review & approval workflow / 阶段结束审核流程 | P1 | Planned / 规划中 |

### Phase 3 — Collaboration & Scale / 第三阶段 — 协同与规模化

| Feature / 功能 | Priority / 优先级 | Status / 状态 |
|---------|----------|--------|
| Task assignment & progress tracking / 任务分配与进度跟踪 | P2 | Planned / 规划中 |
| Cross-experiment comparison / 跨实验对比 | P2 | Planned / 规划中 |
| Enhanced notification system / 增强通知系统 | P2 | Planned / 规划中 |
| Offline data entry support (App) / 离线数据录入支持 | P2 | Planned / 规划中 |
| Poultry experiment data module / 家禽实验数据模块 | P2 | Future / 未来 |

### Phase 4 — Intelligence Upgrade / 第四阶段 — 智能升级

| Feature / 功能 | Priority / 优先级 | Status / 状态 |
|---------|----------|--------|
| Predictive anomaly detection / 预测性异常检测 | Future / 未来 | Not started / 未开始 |
| AI-generated experiment summaries / AI 生成实验总结 | Future / 未来 | Not started / 未开始 |
| Advanced statistical analysis / 高级统计分析 | Future / 未来 | Not started / 未开始 |
| Third-party system integration / 第三方系统集成 | Future / 未来 | Not started / 未开始 |

---

## Appendix: Document Inventory / 附录：文档清单

| Document / 文档 | Description / 说明 |
|----------|-------------|
| `1. vision.html` | Product vision, positioning, core value, target users, scope boundaries / 产品愿景、定位、核心价值、目标用户、范围边界 |
| `2. user.html` | User role definitions, concerns, and data focus per role / 用户角色定义、关注点及各角色数据焦点 |
| `3. journey.html` | User journeys for data entry (manual, auto, batch), anomaly handling, and experiment flow / 数据录入（手工、自动、批量）、异常处理及实验流程的用户旅程 |
| `4. architecture.html` | Functional architecture for Web and App platforms / Web 和 App 平台的功能架构 |
| `5. decision.html` | Key product decisions with rationale (Decision-001: overview-first homepage) / 关键产品决策及理由 |
| `prototype/` | 11 HTML prototype screens covering full experiment lifecycle / 11 个 HTML 原型页面，覆盖完整实验生命周期 |
| `app-flow-preview.html` | Mobile app page flow diagram with screen mockups / 移动端页面流转图及界面示意 |
| `猪实验管理系统设计.md` | Design specification: problem analysis, solution design, validation logic, stage state machine / 设计规格：问题分析、方案设计、验证逻辑、阶段状态机 |
| `docs/review-report.md` | Product Brain review with findings classified by severity (P0/P1/P2) / Product Brain 评审报告，按严重程度分类 |
