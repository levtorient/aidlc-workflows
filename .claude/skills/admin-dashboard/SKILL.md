---
name: admin-dashboard
description: Build the admin dashboard for the project. Use this skill when the user needs to create or modify the admin panel for managing data, viewing metrics, or performing administrative tasks. Functional and clean UI prioritizing data clarity over visual flair.
---

This skill guides development of admin interfaces. Unlike public-facing pages (which prioritize aesthetics and conversion), admin dashboards prioritize **data clarity, efficiency, and usability**. Read `requirements.md` and the backend API to understand what data exists and what management features are needed.

## Design Philosophy

The admin dashboard is a **tool, not a showpiece**:
- Clean and functional — no unnecessary decoration
- Data density over excessive whitespace
- Fast load times, instant feedback on actions
- Keyboard-friendly navigation
- Consistent patterns across all pages
- Optimized for desktop, functional on tablet

## Approach

1. **Inventory the backend** — read existing API endpoints and entities to understand what data is available
2. **Derive pages from the domain** — each major entity or business function gets a list view and detail view
3. **Start with the overview** — build a dashboard home that surfaces the most important metrics
4. **Use a component library** — Shadcn/ui, Ant Design, or similar. Don't hand-craft admin UI components.

## UI Patterns

### Tables
- Sticky header, row hover, clickable rows to detail
- Pagination, column sorting, filters, search
- Empty state, loading skeleton, error with retry
- Bulk actions and CSV export where useful

### Forms
- Inline validation with field-level errors
- Loading state on submit, success toast on completion
- Confirmation dialog for destructive actions

### Navigation
- Sidebar with icon + label per section
- Collapsible on smaller screens
- Active page highlighted, breadcrumbs on detail pages

### Data Display
- Currency formatted to locale
- Dates: relative for recent, absolute for older
- Status indicators: colored badges, not plain text
- Charts for trends — use Recharts, Chart.js, or ECharts

## Data Fetching

- Use TanStack Query (or equivalent) for caching, deduplication, and background refetch
- Show loading and error states for every data fetch
- Invalidate related queries after mutations
- Paginate all list views — never load everything at once
- Debounce search inputs

## Auth

- JWT-based authentication matching the backend admin auth
- Store token in memory or httpOnly cookie — not localStorage
- Redirect to login on 401
- Protect all admin routes

## Performance

- Lazy-load heavy dependencies (chart libraries, export utilities)
- Virtualize long lists when row count exceeds visible area
- Debounce and throttle user-triggered API calls
