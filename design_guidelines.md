# Design Guidelines: Task Management & Collaboration Platform

## Design Approach
**Reference-Based: Linear + Asana Hybrid**
Drawing from Linear's typography-driven clarity and Asana's information density, creating a productivity-focused interface that prioritizes efficiency and data visibility.

## Core Design Principles
1. **Information First**: Maximize data visibility while maintaining breathing room
2. **Hierarchy Through Typography**: Use size and weight variations instead of decorative elements
3. **Purposeful Density**: Pack information efficiently without feeling cramped
4. **Instant Clarity**: Users should understand their workspace at a glance

---

## Typography System

**Font Stack**: Inter (primary), SF Pro Display (headings)
- Page Titles: 2.5rem, weight 700, tight leading
- Section Headers: 1.5rem, weight 600, normal leading
- Card Titles: 1.125rem, weight 600
- Body Text: 0.875rem, weight 400, relaxed leading
- Metadata/Labels: 0.75rem, weight 500, uppercase tracking-wide
- Status Tags: 0.75rem, weight 600

---

## Layout & Spacing System

**Primary Spacing Units**: Tailwind 2, 4, 6, 8, 12, 16
- Component padding: p-4 to p-6
- Section gaps: gap-6 to gap-8
- Page margins: p-6 to p-8
- Card spacing: p-4 inside, gap-4 between

**Grid System**:
- Dashboard: 3-column layout (sidebar 256px + main content + right panel 320px)
- Task Lists: Single column with card rows, max-w-7xl centered
- Project Grid: 3-column responsive grid (grid-cols-1 md:grid-cols-2 lg:grid-cols-3)
- Analytics: 2-4 column metric cards

---

## Core Components

### Navigation
**Sidebar Navigation** (fixed left, 256px width):
- Logo/workspace selector at top
- Main navigation items with icons (Dashboard, Projects, Tasks, Team, Analytics)
- Active state: bold text + accent indicator bar
- Workspace switcher at bottom
- User profile menu at bottom

**Top Bar** (fixed, full-width):
- Search bar (prominent, centered or left-aligned, w-96)
- Quick actions: "+ New Task", "+ New Project" buttons
- Notifications bell icon
- User avatar (far right)

### Dashboard Layout
**Three-Zone Layout**:
- Left sidebar: 256px navigation
- Main content: Flexible width, max-w-screen-2xl
- Right panel (optional): 320px for activity feed

**Dashboard Sections** (stacked vertically):
1. Welcome header with user name + quick stats (4 metric cards in grid)
2. "Your Tasks Today" - Compact list view (8-10 items visible)
3. "Recent Projects" - 3-column card grid
4. "Team Activity" - Timeline view

### Cards & List Items

**Project Cards**:
- Header: Project name (bold), status badge
- Body: Description (2-line truncate), progress bar
- Footer: Avatar stack (team members), due date, task count
- Hover: Subtle lift effect (shadow increase)

**Task List Items**:
- Checkbox + Task title + Priority indicator
- Metadata row: Assignee avatar, project tag, due date
- Compact height (h-14 to h-16), efficient vertical stacking
- Alternating subtle backgrounds for readability

**Stat Cards**:
- Large number (3rem, weight 700)
- Label below (0.875rem, muted)
- Small trend indicator (arrow + percentage)
- Minimal padding (p-6), clean borders

### Forms & Inputs

**Input Fields**:
- Height: h-10 to h-12 (consistent across all inputs)
- Border: 1px solid, rounded-md
- Padding: px-4, py-2
- Focus: Ring effect (ring-2)
- Labels: Above input, 0.875rem, weight 500, mb-2

**Buttons**:
- Primary: px-6, py-2.5, rounded-md, weight 600
- Secondary: Same size, different treatment
- Icon buttons: Square (h-10 w-10), centered icon
- Button groups: Joined borders, no gap

**Modals/Dialogs**:
- Centered, max-w-2xl
- Header: Title (1.5rem, weight 600), close button
- Body: p-6, scrollable if needed
- Footer: Actions right-aligned, gap-3

### Data Display

**Tables** (for task lists, reports):
- Sticky header row
- Row hover: Background change
- Compact row height (h-12)
- Column padding: px-4, py-3
- Sortable headers with arrow indicators

**Charts** (analytics):
- Clean axes, minimal grid lines
- Data labels on hover only
- Use chart.js or recharts patterns
- Height: 320px to 400px

**Status Badges**:
- Rounded-full, px-3, py-1
- Text: 0.75rem, weight 600
- States: Todo, In Progress, Review, Done, Blocked

**Priority Indicators**:
- Small circular dots or vertical bars
- High/Medium/Low variants
- Inline with task titles

### Empty States
- Centered content: Icon (96px), heading, description, CTA button
- Use simple illustrations or large icons
- Encouraging copy: "No tasks yet – Create your first one!"

---

## Page-Specific Layouts

**Dashboard**: Multi-widget layout with metric overview at top

**Projects List**: Grid view with filtering sidebar (left, 240px) + 3-col project cards

**Project Detail**: 
- Hero section: Project name, description, status, team avatars
- Tab navigation: Overview, Tasks, Files, Activity
- Two-column: Main content + sidebar (timeline/stats)

**Task Detail** (modal or side panel):
- Full-height drawer from right (640px)
- Sections: Title edit, description, assignee, dates, comments
- Floating action bar at bottom

**Analytics**: 
- Metric cards at top (4-col grid)
- Charts below (2-col grid)
- Filters/date range picker in sticky header

---

## Responsive Behavior

**Desktop (lg:)**: Full 3-column layout with sidebars
**Tablet (md:)**: Hide right panel, collapsible left sidebar
**Mobile (base)**: 
- Bottom tab navigation replaces sidebar
- Single column layouts
- Floating "+ New" action button (bottom-right)
- Full-screen modals

---

## Images

This platform does NOT require hero images. Use icons and illustrations for:
- Empty states (simple line illustrations)
- Onboarding screens (optional 3-step visual guide)
- User avatars (actual photos or initials in colored circles)
- Project thumbnails (user-uploaded or colored placeholders)

All iconography from Heroicons (outline style for navigation, solid for actions).