# SKILL: Modern React UI Design

## Design System

### Colors (Tailwind classes)
Primary:    violet-600 / violet-700 hover (buttons, links, active nav)
Success:    emerald-500 (positive metrics, success toasts)
Warning:    amber-500 (alerts, approaching limits)
Danger:     red-500 (delete, errors, critical alerts)
Background: gray-50 / dark:gray-950
Surface:    white / dark:gray-900
Border:     gray-200 / dark:gray-800
Text:       gray-900 / dark:gray-100 (primary), gray-500 / dark:gray-400 (secondary)

### Spacing & Layout
Page padding: `px-4 sm:px-6 lg:px-8`
Max content width: `max-w-7xl mx-auto`
Card style: `bg-white dark:bg-gray-900 rounded-xl border border-gray-200 dark:border-gray-800 shadow-sm p-6`
Section gap: `space-y-6`

### Component Patterns

#### Navigation
Desktop: Fixed left sidebar (240px), collapsible
Mobile: Bottom navigation bar (5 items max)
Active state: `bg-violet-50 text-violet-700 dark:bg-violet-950 dark:text-violet-300`

#### Data Tables
Sticky header, `divide-y`, alternating `even:bg-gray-50/50`
Sort icons on headers, action column at right (Edit + Delete)
Empty state: centered icon + heading + subtext + CTA button

#### Loading States
Content areas: Skeleton components (`animate-pulse bg-gray-200 rounded`)
Button submitting: Spinner icon inside button + disabled
Full page: Skeleton matching the actual content layout (not generic)

#### Forms
Label above input, always
Error text: `text-sm text-red-500 mt-1`
Full width inputs on mobile, constrained on desktop
Submit disabled during loading (no double-submit)

#### Charts (Recharts)
Always wrapped in `<ResponsiveContainer width="100%" height={300}>`
Always include `<Tooltip />` and `<Legend />`
Use violet-600 as primary chart color, emerald-500 as secondary

## Dark Mode
Every component has `dark:` variant for all color classes.
Use `class="... dark:..."` — never JS-based theme toggling.