# Enterprise Product Portfolio Portal — Design Specification

> **Version:** 1.0  
> **Status:** Design Phase  
> **Last Updated:** 2026-06-26  
> **Products Onboarded:** CPRI RD Swine (v1)  

---

## Table of Contents

1. [Overview](#1-overview)
2. [Information Architecture](#2-information-architecture)
3. [Navigation System](#3-navigation-system)
4. [Homepage](#4-homepage)
5. [Product Card](#5-product-card)
6. [Product Detail Page](#6-product-detail-page)
7. [Future Product Expansion](#7-future-product-expansion)
8. [Responsive Design](#8-responsive-design)
9. [File Structure](#9-file-structure)
10. [Component List](#10-component-list)

---

## 1. Overview

### 1.1 Purpose

The Enterprise Product Portfolio Portal is the **single entry point** for all CPRI (CP R&D Innovation) products. It provides a unified, enterprise-grade interface for browsing the product portfolio, accessing product documentation, launching live demos, and navigating into individual product workspaces.

### 1.2 Target Audience

| Role | Primary Need | Frequency |
|---|---|---|
| Internal stakeholders / leadership | Product portfolio overview, status at a glance | Weekly / monthly |
| Product team (PM, designer, dev) | Access prototypes, specs, design docs | Daily |
| QA / UX reviewers | Review prototypes, file review reports | Per sprint |
| Clients / external partners | Guided product demos | Ad-hoc (demo sessions) |
| New team members | Onboarding, understanding product landscape | On join |

### 1.3 Design Principles

| Principle | Description |
|---|---|
| **One entry, many doors** | Single URL serves the portfolio; each product has its own workspace accessible from here |
| **Enterprise-grade visual language** | Clean, professional, muted palette — instills trust and credibility |
| **Progressive disclosure** | Homepage shows product cards at a glance; click to reveal depth |
| **Product-agnostic shell** | Portal structure is independent of any single product — new products slot in without restructuring |
| **Static-first, no-build** | Works from a static file server or `file://`; no bundler, no CI pipeline required |
| **Responsive by default** | Full experience from 1920px down to 1024px; graceful degradation below |

### 1.4 Relationship to Existing Artifacts

```
Portal (this spec)
  └── Product: CPRI RD Swine
        ├── Demo Center (demo-center-design.md)
        │     ├── Web Prototypes (index-web.html → 00~10 .html)
        │     └── App Prototypes (index-app.html)
        ├── Product Spec (猪实验管理系统设计.md)
        ├── Product Brain (vision, user, journey, architecture, decision)
        ├── Web Nav Overview (web-nav-overview.html)
        └── App Nav Overview (app-nav-overview.html)
```

---

## 2. Information Architecture

### 2.1 Site Map

```
Portal Home (/)
├── Product Catalog
│   ├── CPRI RD Swine          ← v1 onboarded product
│   ├── [Product 2]            ← future
│   ├── [Product 3]            ← future
│   └── ...
├── Global Navigation
│   ├── Home
│   ├── Products
│   ├── About / Team
│   └── Settings
└── Utility
    ├── Search (cmd palette)
    ├── Theme toggle (future)
    └── Language toggle (future)
```

### 2.2 URL / Routing Scheme

| Route | View | Description |
|---|---|---|
| `/` or `/index.html` | Homepage | Product portfolio grid |
| `/product/swine/` | Product Detail: Swine | Swine product overview + deep links |
| `/product/swine/demo/` | Demo Center (redirect) | Launches the existing Demo Center |
| `/product/swine/spec/` | Product Spec | Renders 猪实验管理系统设计.md |
| `/product/swine/brain/` | Product Brain | Links to vision, user, journey docs |
| `/product/:id/` | Product Detail (generic) | Dynamic product detail page |
| `/search?q=` | Search results | Full-text search across products |

Hash-based routing (`#/product/swine`) for static hosting compatibility. Path-based routing (`/product/swine/`) when served from a web server.

### 2.3 Page Hierarchy

```
Level 0: Portal Home      — browse products, global nav
Level 1: Product Detail   — deep-dive into one product
Level 2: Product Tool     — Demo Center, Spec Viewer, Brain Viewer
```

The user can jump from Level 0 to Level 1 to Level 2, or navigate laterally between products at Level 1.

---

## 3. Navigation System

### 3.1 Global Top Header (56px, fixed)

```
┌──────────────────────────────────────────────────────────────────┐
│ [Logo]  CPRI Portfolio    Products ▾   About   🔍 Search  [⚙️]   │
└──────────────────────────────────────────────────────────────────┘
```

| Element | Position | Behavior |
|---|---|---|
| **Logo + Portal name** | Left | "CPRI" brandmark + "Portfolio" text. Click → Home. |
| **Products dropdown** | Left, after logo | Megamenu listing all products by category. Current product highlighted. |
| **About** | Left | Link to team / portal info page. |
| **Search (⌘K)** | Right | Opens command palette. Searches products, docs, prototypes by name/tag. |
| **Settings gear** | Right | Theme toggle (light/dark placeholder), language. |

**Visual:**
- Background: `#0f172a` (slate-900)
- Text: `#f1f5f9` (slate-100)
- Height: 56px
- Box-shadow: `0 1px 3px rgba(0,0,0,0.12)`
- Z-index: 1000

### 3.2 Products Megamenu

On hover/click of "Products" in the header, a dropdown panel appears:

```
┌────────────────────────────────────────────┐
│  PRODUCT CATEGORIES                        │
│                                            │
│  🧬 R&D Innovation                         │
│    ├─ 🐷 CPRI RD Swine      v2.3  Active  │
│    ├─ [Coming Soon]                        │
│                                            │
│  📊 Data & Analytics                       │
│    └─ [Coming Soon]                        │
│                                            │
│  ⚙️ Operations                             │
│    └─ [Coming Soon]                        │
└────────────────────────────────────────────┘
```

- Max 4 columns of categories
- Each product shows: icon + name + version + status badge
- "Coming Soon" slots shown as muted, non-interactive placeholders
- Clicking a product → navigates to its Product Detail page

### 3.3 Breadcrumb (Product Detail Page only)

```
Home  /  CPRI RD Swine  /  Demo Center
```

- Separator: `/` (forward slash)  
- Home and intermediate segments are clickable links
- Current page is plain text (not a link)

### 3.4 Keyboard Navigation

| Key | Action |
|---|---|
| `⌘K` / `Ctrl+K` | Open command palette / search |
| `⌘/` / `Ctrl+/` | Show keyboard shortcuts overlay |
| `Esc` | Close any open overlay / megamenu / palette |
| `←` `→` | Navigate between sibling products (on Product Detail page) |
| `Tab` | Standard focus traversal through interactive elements |

---

## 4. Homepage

### 4.1 Layout

```
┌──────────────────────────────────────────────────────────────┐
│  TOP HEADER (56px, fixed)                                    │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌──────────────────────────────────────────────────────────┐│
│  │  HERO BANNER                                             ││
│  │  CPRI Product Portfolio                                  ││
│  │  R&D Innovation Platform — from experiment to insight    ││
│  │  [Explore Products ↓]                                    ││
│  └──────────────────────────────────────────────────────────┘│
│                                                              │
│  ┌──────────────────────────────────────────────────────────┐│
│  │  PRODUCT CATALOG                          [Grid ▦] [List ☰] │
│  │                                                          ││
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐   ││
│  │  │ Product Card │  │ Product Card │  │  + Add New   │   ││
│  │  │ CPRI RD      │  │ [Coming      │  │  Product     │   ││
│  │  │ Swine        │  │  Soon]       │  │              │   ││
│  │  └──────────────┘  └──────────────┘  └──────────────┘   ││
│  │                                                          ││
│  └──────────────────────────────────────────────────────────┘│
│                                                              │
│  ┌──────────────────────────────────────────────────────────┐│
│  │  QUICK LINKS BAR                                         ││
│  │  [📋 Latest Specs]  [🎨 Prototypes]  [📊 Reports]  [📝 Notes] ││
│  └──────────────────────────────────────────────────────────┘│
│                                                              │
│  ┌──────────────────────────────────────────────────────────┐│
│  │  FOOTER  © 2026 CPRI. All rights reserved.              ││
│  └──────────────────────────────────────────────────────────┘│
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### 4.2 Hero Banner

- **Height:** 280px (desktop), 200px (tablet)
- **Background:** Gradient `#0f172a` → `#1e3a5f`, with subtle geometric pattern overlay
- **Heading:** "CPRI Product Portfolio" — 32px, weight 700, white
- **Subtitle:** "R&D Innovation Platform — from experiment to insight" — 16px, weight 400, `#94a3b8`
- **CTA Button:** "Explore Products ↓" — scrolls to the product catalog section below
- **Stats strip** (optional, at bottom edge of hero):
  - `3 Products` | `12 Prototypes` | `5 Team Members` | `Last updated: 2026-06-26`

### 4.3 Product Catalog Grid

- **Layout:** CSS Grid, 3 columns at ≥1280px, 2 columns at 1024–1279px, 1 column at <1024px
- **Gap:** 24px
- **Max width:** 1200px, centered
- **Section header:** "Products" on left, view toggle (grid/list icons) on right
- **Empty state:** If only 1 product exists, show it centered with a "More products coming soon" hint beside it
- **"Add Product" placeholder card:** Dashed border, `+` icon, muted text "Add New Product" — links to onboarding flow (future)

### 4.4 Quick Links Bar

A horizontal strip of shortcut links below the product grid:

| Link | Target | Icon |
|---|---|---|
| Latest Specs | `/product/swine/spec/` | 📋 |
| Prototypes | `/product/swine/demo/` | 🎨 |
| Reports | `/product/swine/report/` | 📊 |
| Release Notes | `/product/swine/notes/` | 📝 |

- Displayed as pill-shaped buttons in a flex row
- Only shows links that have content (hide empty ones)
- If multiple products exist, links are contextual to the last-viewed product

### 4.5 Footer

- Height: 48px
- Background: `#f8fafc`
- Border-top: 1px solid `#e2e8f0`
- Text: "© 2026 CPRI. All rights reserved." — 12px, `#94a3b8`, centered

---

## 5. Product Card

### 5.1 Card Anatomy

```
┌─────────────────────────────────────┐
│  ┌─────────────────────────────┐    │
│  │       PRODUCT ICON          │    │
│  │       (64×64 or SVG)        │    │
│  │                             │    │
│  │    CPRI RD Swine            │    │
│  │    猪实验数据管理系统         │    │
│  └─────────────────────────────┘    │
│                                     │
│  A dual-platform (Web + App)        │
│  experiment management system for   │
│  swine R&D. Covers full lifecycle   │
│  from experiment creation through   │
│  stage-based data collection to     │
│  analysis and reporting.            │
│                                     │
│  ┌─────────────────────────────┐    │
│  │  Tags                       │    │
│  │  [R&D] [Swine] [Dual-Platform] │ │
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │
│  │  Meta row                   │    │
│  │  v2.3  ● Active  12 proto   │    │
│  └─────────────────────────────┘    │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  [View Product →]             │  │
│  └───────────────────────────────┘  │
└─────────────────────────────────────┘
```

### 5.2 Card Elements

| Element | Description | Required |
|---|---|---|
| **Product Icon** | 64px × 64px. For Swine: a pig icon or custom SVG. Centered. | Yes |
| **Product Name** | Primary name in English. 18px, weight 700, `#0f172a`. | Yes |
| **Product Name (ZH)** | Chinese name below, 13px, weight 400, `#64748b`. | Optional |
| **Description** | 2–3 line summary. 13px, `#475569`. Max 160 chars. | Yes |
| **Tags** | 1–3 category tags as small pills. Background `#e0f2fe`, text `#0369a1`. | Optional |
| **Version** | Latest version number. Badge style. | Yes |
| **Status** | Status dot + text: Active / In Development / Maintenance / Archived. | Yes |
| **Prototype count** | e.g., "12 prototypes" — links to Demo Center. | Optional |
| **CTA Button** | "View Product →" — full-width button at card bottom. | Yes |

### 5.3 Card States

| State | Visual Treatment |
|---|---|
| **Default** | White background, subtle border, shadow `0 1px 3px rgba(0,0,0,0.06)` |
| **Hover** | Border color → `#2563eb`, shadow elevates to `0 4px 12px rgba(0,0,0,0.10)`, slight translateY(-2px) |
| **Active / Focus** | Blue ring outline (`#2563eb`), for keyboard focus |
| **Coming Soon** | Muted opacity (0.5), no hover effect, CTA reads "Coming Soon" (disabled), dashed border |
| **Archived** | Muted opacity (0.6), status badge reads "Archived", CTA reads "View Archive" |

### 5.4 Card Sizes

| Breakpoint | Cards per Row | Card Max Width |
|---|---|---|
| ≥ 1440px | 3 | 380px |
| 1280–1439px | 3 | 360px |
| 1024–1279px | 2 | 420px |
| < 1024px | 1 | 100% |

### 5.5 Data Schema (per product)

```json
{
  "id": "cpri-rd-swine",
  "name": "CPRI RD Swine",
  "nameZh": "猪实验数据管理系统",
  "category": "rnd-innovation",
  "description": "A dual-platform (Web + App) experiment management system for swine R&D...",
  "icon": "assets/icons/swine.svg",
  "thumbnail": "assets/thumbnails/swine-hero.png",
  "version": "2.3",
  "status": "active",
  "tags": ["R&D", "Swine", "Dual-Platform"],
  "prototypeCount": 12,
  "lastUpdated": "2026-06-26",
  "links": {
    "demo": "Product Brain/demo-center-design.html",
    "spec": "Product Brain/猪实验管理系统设计.md",
    "brain": "Product Brain/",
    "webOverview": "web-nav-overview.html",
    "appOverview": "app-nav-overview.html"
  }
}
```

---

## 6. Product Detail Page

### 6.1 Layout

```
┌──────────────────────────────────────────────────────────────┐
│  TOP HEADER (56px, fixed)                                    │
├──────────────────────────────────────────────────────────────┤
│  Breadcrumb: Home / CPRI RD Swine                            │
│                                                              │
│  ┌──────────────────────────────────────────────────────────┐│
│  │  PRODUCT HEADER                                          ││
│  │  [Icon] CPRI RD Swine           v2.3  ● Active           ││
│  │  猪实验数据管理系统                                       ││
│  │  Dual-platform experiment management for swine R&D       ││
│  │  [Launch Demo]  [View Spec]  [Product Brain]             ││
│  └──────────────────────────────────────────────────────────┘│
│                                                              │
│  ┌────────────────────┐  ┌──────────────────────────────────┐│
│  │  QUICK STATS       │  │  PRODUCT OVERVIEW                ││
│  │                    │  │                                  ││
│  │  12 Prototypes     │  │  Multi-line description of the   ││
│  │  2 Platforms       │  │  product, its purpose, key       ││
│  │  11 Web Pages      │  │  features, and target users.     ││
│  │  5 App Screens     │  │                                  ││
│  │  3 Roles           │  │  Tags: [R&D] [Swine] [Dual-Plat] ││
│  │                    │  │                                  ││
│  └────────────────────┘  └──────────────────────────────────┘│
│                                                              │
│  ┌──────────────────────────────────────────────────────────┐│
│  │  LAUNCHPAD — Quick Actions                               ││
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐   ││
│  │  │ 🎨 Demo  │ │ 📋 Spec  │ │ 🧠 Brain │ │ 🌐 Web   │   ││
│  │  │ Center  │ │ Document │ │  Docs    │ │ Overview │   ││
│  │  └──────────┘ └──────────┘ └──────────┘ └──────────┘   ││
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐   ││
│  │  │ 📱 App   │ │ 📊 Report│ │ 📝 Notes │ │ ⚙️ Config │   ││
│  │  │ Overview │ │          │ │          │ │          │   ││
│  │  └──────────┘ └──────────┘ └──────────┘ └──────────┘   ││
│  └──────────────────────────────────────────────────────────┘│
│                                                              │
│  ┌──────────────────────────────────────────────────────────┐│
│  │  PROTOTYPE PREVIEW STRIP                                 ││
│  │  ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐  → scroll     ││
│  │  │ 00  │ │ 01  │ │ 02  │ │ 03  │ │ 04  │               ││
│  │  └─────┘ └─────┘ └─────┘ └─────┘ └─────┘               ││
│  └──────────────────────────────────────────────────────────┘│
│                                                              │
│  ┌──────────────────────────────────────────────────────────┐│
│  │  TIMELINE / ACTIVITY                                      ││
│  │  Jun 26 — v2.3 released                                   ││
│  │  Jun 24 — App nav overview added                          ││
│  │  Jun 20 — Web nav overview added                          ││
│  └──────────────────────────────────────────────────────────┘│
│                                                              │
├──────────────────────────────────────────────────────────────┤
│  FOOTER                                                       │
└──────────────────────────────────────────────────────────────┘
```

### 6.2 Product Header

- **Icon:** 80px × 80px, left-aligned
- **Name:** 28px, weight 700
- **Chinese name:** 16px, `#64748b`, below the English name
- **Description:** One-line tagline, 14px, `#475569`
- **Status badge + version:** Right side of header
- **CTA Buttons:** Row of secondary buttons: "Launch Demo", "View Spec", "Product Brain"

### 6.3 Quick Stats Panel

A compact sidebar panel showing key metrics:

| Stat | Value for Swine | Icon |
|---|---|---|
| Prototypes | 12 | 🎨 |
| Platforms | 2 (Web + App) | 🖥️📱 |
| Web Pages | 11 | 🌐 |
| App Screens | 5 | 📱 |
| User Roles | 3 | 👥 |
| Last Updated | 2026-06-26 | 📅 |

### 6.4 Launchpad — Quick Action Grid

An 8-slot grid of action cards. Each card is a clickable tile that navigates to a specific resource:

| Slot | Label | Target | Icon |
|---|---|---|---|
| 1 | Demo Center | `/product/swine/demo/` | 🎨 |
| 2 | Spec Document | `/product/swine/spec/` | 📋 |
| 3 | Product Brain | `/product/swine/brain/` | 🧠 |
| 4 | Web Overview | `web-nav-overview.html` | 🌐 |
| 5 | App Overview | `app-nav-overview.html` | 📱 |
| 6 | Review Report | `/product/swine/report/` | 📊 |
| 7 | Release Notes | `/product/swine/notes/` | 📝 |
| 8 | Configuration | (future) | ⚙️ |

- **Layout:** CSS Grid, 4 columns → 3 → 2 responsive
- **Card size:** 120px × 100px
- **Hover:** Border highlight, slight scale
- **Empty state:** If a target doesn't exist yet, show the card as muted with "(Coming Soon)" subtitle

### 6.5 Prototype Preview Strip

A horizontally scrollable thumbnail strip showing all prototypes for this product:

- Each thumbnail: 160px × 100px, with prototype name below
- Clicking a thumbnail → opens that prototype in the Demo Center
- Shows a subset (first 6), with "View all 12 →" link at the end
- Background: light gray track with subtle inner shadow for scroll affordance

### 6.6 Activity Timeline

Chronological list of recent updates for this product:

- Each entry: date, version/event, one-line description
- Most recent 5 entries shown by default
- "View full changelog →" link to Release Notes
- Icons: 🆕 for new, 🔧 for changed, 🐛 for fixed

### 6.7 Empty State (for products with no data yet)

```
┌──────────────────────────────────────────┐
│                                          │
│         🧬                               │
│    Product Created                       │
│    Start adding prototypes and docs      │
│                                          │
│    [Add First Prototype]  [Write Spec]   │
│                                          │
└──────────────────────────────────────────┘
```

---

## 7. Future Product Expansion

### 7.1 Adding a New Product

When a second product is ready to be onboarded:

**Step 1 — Add to product manifest:**
```json
// products.json — append new entry
{
  "id": "cpri-aqua-feed",
  "name": "CPRI RD Aqua Feed",
  "nameZh": "水产饲料实验系统",
  "category": "rnd-innovation",
  "status": "in-development",
  ...
}
```

**Step 2 — Create product directory:**
```
原型test1/
├── products/
│   ├── swine/           ← existing
│   │   ├── demo/
│   │   ├── specs/
│   │   └── brain/
│   └── aqua-feed/       ← new
│       ├── demo/
│       ├── specs/
│       └── brain/
```

**Step 3 — Add icon and thumbnail assets.**  
**Step 4 — Verify product card renders on homepage.**  
**Step 5 — Fill in detail page resources incrementally.**

No portal code changes needed — the manifest drives everything.

### 7.2 Product Categories (Future)

| Category | Description | Example Products |
|---|---|---|
| **R&D Innovation** | Experiment management, research data pipelines | Swine, Aqua Feed, Poultry |
| **Data & Analytics** | Dashboards, BI, reporting tools | Analytics Dashboard, Report Builder |
| **Operations** | Farm ops, supply chain, inventory | Farm Manager, Feed Tracker |
| **Platform** | Shared infrastructure, auth, design system | Design System, API Gateway |

### 7.3 Portal Evolution Roadmap

```
Phase 1 (Current)        Phase 2                  Phase 3
│                        │                        │
│  Single product        │  2–3 products          │  5+ products
│  Static JSON manifest  │  Same manifest model   │  Optional: headless CMS
│  Grid of card(s)       │  Category sections     │  Search + filtering
│  Basic detail page     │  Cross-product linking  │  Personalized dashboard
│  Hash routing          │  Path-based routing     │  User auth + roles
│  No build              │  No build               │  Optional static gen
```

### 7.4 Manifest-Driven Architecture

The portal is driven by a single `products.json` manifest. Adding a product is a data change, not a code change:

```
products.json  ──→  Homepage renders product cards
               ──→  Product Detail page renders from product data
               ──→  Navigation megamenu populates from categories
               ──→  Search index built from product names, tags, descriptions
```

This ensures the portal scales linearly — 1 product or 50 products, the same shell serves them all.

---

## 8. Responsive Design

### 8.1 Breakpoints

| Breakpoint | Designation | Layout |
|---|---|---|
| ≥ 1440px | Large Desktop | Full layout; 3-column product grid; hero at full height (280px) |
| 1280–1439px | Desktop | Full layout; 3-column grid (tighter); hero at 240px |
| 1024–1279px | Small Desktop / Landscape Tablet | 2-column product grid; product detail stacks vertically; header condensed |
| 768–1023px | Tablet | 1-column product grid; product detail fully stacked; quick actions grid: 3 cols |
| < 768px | Mobile (not primary target) | Single column; hero minimal (160px); nav as hamburger drawer; footer simplified |

### 8.2 Breakpoint-Specific Behaviors

**≥ 1280px:**
- Product Detail page: two-column layout (stats sidebar + main content)
- Quick action grid: 4 columns

**1024–1279px:**
- Product Detail page: stats sidebar moves above main content as a horizontal strip
- Quick action grid: 3 columns
- Prototype preview strip: smaller thumbnails (120px × 75px)

**768–1023px:**
- Product Detail page: single-column stacked
- Quick action grid: 2 columns
- Header: logo remains, nav links collapse into hamburger menu
- Product card: full width

**< 768px (minimum support):**
- Header: 48px height, hamburger menu
- Hero: 160px, smaller heading (24px)
- Product card: edge-to-edge with 16px margin
- Quick action grid: 2 columns, smaller tiles (80px)
- Breadcrumb hidden
- "Not optimized for mobile — use a larger screen for the full experience" banner

### 8.3 Responsive Navigation

| Breakpoint | Navigation Mode |
|---|---|
| ≥ 1024px | Full top header with visible nav links + megamenu |
| < 1024px | Hamburger icon → slide-out drawer from left (overlay) |

The drawer contains all nav items stacked vertically, with accordions for categories. It closes on:
- Selecting a navigation target
- Clicking the overlay backdrop
- Pressing `Esc`

### 8.4 Responsive Typography

| Element | ≥ 1280px | 768–1279px | < 768px |
|---|---|---|---|
| Hero heading | 32px | 28px | 24px |
| Hero subtitle | 16px | 14px | 13px |
| Product card title | 18px | 16px | 16px |
| Section headers | 20px | 18px | 16px |
| Body text | 14px | 13px | 13px |

---

## 9. File Structure

### 9.1 Target Directory Layout

```
原型test1/
│
├── index.html                          # Portal entry point (HOME)
├── products.json                       # Product manifest (single source of truth)
├── README.md                           # Dev setup notes
│
├── docs/
│   └── portal-spec.md                  # This document
│
├── assets/
│   ├── css/
│   │   └── portal.css                  # All portal styles
│   ├── js/
│   │   ├── portal.js                   # App shell, routing, manifest loader
│   │   ├── components.js               # Reusable component definitions
│   │   └── search.js                   # Client-side search index
│   ├── icons/
│   │   ├── swine.svg                   # Product-specific icons
│   │   └── placeholder.svg             # Default icon for products without one
│   └── thumbnails/
│       ├── swine-hero.png              # Product hero thumbnail
│       └── prototype-thumbs/           # Prototype preview thumbs (future)
│
├── products/
│   └── swine/
│       ├── demo/                       # Demo Center files (from demo-center-design.md)
│       │   ├── index.html
│       │   ├── prototypes.json
│       │   ├── css/
│       │   ├── js/
│       │   └── content/
│       ├── specs/
│       │   └── 猪实验管理系统设计.md    # Product specification
│       ├── brain/                      # Product Brain documents
│       │   ├── 1. vision.html
│       │   ├── 2. user.html
│       │   ├── 3. journey.html
│       │   ├── 4. architecture.html
│       │   └── 5. decision.html
│       ├── prototypes/                 # Actual prototype HTML files
│       │   ├── 00-Experiment_overview.html
│       │   ├── 01-Add_New.html
│       │   ├── ... (02–10)
│       │   ├── index-web.html
│       │   ├── index-app.html
│       │   ├── web-nav-overview.html
│       │   └── app-nav-overview.html
│       └── README.md                   # Swine product README
│
├── Product Brain/                      # (keep existing top-level for now)
├── OOO/                                # (keep existing)
└── [existing prototype files]          # (gradually migrate into products/swine/)
```

### 9.2 Migration Path

**Phase 1 (current state):** Portal `index.html` reads `products.json`. Product paths point to existing files at their current locations. No file moving needed.

**Phase 2 (gradual):** As each product matures, move its files into `products/:id/` subdirectories. Update paths in `products.json`.

**Phase 3 (clean):** All products in `products/`. Top-level only contains portal files + shared assets.

### 9.3 File Naming Conventions

| Type | Convention | Example |
|---|---|---|
| Portal pages | `kebab-case.html` | `index.html` |
| Product directories | `kebab-case/` | `cpri-rd-swine/` |
| Assets | `kebab-case.ext` | `swine-hero.png` |
| Config / data | `kebab-case.json` | `products.json` |
| Documentation | `kebab-case.md` | `portal-spec.md` |
| Chinese docs | Keep original names or use `kebab-case-zh.md` | `swine-spec-zh.md` |

---

## 10. Component List

### 10.1 Component Hierarchy

```
Portal App
├── GlobalHeader
│   ├── Logo
│   ├── NavLinks
│   │   ├── NavLink (Home)
│   │   ├── NavLink (Products) → ProductsMegaMenu
│   │   │   ├── MegaMenuCategory[]
│   │   │   │   └── MegaMenuItem[] (per product)
│   │   │   └── MegaMenuFooter ("View All Products →")
│   │   └── NavLink (About)
│   ├── SearchTrigger (⌘K)
│   └── SettingsTrigger
│
├── PageRouter (hash-based)
│   │
│   ├── [Route: /] HomePage
│   │   ├── HeroBanner
│   │   │   ├── HeroHeading
│   │   │   ├── HeroSubtitle
│   │   │   ├── HeroCTA
│   │   │   └── HeroStatsStrip
│   │   ├── ProductCatalog
│   │   │   ├── CatalogHeader (title + view toggle)
│   │   │   ├── ProductCard[] (one per product in manifest)
│   │   │   └── AddProductPlaceholder
│   │   ├── QuickLinksBar
│   │   │   └── QuickLinkPill[]
│   │   └── Footer
│   │
│   ├── [Route: /product/:id] ProductDetailPage
│   │   ├── Breadcrumb
│   │   ├── ProductHeader
│   │   │   ├── ProductIcon
│   │   │   ├── ProductTitles
│   │   │   ├── StatusBadge
│   │   │   └── HeaderCTAs
│   │   ├── QuickStatsPanel
│   │   │   └── StatItem[]
│   │   ├── ProductDescription
│   │   ├── TagList
│   │   │   └── TagPill[]
│   │   ├── LaunchpadGrid
│   │   │   └── ActionCard[] (8 slots)
│   │   ├── PrototypePreviewStrip
│   │   │   ├── PrototypeThumbnail[]
│   │   │   └── ViewAllLink
│   │   ├── ActivityTimeline
│   │   │   └── TimelineEntry[]
│   │   └── EmptyState (conditional)
│   │
│   └── [Route: /search] SearchResults
│       ├── SearchInput
│       ├── SearchResultList
│       │   └── SearchResultItem[]
│       └── NoResults
│
├── CommandPalette (overlay, ⌘K)
│   ├── SearchInput
│   └── ResultList
│       └── PaletteResultItem[]
│
├── HamburgerDrawer (mobile nav, < 1024px)
│   ├── DrawerOverlay
│   └── DrawerContent
│       └── NavAccordion[]
│
└── ToastContainer (notifications)
    └── Toast[]
```

### 10.2 Component Inventory

#### Shell Components

| Component | Description | Reusable? |
|---|---|---|
| `GlobalHeader` | Fixed 56px top bar with logo, nav, search, settings | Yes — shared across all pages |
| `Footer` | 48px footer with copyright | Yes — shared across all pages |
| `PageRouter` | Hash-based SPA router. Reads URL, mounts the correct page component | Yes — core shell |
| `Breadcrumb` | `Home / Product / Page` navigation trail | Yes — used on detail pages |
| `ToastContainer` | Fixed-position toast notification layer | Yes — global |

#### Homepage Components

| Component | Description |
|---|---|
| `HeroBanner` | Gradient hero with heading, subtitle, CTA, stats strip |
| `HeroStatsStrip` | Optional stats row at bottom of hero |
| `ProductCatalog` | Grid container for product cards |
| `CatalogHeader` | Section title + grid/list toggle |
| `ProductCard` | Individual product card (see Section 5) |
| `AddProductPlaceholder` | Dashed-border card for adding future products |
| `QuickLinksBar` | Horizontal row of quick-link pills |
| `QuickLinkPill` | Individual pill-shaped shortcut link |

#### Product Detail Components

| Component | Description |
|---|---|
| `ProductHeader` | Product icon, name, description, status, CTA buttons |
| `ProductIcon` | 80px product icon with fallback |
| `StatusBadge` | Colored badge: Active / In Development / Maintenance / Archived |
| `QuickStatsPanel` | Sidebar panel with key stat items |
| `StatItem` | Single stat: icon + number + label |
| `ProductDescription` | Multi-paragraph product overview |
| `TagList` / `TagPill` | Horizontal tag row; individual tag pill |
| `LaunchpadGrid` | Grid of action cards |
| `ActionCard` | Single clickable action tile (icon + label + subtitle) |
| `PrototypePreviewStrip` | Horizontally scrollable thumbnail strip |
| `PrototypeThumbnail` | Individual prototype preview thumb (image + name) |
| `ActivityTimeline` | Chronological activity log |
| `TimelineEntry` | Single timeline row: date + event + description |
| `EmptyState` | Centered empty state with icon, message, CTA buttons |

#### Navigation Components

| Component | Description |
|---|---|
| `NavLinks` | Horizontal list of top-level nav links |
| `NavLink` | Single nav link with optional dropdown |
| `ProductsMegaMenu` | Dropdown megamenu showing product categories |
| `MegaMenuCategory` | Category section within the megamenu |
| `MegaMenuItem` | Individual product row in the megamenu |
| `HamburgerDrawer` | Mobile slide-out navigation drawer |
| `DrawerOverlay` | Semi-transparent backdrop behind the drawer |
| `DrawerContent` | Scrollable drawer content with nav items |
| `NavAccordion` | Expandable nav section in the drawer |

#### Utility Components

| Component | Description |
|---|---|
| `CommandPalette` | ⌘K search overlay with input and results |
| `SearchInput` | Text input with icon, used in palette and search page |
| `SearchResults` | Full search results page |
| `SearchResultItem` | Single search result row |
| `NoResults` | "No results found" empty state |
| `ViewToggle` | Grid/List icon toggle for product catalog |
| `SkeletonCard` | Loading placeholder with shimmer animation |
| `SkeletonDetail` | Loading placeholder for product detail page |
| `ErrorBoundary` | Catches rendering errors, shows fallback UI |
| `KeyboardShortcuts` | Overlay listing all keyboard shortcuts |

### 10.3 Component States

Every interactive component supports these states where applicable:

| State | Description |
|---|---|
| **Default** | Normal resting state |
| **Hover** | Mouse pointer over the element |
| **Focus** | Keyboard-focused (visible ring) |
| **Active** | Being pressed / clicked |
| **Loading** | Data not yet available (skeleton / spinner) |
| **Empty** | Data loaded but no results |
| **Error** | Data failed to load |
| **Disabled** | Not interactive (e.g., "Coming Soon" card) |

### 10.4 Reusable Design Tokens

| Token | Value | Usage |
|---|---|---|
| `--color-primary` | `#2563eb` | Accent, links, active states |
| `--color-header-bg` | `#0f172a` | Global header background |
| `--color-surface` | `#ffffff` | Cards, content areas |
| `--color-bg` | `#f8fafc` | Page background |
| `--color-text-primary` | `#0f172a` | Headings, body |
| `--color-text-secondary` | `#475569` | Descriptions |
| `--color-text-muted` | `#94a3b8` | Captions, metadata |
| `--color-border` | `#e2e8f0` | Card borders, dividers |
| `--color-success` | `#16a34a` | Active status, success |
| `--color-warning` | `#ca8a04` | In Development status |
| `--color-error` | `#dc2626` | Error states |
| `--header-height` | `56px` | Global header, position offsets |
| `--card-radius` | `12px` | Product cards, panels |
| `--transition-standard` | `200ms ease` | Hover effects, toggles |
| `--shadow-card` | `0 1px 3px rgba(0,0,0,0.06)` | Default card shadow |
| `--shadow-card-hover` | `0 4px 12px rgba(0,0,0,0.10)` | Card hover shadow |
| `--font-family` | `"Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif` | All text |

---

## Appendix A: CPRI RD Swine — Product Card Data Reference

For implementing the first product card, here is the complete data:

```json
{
  "id": "cpri-rd-swine",
  "name": "CPRI RD Swine",
  "nameZh": "猪实验数据管理系统",
  "category": "rnd-innovation",
  "description": "Dual-platform (Web + App) experiment management system for swine R&D. Covers the full lifecycle: experiment creation, grouping, stage-based daily data collection, stage review & archive, experiment conclusion, and analysis reporting.",
  "icon": "assets/icons/swine.svg",
  "thumbnail": "assets/thumbnails/swine-hero.png",
  "version": "2.3",
  "status": "active",
  "tags": ["R&D", "Swine", "Dual-Platform"],
  "prototypeCount": 12,
  "platforms": ["Web", "App"],
  "roles": ["博士 (Researcher)", "场长 (Farm Manager)", "技术员 (Technician)"],
  "lastUpdated": "2026-06-26",
  "links": {
    "demo": "Product Brain/demo-center-design.html",
    "spec": "Product Brain/猪实验管理系统设计.md",
    "brain": "Product Brain/",
    "webOverview": "web-nav-overview.html",
    "appOverview": "app-nav-overview.html",
    "report": null,
    "notes": null
  },
  "activity": [
    { "date": "2026-06-26", "event": "Portal design spec created", "type": "doc" },
    { "date": "2026-06-26", "event": "Web navigation overview added", "type": "feature" },
    { "date": "2026-06-24", "event": "App navigation overview added", "type": "feature" },
    { "date": "2026-06-20", "event": "Demo Center design spec created", "type": "doc" },
    { "date": "2026-06-11", "event": "Product Brain documents completed", "type": "doc" }
  ]
}
```

---

## Appendix B: Visual Style Reference

### Color Palette

| Role | Hex | Tailwind | Usage |
|---|---|---|---|
| Primary | `#2563eb` | blue-600 | Links, active states, CTA buttons |
| Header bg | `#0f172a` | slate-900 | Global header |
| Page bg | `#f8fafc` | slate-50 | Page background |
| Surface | `#ffffff` | white | Cards, panels |
| Text primary | `#0f172a` | slate-900 | Headings |
| Text secondary | `#475569` | slate-600 | Body, descriptions |
| Text muted | `#94a3b8` | slate-400 | Metadata, captions |
| Border | `#e2e8f0` | slate-200 | Card borders, dividers |
| Success | `#16a34a` | green-600 | Active status |
| Warning | `#ca8a04` | yellow-600 | In Development status |
| Info | `#0369a1` | sky-700 | Tag backgrounds |

### Typography Scale

| Level | Size | Weight | Usage |
|---|---|---|---|
| Display | 32px | 700 | Hero heading |
| H1 | 28px | 700 | Product name (detail page) |
| H2 | 20px | 600 | Section headers |
| H3 | 18px | 700 | Product card title |
| H4 | 16px | 600 | Card section headers |
| Body | 14px | 400 | Descriptions, paragraphs |
| Body-sm | 13px | 400 | Secondary text, card descriptions |
| Caption | 12px | 400 | Meta info, breadcrumbs, footer |
| Caption-xs | 11px | 500 | Tags, badges |

---

## Appendix C: Cross-Reference Map

This document should be read alongside:

| Document | Relationship |
|---|---|
| `Product Brain/demo-center-design.md` | The Demo Center is the prototype preview engine launched from the Product Detail page |
| `Product Brain/猪实验管理系统设计.md` | The full product spec for CPRI RD Swine — linked from the Product Detail page |
| `web-nav-overview.html` | Visual overview of all Web prototype pages — linked from the Launchpad |
| `app-nav-overview.html` | Visual overview of all App prototype screens — linked from the Launchpad |
| `Product Brain/1. vision.html` through `5. decision.html` | Product Brain documents — linked from the Launchpad |
