# Design Guidelines: SCOR Level 1 Make - Serious Simulation Game

## Design Approach: Material Design System
**Rationale**: Data-heavy educational dashboard requiring clear information hierarchy, robust component library for forms/tables/charts, and proven patterns for multi-user collaborative interfaces.

---

## Core Design Principles

1. **Data-First Clarity**: Information hierarchy prioritizes KPI visibility and decision-making efficiency
2. **Role-Based Contextualization**: Each user role sees relevant controls without clutter
3. **Progressive Disclosure**: Complex manufacturing concepts revealed through structured phases
4. **Collaborative Awareness**: Visual indicators show team member activities and decisions

---

## Typography System

**Font Family**: 
- Primary: Inter (via Google Fonts CDN)
- Monospace: JetBrains Mono (for numerical data, KPIs)

**Hierarchy**:
- H1: 2.5rem/bold - Page titles (Dashboard, Scenario Setup)
- H2: 2rem/semibold - Section headers (Production Configuration, KPI Overview)
- H3: 1.5rem/semibold - Card titles, Role module headers
- H4: 1.25rem/medium - Subsection headers
- Body: 1rem/regular - Standard content, descriptions
- Small: 0.875rem/regular - Helper text, labels
- Data: 1.125rem/medium (monospace) - KPIs, metrics, calculations

---

## Layout System

**Spacing Units**: Tailwind units of 2, 4, 6, 8, 12, 16, 24
- Component padding: p-4, p-6
- Section spacing: gap-6, gap-8
- Card margins: m-4, m-6
- Dashboard grid gaps: gap-6

**Grid Structure**:
- Main dashboard: 12-column grid (grid-cols-12)
- KPI cards: 3-4 columns on desktop (lg:grid-cols-4), 2 on tablet (md:grid-cols-2), 1 on mobile
- Role modules: 2-column layouts for forms + preview (lg:grid-cols-2)

**Container Widths**:
- Full dashboards: max-w-[1600px] mx-auto
- Role modules: max-w-7xl
- Forms/dialogs: max-w-2xl

---

## Component Library

### Navigation & Structure

**Top Navigation Bar**:
- Fixed header (h-16) with logo, session info, role indicator, team name
- Right section: timer/round indicator, notifications, user menu
- Material elevation-2 shadow

**Side Navigation** (Dosen/Admin):
- w-64 sidebar with menu items for Scenarios, Classes, Analytics, Reports
- Active state with subtle background and left border accent
- Collapsible on mobile

**Role-Based Dashboard Layout**:
- Top: Session context card (current round, team performance summary)
- Main area: 2-3 column grid of role-specific modules
- Bottom: Quick access to team chat/collaboration panel

### Data Display Components

**KPI Cards**:
- Compact cards (min-h-32) with:
  - Metric label (small, muted)
  - Large numerical value (data typography, monospace)
  - Trend indicator (arrow icon + percentage change)
  - Sparkline visualization for historical trend
- Grid layout: 4 cards per row (desktop), responsive stack

**OEE Dashboard Panel**:
- 3-metric breakdown (Availability, Performance, Quality)
- Horizontal bar indicators showing component contribution
- Color-coded segments (avoid specific colors per guidelines, but maintain visual distinction)
- Overall OEE score prominently displayed (2.5rem monospace)

**Production Line Visualizer**:
- Horizontal flow diagram showing stations
- Bottleneck highlighting with pulsing indicator
- WIP counts at each station
- Clickable stations to view detailed metrics

**Data Tables**:
- Striped rows for readability (alternate row backgrounds)
- Sticky header row
- Sortable columns with icon indicators
- Inline edit capability for configuration tables
- Pagination for large datasets

### Input & Configuration

**Role Module Cards**:
- Sectioned cards with clear boundaries (border-2)
- Header with role icon + title
- Form sections with labeled groups
- Action buttons aligned right in footer

**Configuration Forms**:
- Label above input pattern
- Helper text below inputs for guidance
- Validation messages inline with field
- Toggle switches for binary choices (MTS/MTO)
- Number spinners for capacity, lot size
- Range sliders for continuous values (automation level)

**Decision Confirmation Modal**:
- Centered dialog (max-w-lg)
- Summary of changes to be applied
- Impact preview (estimated KPI changes)
- Dual action: Cancel (outlined) + Confirm (filled)

### Feedback & Analytics

**Round Summary Panel**:
- Full-width card appearing between rounds
- 3-section layout:
  - Left: Key KPI changes (before/after comparison)
  - Center: Notable events/insights
  - Right: Team ranking/position
- Expandable detailed breakdown

**Learning Analytics Dashboard** (Dosen):
- Multi-tab interface: Overview, Individual Performance, Team Comparison, LO/SO3 Achievement
- Filter controls: Class, Session, Round, Team
- Combination of charts: bar charts for comparisons, line charts for trends, heat maps for engagement
- Export button (top-right)

**Tutorial/Practice Mode**:
- Overlay guide with step-by-step progression
- Highlighted interactive areas with tooltips
- Progress indicator (step X of Y)
- Skip option for experienced users

### Visualization Components

**Charts** (using Chart.js or similar):
- Utilization Bar Chart: horizontal bars per station
- OEE Trend Line: multi-round progression
- Defect Rate Area Chart: cumulative view
- Capacity vs Output Comparison: grouped bars

**Status Indicators**:
- Round status badge: "Design Phase" / "Simulating" / "Reviewing Results"
- Team member activity indicators: small avatars with status dots
- Alert chips for critical issues (bottleneck detected, target missed)

---

## Specialized Interfaces

### Student Dashboard (Main Play Area):
- Top: Session header with round timer, team KPIs at-a-glance
- Left sidebar (w-72): Role switcher + quick navigation to team member modules
- Center (flex-1): Primary workspace for current role
- Right panel (w-80, collapsible): Team chat + recent decisions log

### Dosen Scenario Builder:
- Two-column layout:
  - Left: Configuration form (products, routing, demand patterns, targets)
  - Right: Live preview of production line diagram
- Stepper component for multi-step scenario creation
- Template library for quick starts

### Team Collaboration View:
- Quadrant layout showing all 4 role modules simultaneously (2x2 grid on large screens)
- Each quadrant shows real-time status of that role's configuration
- Lock icons indicating finalized decisions
- Central "Submit Round" button when all roles ready

---

## Responsive Behavior

**Desktop (≥1280px)**:
- Full dashboard layouts with multi-column KPI grids
- Side-by-side role module comparisons
- Expanded charts and visualizations

**Tablet (768px - 1279px)**:
- 2-column KPI grids
- Stacked role modules with tabbed navigation
- Collapsible sidebars

**Mobile (≤767px)**:
- Single column layouts
- Bottom navigation bar for key actions
- Full-screen modals for complex inputs
- Simplified chart views

---

## Images

**Not required for this application** - This is a data-driven educational tool where:
- Visual content is generated dynamically (production line diagrams, charts)
- Focus is on functional clarity over marketing aesthetics
- Icons from Material Icons library provide sufficient visual elements
- Avatars for users can use placeholder services (UI Avatars)

---

## Accessibility & Usability

- High contrast for data readability (especially numerical KPIs)
- Keyboard navigation for all form inputs and table interactions
- ARIA labels for complex visualizations and charts
- Focus indicators clearly visible on all interactive elements
- Consistent button sizing (min h-10) for touch targets
- Loading states for simulation execution with progress indicators
- Error states with clear recovery actions

---

## Animation & Transitions

Use **sparingly and purposefully**:
- KPI value changes: number counter animation (300ms)
- Card state changes: subtle scale + shadow transition (200ms)
- Tab/role switching: fade transition (150ms)
- Modal open/close: scale + opacity (250ms)
- Chart data updates: smooth interpolation (400ms)
- **No decorative animations** - every animation serves functional feedback