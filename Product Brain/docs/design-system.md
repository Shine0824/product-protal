# Experiment R&D Platform — Design System

**Version:** 1.0
**Date:** 2026-06-22
**Source:** 11 prototype HTML pages under `prototype/`

---

## 1. Color System

### 1.1 Brand Palette

| Token | Hex | Usage |
|-------|-----|-------|
| `--brand-primary` | `#1ab394` | Primary buttons, active states, emphasis, links, flow-node active bg |
| `--brand-primary-hover` | `#17a689` / `#18a689` | Primary button hover |
| `--brand-primary-light` | `#e8f5e9` | Completed state bg, success backgrounds |
| `--brand-primary-light-border` | `#a5d6a7` | Completed state border, hover border |

### 1.2 Neutral Palette

| Token | Hex | Usage |
|-------|-----|-------|
| `--bg-page` | `#f5f7fa` | Page background |
| `--bg-white` | `#ffffff` | Card backgrounds |
| `--bg-section` | `#fafafa` | Section backgrounds, content headers, form sections |
| `--bg-header` | `#fafbfc` | Card headers (drawer) |
| `--text-primary` | `#333333` | Primary text, headings |
| `--text-secondary` | `#666666` | Secondary text, labels |
| `--text-muted` | `#999999` | Muted text, placeholders |
| `--text-muted-light` | `#94a3b8` / `#64748b` | Drawer field labels, route paths |
| `--border-light` | `#e6e6e6` | Standard borders |
| `--border-input` | `#dddddd` | Input borders, secondary button borders |
| `--border-card` | `#e8eaed` | Card borders |
| `--shadow-card` | `0 2px 12px rgba(0, 0, 0, 0.08)` | Standard card shadow |
| `--shadow-sm` | `0 2px 8px rgba(0, 0, 0, 0.04)` | Light section shadow |
| `--shadow-hover` | `0 2px 8px rgba(26, 179, 148, 0.3)` | Active/primary glow |

### 1.3 Semantic Palette

| Token | Hex | Usage |
|-------|-----|-------|
| `--semantic-success` | `#67c23a` | Positive trends, success states |
| `--semantic-danger` | `#f56c6c` | Negative trends, errors, delete buttons |
| `--semantic-danger-hover` | `#f44336` | Delete button hover |
| `--semantic-warning` | `#e6a23c` | Warning states, pending badges |
| `--semantic-info` | `#3b82f6` | Info links, edit actions, Web platform indicator |
| `--semantic-info-light` | `#4facfe` | Calendar medicine marker |

### 1.4 Sidebar Palette

| Token | Hex | Usage |
|-------|-----|-------|
| `--sidebar-bg` | `linear-gradient(180deg, #1e3a5f 0%, #2d5a87 100%)` | Experiment Overview sidebar |
| `--sidebar-bg-alt` | `linear-gradient(180deg, #1a2035 0%, #2d3550 100%)` | Analysis Report sidebar |
| `--sidebar-text` | `#ffffff` | Sidebar text |
| `--sidebar-text-muted` | `rgba(255, 255, 255, 0.7)` | Inactive menu items |
| `--sidebar-item-hover` | `rgba(255, 255, 255, 0.1)` | Menu item hover |
| `--sidebar-divider` | `rgba(255, 255, 255, 0.1)` | Logo divider |

### 1.5 Summary Card Gradients (Web Reports)

| Token | Gradient | Use |
|-------|----------|-----|
| `--gradient-purple` | `#667eea → #764ba2` | Primary metric card |
| `--gradient-pink` | `#f093fb → #f5576c` | Secondary metric card |
| `--gradient-blue` | `#4facfe → #00f2fe` | Tertiary metric card |
| `--gradient-teal` | `#43e97b → #38f9d7` | Quaternary metric card |
| `--gradient-warm` | `#fa709a → #fee140` | Fifth metric card (dark text) |

### 1.6 Status Color Map

| Status | Background | Text/Border |
|--------|-----------|-------------|
| Active / In Progress | `#1ab394` | `#ffffff` |
| Completed | `#e8f5e9` | `#1ab394` |
| Pending | `#f5f7fa` | `#e6e6e6` |
| Locked / Disabled | `#f5f7fa` (opacity 0.5) | `#e6e6e6` |
| Anomaly Low | `rgba(26,179,148,0.1)` | `#1ab394` |
| Anomaly Medium | `rgba(230,162,60,0.1)` | `#e6a23c` |
| Anomaly High | `rgba(245,108,108,0.1)` | `#f56c6c` |

---

## 2. Typography

### 2.1 Font Stack

```css
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto,
             'Helvetica Neue', Arial, sans-serif;
```

**Monospace (route/path display):**
```css
font-family: 'SF Mono', 'Menlo', monospace;
```

### 2.2 Type Scale

| Token | Size | Weight | Line Height | Usage |
|-------|------|--------|-------------|-------|
| `--text-stat` | 28px | bold (700) | 1.2 | Stat card values |
| `--text-stat-sm` | 24px | bold (700) | 1.2 | Summary card values |
| `--text-stat-xs` | 20px | bold (700) | 1.2 | Section metric values |
| `--text-title-lg` | 18px | bold (700) | 1.4 | Experiment code, page titles |
| `--text-title` | 16px | bold (700) | 1.4 | Content titles, section titles |
| `--text-title-sm` | 14-15px | bold (700) | 1.4 | Sub-section titles, card titles |
| `--text-body` | 13-14px | normal (400) | 1.5-1.6 | Body text, form labels |
| `--text-body-sm` | 12-13px | normal (400) | 1.5 | Table cells, secondary info |
| `--text-caption` | 11-12px | normal (400) | 1.4 | Captions, trend text, meta |
| `--text-label` | 11px | 600 | 1.4 | Drawer field labels (uppercase) |
| `--text-badge` | 10px | 600 | 1.2 | Platform badges (uppercase) |

### 2.3 Text Colors

| Token | Value | Usage |
|-------|-------|-------|
| Headings | `#333` / `#1e293b` | All titles |
| Body | `#475569` / `#333` | Paragraphs, descriptions |
| Secondary | `#666` | Labels, help text |
| Muted | `#999` | Placeholders, metadata |
| Link | `#3b82f6` | Clickable text, navigation |
| Brand | `#1ab394` | Experiment codes, emphasized values |
| Danger | `#f56c6c` | Required markers, negative values |
| White | `#fff` | On dark/gradient backgrounds |

---

## 3. Cards

### 3.1 Standard Content Card

```css
.card {
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.08);
  overflow: hidden;
  margin-bottom: 20px;
}
.card-header {
  padding: 15px 20px;
  border-bottom: 1px solid #e6e6e6;
  background-color: #fafafa;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.card-title { font-size: 16px; font-weight: bold; color: #333; }
.card-body { padding: 20px; }
```

**Used in:** Experiment lists, anomaly alerts, stage sections, daily record forms.

### 3.2 Experiment Header Card

```css
.experiment-header {
  background-color: #fff;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.08);
}
.experiment-header .exp-code {
  font-size: 18px;
  font-weight: bold;
  color: #1ab394;
  margin-bottom: 15px;
}
```

**Used in:** Every experiment detail page — groups info items in a 4-column grid with `#fafafa` background items.

### 3.3 Info Item (Card Interior)

```css
.info-item {
  display: flex;
  justify-content: space-between;
  padding: 10px;
  background-color: #fafafa;
  border-radius: 4px;
}
.info-label { color: #999; font-size: 14px; }
.info-value { color: #333; font-weight: 500; }
```

**Layout:** `grid-template-columns: repeat(4, 1fr); gap: 15px;`

### 3.4 Stat Card (Dashboard)

```css
.stat-card {
  background-color: #fff;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.08);
}
.stat-icon { font-size: 32px; margin-bottom: 10px; }
.stat-value { font-size: 28px; font-weight: bold; color: #333; }
.stat-label { font-size: 14px; color: #999; margin-top: 5px; }
.stat-trend { font-size: 12px; margin-top: 8px; }
.trend-up { color: #1ab394; }
.trend-down { color: #f56c6c; }
```

**Layout:** `grid-template-columns: repeat(4, 1fr); gap: 15px;`

### 3.5 Summary Metric Card (Gradient)

```css
.summary-card {
  flex: 1; min-width: 180px; padding: 15px;
  border-radius: 8px; color: #fff; text-align: center;
}
.summary-card .summary-value { font-size: 28px; font-weight: bold; }
.summary-card .summary-label { font-size: 12px; opacity: 0.9; margin-top: 5px; }
```

**Color variants:**
| Class | Gradient |
|-------|----------|
| Default | `#667eea → #764ba2` |
| `.orange` | `#f093fb → #f5576c` |
| `.green` | `#4facfe → #00f2fe` |
| `.teal` | `#43e97b → #38f9d7` |
| `.purple` | `#a8edea → #fed6e3` (dark text) |
| `.yellow` | `#fa709a → #fee140` |

### 3.6 Product Guide Card (Drawer)

```css
.guide-page-card {
  background: #fff;
  border: 1px solid #e8eaed;
  border-radius: 8px;
  margin-bottom: 12px;
  overflow: hidden;
}
.guide-page-card.web-card { border-left: 3px solid #3b82f6; }
.guide-page-card.app-card { border-left: 3px solid #1ab394; }
.guide-card-header {
  padding: 14px 16px; cursor: pointer;
  background: #fafbfc;
  display: flex; align-items: center; justify-content: space-between;
}
.guide-card-body { padding: 16px; border-top: 1px solid #f0f0f0; }
```

---

## 4. Tables

### 4.1 Element Plus Table (Primary)

All data tables use Element Plus `<el-table>` with borders:

```css
.el-table {
  font-size: 12px;
  --el-table-header-text-color: #666;
  --el-table-row-hover-bg-color: #f8f9fa;
}
.el-table th { background-color: #fafafa; }
.el-table__body tr { cursor: pointer; }
```

**Column patterns:**
- Experiment codes: `#1ab394`, bold, clickable, `text-overflow: ellipsis`
- Current progress: `#3b82f6`, underlined, clickable
- Status tags: colored badges (see Status Color Map)
- Anomaly levels: severity badges (see Status Color Map)
- Completeness: 6px progress bar + percentage text

**Column widths:** `min-width` based on content with `width="auto"`, text wrapping via `white-space: nowrap` + `text-overflow: ellipsis`.

### 4.2 Report Table (Static)

```css
.report-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 12px;
}
.report-table th, .report-table td {
  border: 1px solid #e6e6e6;
  padding: 8px;
  text-align: center;
  white-space: nowrap;
}
.report-table th { background-color: #f8f9fa; font-weight: bold; color: #333; }
.report-table tr:hover { background-color: #f5f7fa; }
```

**Used in:** Analysis Report page — up to 28 columns, horizontal scroll wrapper.

### 4.3 Progress Bar

```css
.progress-bar {
  height: 6px; background-color: #e6e6e6; border-radius: 3px; overflow: hidden;
}
.progress-fill {
  height: 100%;
  background: var(--semantic-success); /* default green */
}
.progress-fill.progress-complete { background: #1ab394; }   /* ≥80% */
.progress-fill.progress-warning { background: #e6a23c; }    /* 50-79% */
.progress-fill.progress-danger  { background: #f56c6c; }    /* <50% */
```

---

## 5. Charts

### 5.1 Technology

Charts use **Chart.js** (loaded from CDN). Canvas elements rendered within `.chart-container`.

```css
.chart-container {
  width: 100%;
  height: 300px;
  margin-bottom: 20px;
}
```

### 5.2 Chart Types Observed

| Chart | Configuration | Usage |
|-------|--------------|-------|
| Line chart | Dual-axis: date/日龄 vs 头数 + 死淘率(%) | Mortality trend over time |
| Bar chart | Grouped bars | Treatment group comparison |
| Calendar heatmap | 7-column CSS grid | Daily data presence (green=recorded, red=vaccine, blue=medicine) |

### 5.3 Calendar Heat Map

```css
.calendar-chart {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 5px;
  max-width: 600px;
}
.calendar-day {
  aspect-ratio: 1;
  font-size: 12px;
  border-radius: 4px;
  background-color: #f8f9fa;
}
.calendar-day.has-data { background-color: #1ab394; color: #fff; }
.calendar-day.has-data.vaccine { background-color: #f56c6c; }
.calendar-day.has-data.medicine { background-color: #4facfe; }
.calendar-day.today { border: 2px solid #1ab394; }
```

### 5.4 Empty / No-Data State

```css
.no-data {
  text-align: center;
  padding: 60px;
  color: #999;
}
.no-data-icon { font-size: 48px; margin-bottom: 15px; }
```

**Examples:** "✅ 暂无数据异常预警", "暂无报表数据"

---

## 6. AI Components

### 6.1 Intelligent Features Overview

The platform's "智能" capability is expressed through these UI components:

| Component | Behavior | Page(s) |
|-----------|----------|---------|
| Anomaly Alert Table | Rule-based detection results with severity levels, drill-down to reports | `00-Experiment_overview` |
| Data Completeness Score | Auto-calculated % with color-coded progress bar | `00-Experiment_overview`, `03-DailyRecords` |
| Stage State Machine | Auto-tracking of experiment step progress with visual flow | `03-DailyRecords`, `04-StageDone`, `05-StageConfirm`, `09-ExperimentEnd` |
| Automated Report Dropdown | 8 pre-built reports generated from raw data | `00-Experiment_overview`, `10-AnalysisReport` |
| Product Guide Drawer | Intelligent documentation layer showing page purpose, value, users, features | `00-Experiment_overview` (via button) |

### 6.2 Anomaly Alert Component

```html
<el-table :data="alerts" border>
  <el-table-column prop="time" label="预警时间" />
  <el-table-column prop="experiment" label="实验编号" />
  <el-table-column prop="pen" label="栏位" />
  <el-table-column prop="type" label="异常类型">
    <!-- severity badge: low/medium/high -->
  </el-table-column>
  <el-table-column prop="description" label="异常描述" />
  <el-table-column label="操作">
    <el-button type="text" @click="handleAlert">查看详情</el-button>
  </el-table-column>
</el-table>
```

**Alert severity levels:** `high` (red, `#f56c6c`), `medium` (orange, `#e6a23c`), `low` (green, `#1ab394`).

### 6.3 Stage Flow Component

```html
<div class="flow-container">
  <div v-for="step in flowSteps" class="flow-item">
    <div :class="['flow-node', {
      completed: completedSteps.includes(step.id),
      active: currentStep === step.id,
      locked: !canAccessStep(step.id)
    }]">{{ step.name }}</div>
    <span v-if="!last" :class="['flow-arrow', { active: completed }]">→</span>
  </div>
</div>
```

**States:** `active` (brand bg, white text, glow), `completed` (light green bg, brand text/border), `locked` (muted, no interaction), `default` (neutral, hoverable).

### 6.4 Data Completeness Score

```
┌──────────────────────────────────┐
│ ████████████████░░░░  85%       │
│ progress bar (6px)   percentage │
└──────────────────────────────────┘
```

Color coding: ≥80% green (`#1ab394`), 50-79% orange (`#e6a23c`), <50% red (`#f56c6c`).

### 6.5 Automated Report Access

Dropdown menu with 8 report types accessible per experiment row:

| Icon | Report | Key |
|------|--------|-----|
| 📅 | 日报表 | `daily` |
| 📈 | 阶段报表 | `stage` |
| 📊 | 实验总结表 | `summary` |
| ⚰️ | 死淘明细表 | `death` |
| 💩 | 腹泻明细表 | `diarrhea` |
| 💊 | 药品疫苗明细表 | `medicine` |
| 🌡️ | 环控明细表 | `environment` |
| ⚖️ | 称重明细表 | `weight` |

### 6.6 Product Guide Drawer

Accessible via the "📖 Product Guide" button in the top navigation bar. Opens a 520px right-side drawer with expandable cards showing:

- Module purpose, business value, target users
- Key features (bullet list)
- Data sources
- Future roadmap

Visual distinction: Web pages have blue left border (`#3b82f6`), App pages have green left border (`#1ab394`).

---

## 7. Navigation

### 7.1 Layout Shell

```
┌──────────┬────────────────────────────────────────────┐
│ Sidebar  │ Top Nav (60px)                             │
│ (220px)  ├────────────────────────────────────────────┤
│ Fixed    │                                            │
│          │ Main Content                               │
│ Nav      │ margin-left: 220px; margin-top: 60px;      │
│          │ padding: 20px;                             │
│          │                                            │
└──────────┴────────────────────────────────────────────┘
```

### 7.2 Sidebar

```css
.sidebar {
  width: 220px;
  height: 100vh;
  position: fixed; left: 0; top: 0; z-index: 100;
  background: linear-gradient(180deg, #1e3a5f 0%, #2d5a87 100%);
  color: #fff;
}
```

**Structure:**
```
🔬 实验研发
─────────────────
📚 知识库              ▶
📋 项目管理            ▶
🏭 实验场              ▶
🐷 猪实验数据          ▶
   📊 实验概览         (active: #1ab394 bg)
   📈 报表分析
🐔 家禽实验数据        ▶
```

**Menu items:**
- Padding: `12px 20px`, font-size: `14px`
- Hover: `rgba(255,255,255,0.1)` background
- Active: `#1ab394` background, white text
- Sub-items: `padding-left: 50px`
- Active sub-item: `rgba(26,179,148,0.3)` background

### 7.3 Top Navigation Bar

```css
.top-nav {
  height: 60px;
  background-color: #fff;
  border-bottom: 1px solid #e6e6e6;
  position: fixed; top: 0; right: 0; left: 220px; z-index: 99;
  padding: 0 20px;
  display: flex; justify-content: space-between; align-items: center;
}
```

**Left side:** Breadcrumb navigation
```
实验研发 › 猪实验数据 › 实验概览
   13px       #999       #1ab394 (current)
```

**Right side:**
- Product Guide button: gradient green bg, white text, `📖` icon
- Language switch: `中文` button, white bg, `1px solid #ddd` border, `4px` radius
- User info: avatar circle (36px, `#1ab394` bg, white initials) + name (14px)

### 7.4 Breadcrumb

```css
.top-nav-breadcrumb {
  font-size: 13px; color: #999; margin-left: 15px;
  display: flex; align-items: center;
}
.top-nav-breadcrumb span { margin-right: 5px; }
/* Current page: color: #1ab394 */
```

### 7.5 Tab Navigation (Content)

```css
.tab-item {
  display: inline-block;
  padding: 10px 20px;
  cursor: pointer;
  font-size: 14px;
  color: #666;
  border-bottom: 2px solid transparent;
  margin-right: 10px;
  transition: all 0.3s;
}
.tab-item.active {
  color: #1ab394;
  border-bottom-color: #1ab394;
  font-weight: bold;
}
```

**Used in:** Daily Records (死淘/采食/环控/药品疫苗/腹泻/称重), Analysis Report tabs.

### 7.6 Treatment Group Tabs

```css
.treatment-tab {
  display: flex; gap: 10px; margin-bottom: 15px;
}
.treatment-tab button {
  padding: 8px 16px;
  border: 1px solid #ddd;
  background: #fff;
  border-radius: 4px;
  cursor: pointer;
  font-size: 13px;
}
.treatment-tab button.active {
  background: #1ab394;
  color: #fff;
  border-color: #1ab394;
}
```

### 7.7 Stage Tabs (Experiment End)

```css
.stage-tab {
  display: flex; gap: 10px; margin-bottom: 15px;
  padding-bottom: 15px; border-bottom: 1px solid #eee;
}
.stage-tab button {
  padding: 8px 20px;
  border: 1px solid #ddd;
  background: #fff;
  border-radius: 4px;
  cursor: pointer;
  font-size: 13px;
}
.stage-tab button.active {
  background: #1ab394;
  color: #fff;
  border-color: #1ab394;
}
```

### 7.8 Report Tabs (Analysis Page)

```css
.report-tab {
  padding: 10px 20px;
  font-size: 14px; color: #666;
  cursor: pointer;
  border-bottom: 2px solid transparent;
  margin-right: 10px;
  display: flex; align-items: center; gap: 8px;
  transition: all 0.3s;
}
.report-tab.active {
  color: #1ab394;
  border-bottom-color: #1ab394;
  font-weight: bold;
}
```

**8 Tabs:** 📅 日报表, 📈 阶段报表, 📊 实验总结表, ⚰️ 死淘明细表, 💩 腹泻明细表, 💊 药品疫苗明细表, 🌡️ 环控明细表, ⚖️ 称重明细表

---

## Appendix A: Form Patterns

### Form Grids

```css
.form-grid   { grid-template-columns: repeat(4, 1fr); }  /* 4-column */
.form-grid-3 { grid-template-columns: repeat(3, 1fr); }  /* 3-column */
.form-grid-2 { grid-template-columns: repeat(2, 1fr); }  /* 2-column */
```

### Form Item

```css
.form-item { display: flex; flex-direction: column; }
.form-item label { font-size: 13px; color: #666; margin-bottom: 6px; }
.form-item label.required::before { content: '*'; color: #f56c6c; margin-right: 4px; }
```

### Buttons

```css
/* Primary */
.el-button--primary { background-color: #1ab394; border-color: #1ab394; }
.el-button--primary:hover { background-color: #18a689; border-color: #18a689; }

/* Confirm / Submit */
.confirm-btn.confirm { background: #1ab394; color: #fff; }
.confirm-btn.confirm:hover { background: #17a689; }
.confirm-btn.confirm:disabled { background: #ccc; cursor: not-allowed; }

/* Back / Cancel */
.confirm-btn.back { background: #fff; color: #666; border: 1px solid #ddd; }
.confirm-btn.back:hover { background: #f5f5f5; }

/* Delete */
.delete-btn { background-color: #f56c6c; color: #fff; border-color: #f56c6c; }
.delete-btn:hover { background-color: #f44336; border-color: #f44336; }

/* Guide (special) */
.guide-btn {
  background: linear-gradient(135deg, #1ab394 0%, #10b981 100%);
  color: #fff; border: 1px solid #1ab394; border-radius: 6px;
}
.guide-btn:hover {
  background: linear-gradient(135deg, #159a7e 0%, #0d9e6e 100%);
  box-shadow: 0 2px 8px rgba(26,179,148,0.3);
}
```

## Appendix B: Component Inventory

| Page | Shared Components | Unique Components |
|------|------------------|-------------------|
| `00-Experiment_overview` | Sidebar, Top Nav, Search/Filters, Stats Grid, Table, Progress Bars | Anomaly Alert Table, Report Dropdown, Product Guide Button & Drawer |
| `01-Add_New` | Modal | Product Notes Panel, Form Grid |
| `02-Grouping` | Experiment Header, Status Flow, Info Grid | Treatment Group Table |
| `03-DailyRecords` | Experiment Header, Status Flow, Info Grid, Content Card, Tabs | Pen Info Box, Form Grid (2/3/4 cols), Record Tables, Collapse Sections, Upload Area, Edit Dialog, Query Modal |
| `06-DailyRecord2` | Same as 03-DailyRecords | Same (different stage context) |
| `04-StageDone` | Experiment Header, Status Flow, Info Grid, Content Card | Stage Summary Grid, Treatment Summary Cards, Confirm Buttons |
| `07-StageDone2` | Same as 04-StageDone | Same (different stage context) |
| `05-StageConfirm` | Experiment Header, Status Flow, Info Grid, Content Card | Stage Summary Cards (gradient), Treatment Tabs, Confirm/Back Buttons |
| `08-StageConfirm2` | Same as 05-StageConfirm | Same (different stage context) |
| `09-ExperimentEnd` | Experiment Header, Status Flow, Info Grid, Content Card | Stage Tabs, Treatment Tabs, Stage Summary Cards, Experiment Summary Grid, Report Modal |
| `10-AnalysisReport` | Sidebar, Top Nav, Search/Filters | Summary Cards (5 gradients), Report Tabs, Report Table, Chart Containers (Chart.js), Calendar Heatmap |
