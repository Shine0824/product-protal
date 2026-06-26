# Product Demo Center — Design Specification

---

## 1. Overview

The Product Demo Center is an internal portal that serves as a single entry point for browsing, previewing, and reviewing all product prototypes (Web & App). It provides a structured navigation experience with supporting documentation (Product Guide, Review Report, Release Notes) displayed alongside live iframe previews.

**Target audience:** Internal stakeholders, product team, QA, UX reviewers, and clients during demo sessions.

**Design principles:**
- Enterprise-grade visual consistency (clean, professional, muted palette)
- Fast orientation — left-nav tree + top header breadcrumb
- Zero-friction preview — iframe sandbox with device frame toggle
- Responsive from 1920px down to 1024px (no mobile target; internal tool)

---

## 2. Information Architecture

```
Demo Center
├── Web Prototypes
│   ├── Experiment Overview
│   ├── Add New Record
│   ├── Grouping
│   ├── Daily Records
│   ├── Stage Done
│   ├── Stage Confirm
│   ├── Experiment End
│   └── Analysis Report
├── App Prototypes
│   ├── App Navigation Overview
│   └── App Index
├── Product Guide
├── Review Report
└── Release Notes
```

---

## 3. Page Layout

```
┌──────────────────────────────────────────────────────────────┐
│  TOP HEADER (fixed, 56px)                            [⚙] [👤] │
├────────────┬─────────────────────────────────────────────────┤
│            │                                                 │
│  LEFT NAV  │           CONTENT AREA                          │
│  (240px)   │  ┌─────────────────────────────────────────┐    │
│            │  │  BREADCRUMB + TOOLBAR                    │    │
│  ◉ Web     │  ├─────────────────────────────────────────┤    │
│    ├─ Ovw  │  │                                         │    │
│    ├─ Add  │  │         IFRAME PREVIEW                  │    │
│    ├─ Grp  │  │         (fills remaining height)        │    │
│    ├─ ...  │  │                                         │    │
│  ◉ App     │  │                                         │    │
│    ├─ Nav  │  │                                         │    │
│    └─ Idx  │  │                                         │    │
│  · Guide   │  │                                         │    │
│  · Report  │  │                                         │    │
│  · Notes   │  └─────────────────────────────────────────┘    │
│            │                                                 │
├────────────┴─────────────────────────────────────────────────┤
│  STATUS BAR (optional, 24px)  "Prototype v2.3  |  Last sync" │
└──────────────────────────────────────────────────────────────┘
```

### 3.1 Top Header (56px fixed)

| Element | Position | Notes |
|---|---|---|
| Logo / Product name | Left, 16px padding | "Product Demo Center" or company logo |
| Breadcrumb | Center-left | `Home > Web Prototypes > Experiment Overview` |
| Device toggle | Right group | [Desktop] [Tablet] [Mobile] — switches iframe width |
| New-tab link | Right group | Opens prototype in new tab |
| Settings gear | Far right | Theme toggle, layout density |

Background: `#1e293b` (slate-800), text: `#f8fafc`, height: 56px.

### 3.2 Left Navigation (240px, collapsible to 64px)

Tree-structure sidebar with three sections:

**Section 1 — Prototypes (collapsible accordion)**
- **Web Prototypes** (folder icon, expandable)
  - Each prototype as a leaf node (file icon)
- **App Prototypes** (folder icon, expandable)
  - Each prototype as a leaf node (phone icon)

**Section 2 — Documentation (static links)**
- Product Guide (book icon)
- Review Report (clipboard icon)
- Release Notes (tag icon)

**Behavior:**
- Active item highlighted with accent left-border (3px, `#3b82f6`)
- Collapse toggle at bottom: hamburger → icons only (64px)
- Section accordions remember open/closed state in sessionStorage
- Selected prototype name appears in top-header breadcrumb

**Visual:**
- Background: `#f8fafc`
- Active item background: `#e0f2fe` with blue left-border
- Hover: `#f1f5f9`
- Typography: 14px, `#334155`, weight 400; section headers weight 600, uppercase, 11px, letter-spacing 0.05em

### 3.3 Content Area — iframe Preview

The content area is split vertically when a documentation item is selected:

- **Prototype selected:** iframe fills the entire content area
- **Documentation selected:** split view — rendered markdown on left, related prototype iframe on right (60/40 or collapsible)

**Toolbar (48px, above iframe):**

| Control | Purpose |
|---|---|
| Breadcrumb | Mirrors header, or shows selected path |
| Device frame toggle | [💻 Desktop 100%] [📱 Tablet 768px] [📱 Mobile 375px] — sets the iframe container width, centered |
| Zoom slider | 50%–150% (when not using device presets) |
| Rotate button | Swap width/height (useful for landscape mobile preview) |
| Open in new tab | `target="_blank"` link |
| Refresh | Reload iframe |

**iframe container:**
- White background, centered in the content area
- Subtle box-shadow when using device frame mode (simulates device bezel)
- `border: none` with `border-radius: 8px` for desktop; `border-radius: 24px` for mobile frame
- The iframe `src` is loaded from a local URL map (relative paths to HTML files)
- Sandbox attributes: `allow-scripts allow-same-origin`

### 3.4 Status Bar (24px, optional)

Right-aligned metadata: prototype filename, last-modified date, version tag.

---

## 4. Responsive Breakpoints

| Breakpoint | Layout |
|---|---|
| ≥ 1440px | Full layout: 240px nav + content + optional right panel |
| 1280–1439px | Left nav collapses to 64px (icons only) |
| 1024–1279px | Left nav hidden by default, hamburger overlay toggle; top header condenses |
| < 1024px | Single-column stack: header → content (nav as overlay drawer). Minimum supported; not optimized for mobile. |

Nav collapse behavior: clicking the hamburger/chevron at the bottom of the sidebar toggles between 240px and 64px. At 64px, only icons are visible; hovering over an icon shows a tooltip with the full label.

---

## 5. Page / View Specifications

### 5.1 Web Prototype View

- **URL scheme:** `/demo/web/:prototypeId`
- **Data source:** `prototypes.json` or inline config array
- Each prototype entry:
  ```json
  {
    "id": "experiment-overview",
    "name": "Experiment Overview",
    "category": "web",
    "path": "00-Experiment_overview.html",
    "thumbnail": "thumbnails/exp-overview.png",
    "version": "2.3",
    "lastUpdated": "2026-06-20"
  }
  ```
- The iframe loads the file from a local relative path
- The left-nav highlights the active prototype
- Breadcrumb updates: `Home > Web Prototypes > Experiment Overview`

### 5.2 App Prototype View

- **URL scheme:** `/demo/app/:prototypeId`
- Same structure as Web but renders inside a **device frame** by default
- Default device preset: Mobile (375×812)
- App prototypes render `index-app.html` and related files
- Device bezel rendered via CSS (border-radius + box-shadow), not an image asset

### 5.3 Product Guide View

- **URL scheme:** `/demo/guide`
- Content area shows rendered documentation (Markdown or structured HTML)
- Optional: right-side mini-preview of the currently discussed prototype
- Sections: Getting Started, Feature Overview, Workflows, FAQ
- Table of contents on the right (sticky, 200px) for quick section jump

### 5.4 Review Report View

- **URL scheme:** `/demo/report`
- Displays a structured review report:
  - Review date, reviewer, status (Approved / Changes Requested / In Review)
  - Per-screen comments with screenshot references
  - Action items checklist
- Linked prototypes open in split view: report on left, prototype on right
- Export to PDF placeholder (future)

### 5.5 Release Notes View

- **URL scheme:** `/demo/notes`
- Chronological list of release entries, grouped by version
- Each entry: version number, date, change type (Added / Changed / Fixed), description
- Tag-based filter: All / Feature / Fix / Breaking
- Version selector dropdown to jump to a specific release

---

## 6. Component Tree

```
App
├── TopHeader
│   ├── Logo
│   ├── Breadcrumb
│   └── HeaderActions (device toggle, open-tab, settings)
├── LayoutShell
│   ├── LeftNav
│   │   ├── NavSection (Prototypes)
│   │   │   ├── NavFolder (Web, expandable)
│   │   │   │   └── NavItem[] (each prototype)
│   │   │   └── NavFolder (App, expandable)
│   │   │       └── NavItem[] (each prototype)
│   │   ├── NavDivider
│   │   ├── NavSection (Documentation)
│   │   │   ├── NavItem (Product Guide)
│   │   │   ├── NavItem (Review Report)
│   │   │   └── NavItem (Release Notes)
│   │   └── CollapseToggle
│   └── ContentArea
│       ├── PreviewToolbar
│       │   ├── Breadcrumb
│       │   ├── DeviceFrameToggle
│       │   ├── ZoomSlider
│       │   ├── RotateButton
│       │   ├── OpenTabButton
│       │   └── RefreshButton
│       ├── IframePreview
│       │   └── DeviceFrame (conditional)
│       ├── MarkdownViewer (for Guide / Report / Notes)
│       └── SplitPanel (documentation + prototype side-by-side)
└── StatusBar
```

---

## 7. State Design

### 7.1 Navigation State

```ts
interface NavState {
  selectedItemId: string;           // currently active nav item
  expandedFolders: string[];        // which accordion folders are open
  sidebarCollapsed: boolean;        // 240px vs 64px
  mobileDrawerOpen: boolean;        // overlay nav on small screens
}
```

### 7.2 Preview State

```ts
interface PreviewState {
  prototypeId: string | null;       // active prototype (null when on doc page)
  devicePreset: 'desktop' | 'tablet' | 'mobile' | 'auto';
  zoom: number;                     // 0.5 – 1.5
  orientation: 'portrait' | 'landscape';
  splitView: boolean;               // doc + prototype side-by-side
  splitRatio: number;               // 0.6 = 60% doc, 40% preview
}
```

### 7.3 Persistence

| What | Where | Why |
|---|---|---|
| Active prototype | URL hash (`#/web/experiment-overview`) | Shareable, back-button support |
| Sidebar collapsed | sessionStorage | Per-session preference |
| Expanded folders | sessionStorage | Per-session preference |
| Device preset | sessionStorage | Stays consistent while browsing prototypes |
| Zoom level | Not persisted | Resets to 100% on navigation |

---

## 8. Data Model

### 8.1 Prototype Manifest (`prototypes.json`)

```json
{
  "web": [
    {
      "id": "experiment-overview",
      "name": "Experiment Overview",
      "path": "00-Experiment_overview.html",
      "thumbnail": "thumbnails/00-exp-overview.png",
      "version": "2.3",
      "lastUpdated": "2026-06-20",
      "tags": ["experiment", "overview"]
    }
  ],
  "app": [
    {
      "id": "app-nav-overview",
      "name": "App Navigation Overview",
      "path": "app-nav-overview.html",
      "thumbnail": "thumbnails/app-nav.png",
      "version": "1.1",
      "lastUpdated": "2026-06-18",
      "tags": ["app", "navigation"]
    }
  ]
}
```

### 8.2 Documentation Pages

Markdown files rendered client-side:
- `content/product-guide.md`
- `content/review-report.md`
- `content/release-notes.md`

Each doc page can embed `[prototype:id]` shortcodes that render as inline links to open the referenced prototype in split view.

---

## 9. URL / Routing Scheme

| Route | View |
|---|---|
| `#/web/:id` | Web prototype preview |
| `#/app/:id` | App prototype preview (mobile frame default) |
| `#/guide` | Product Guide |
| `#/report` | Review Report |
| `#/notes` | Release Notes |
| `#/guide?proto=:id` | Guide with split-view prototype |

Hash-based routing keeps the implementation simple (no server required — works from `file://` or a static server).

---

## 10. Visual Style — Enterprise Theme

### 10.1 Color Palette

| Role | Color | Usage |
|---|---|---|
| Primary | `#2563eb` (blue-600) | Active states, links, accent borders |
| Primary hover | `#1d4ed8` (blue-700) | Button hover |
| Surface | `#ffffff` | Content cards, iframe background |
| Background | `#f1f5f9` (slate-100) | Page background |
| Nav background | `#f8fafc` (slate-50) | Left sidebar |
| Header background | `#1e293b` (slate-800) | Top header |
| Text primary | `#0f172a` (slate-900) | Headings, body text |
| Text secondary | `#475569` (slate-600) | Descriptions, metadata |
| Border | `#e2e8f0` (slate-200) | Dividers, card borders |
| Success | `#16a34a` (green-600) | Approved status |
| Warning | `#ca8a04` (yellow-600) | Changes requested |
| Error | `#dc2626` (red-600) | Breaking changes badge |

### 10.2 Typography

- **Font stack:** `"Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif`
- **Mono (code / release notes):** `"JetBrains Mono", "Fira Code", monospace`
- **Scale (px):** 11 (captions) / 12 (metadata) / 14 (body) / 16 (nav items) / 18 (section headers) / 24 (page titles)

### 10.3 Iconography

- Use a consistent icon set (Heroicons or Lucide, 20px/24px stroke-width 1.5)
- Nav items: outlined style when idle, filled style when active

---

## 11. Interaction Details

| Interaction | Behavior |
|---|---|
| Click nav item | Load prototype into iframe, update URL hash, update breadcrumb |
| Click device toggle | Animate iframe container width transition (300ms ease) |
| Hover device frame | Show subtle drop-shadow enhancement |
| Keyboard: `Ctrl+K` | Open command palette (search prototypes) |
| Keyboard: `D` / `T` / `M` | Switch device preset |
| Keyboard: `[` / `]` | Previous / next prototype in category |
| Right-click iframe | Prevent context menu (avoid confusion with prototype's own context menu) |
| iframe load error | Show fallback: "Prototype not found" with the expected path |

---

## 12. Spacing & Layout Tokens

| Token | Value |
|---|---|
| Header height | 56px |
| Nav width (expanded) | 240px |
| Nav width (collapsed) | 64px |
| Content padding | 24px |
| Toolbar height | 48px |
| Card border-radius | 8px |
| Mobile frame border-radius | 24px |
| Transition duration (standard) | 200ms ease |
| Transition duration (layout) | 300ms ease |
| Box shadow (card) | `0 1px 3px rgba(0,0,0,0.08), 0 1px 2px rgba(0,0,0,0.06)` |
| Box shadow (device frame) | `0 4px 24px rgba(0,0,0,0.12)` |

---

## 13. File Structure (Target)

```
原型test1/
├── index.html                    # Demo Center entry point
├── demo-center-design.md         # This document
├── prototypes.json               # Prototype manifest
├── css/
│   └── demo-center.css           # All styles (single file for simplicity)
├── js/
│   ├── demo-center.js            # App shell, routing, state
│   ├── nav.js                    # Left-nav logic
│   ├── preview.js                # iframe management
│   └── markdown.js               # Client-side MD rendering (marked.js or similar)
├── content/
│   ├── product-guide.md
│   ├── review-report.md
│   └── release-notes.md
├── thumbnails/                   # Optional: prototype screenshots
├── 00-Experiment_overview.html   # Existing prototypes (untouched)
├── 01-Add_New.html
├── ... (other prototype HTML files)
├── index-app.html
├── index-web.html
└── app-nav-overview.html
```

---

## 14. Non-Functional Requirements

| Requirement | Detail |
|---|---|
| No build step | Vanilla HTML/CSS/JS — works directly from a static file server or `file://` |
| No external CDN dependency | Vendor libraries (marked.js, etc.) bundled locally for air-gapped environments |
| iframe sandbox | `sandbox="allow-scripts allow-same-origin"` — prevents prototype JS from escaping into the shell |
| Loading state | Skeleton placeholder while iframe loads; 10s timeout with "Taking longer than expected" message |
| Error boundary | iframe `onerror` → inline error message; nav should remain functional |
| Browser support | Chrome 100+, Edge 100+, Firefox 120+, Safari 17+ |

---

## 15. Future Considerations (Out of Scope for v1)

- User authentication / role-based access
- Prototype comments / annotation overlay
- Side-by-side diff mode (compare two prototype versions)
- Video recording of demo walkthroughs
- Analytics on which prototypes are most viewed
- Dark mode
- Full-text search across prototypes and documentation
