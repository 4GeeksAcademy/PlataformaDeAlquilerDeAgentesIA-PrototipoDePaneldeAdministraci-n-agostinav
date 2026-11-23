---
name: Nexus Precision
colors:
  surface: '#f8f9ff'
  surface-dim: '#cbdbf5'
  surface-bright: '#f8f9ff'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#eff4ff'
  surface-container: '#e5eeff'
  surface-container-high: '#dce9ff'
  surface-container-highest: '#d3e4fe'
  on-surface: '#0b1c30'
  on-surface-variant: '#464555'
  inverse-surface: '#213145'
  inverse-on-surface: '#eaf1ff'
  outline: '#777587'
  outline-variant: '#c7c4d8'
  surface-tint: '#4d44e3'
  primary: '#3525cd'
  on-primary: '#ffffff'
  primary-container: '#4f46e5'
  on-primary-container: '#dad7ff'
  inverse-primary: '#c3c0ff'
  secondary: '#712ae2'
  on-secondary: '#ffffff'
  secondary-container: '#8a4cfc'
  on-secondary-container: '#fffbff'
  tertiary: '#00505f'
  on-tertiary: '#ffffff'
  tertiary-container: '#006a7c'
  on-tertiary-container: '#93e8ff'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#e2dfff'
  primary-fixed-dim: '#c3c0ff'
  on-primary-fixed: '#0f0069'
  on-primary-fixed-variant: '#3323cc'
  secondary-fixed: '#eaddff'
  secondary-fixed-dim: '#d2bbff'
  on-secondary-fixed: '#25005a'
  on-secondary-fixed-variant: '#5a00c6'
  tertiary-fixed: '#acedff'
  tertiary-fixed-dim: '#4cd7f6'
  on-tertiary-fixed: '#001f26'
  on-tertiary-fixed-variant: '#004e5c'
  background: '#f8f9ff'
  on-background: '#0b1c30'
  surface-variant: '#d3e4fe'
typography:
  headline-xl:
    fontFamily: Inter
    fontSize: 36px
    fontWeight: '700'
    lineHeight: 44px
    letterSpacing: -0.025em
  headline-xl-mobile:
    fontFamily: Inter
    fontSize: 28px
    fontWeight: '700'
    lineHeight: 36px
    letterSpacing: -0.02em
  headline-lg:
    fontFamily: Inter
    fontSize: 30px
    fontWeight: '600'
    lineHeight: 38px
    letterSpacing: -0.02em
  headline-lg-mobile:
    fontFamily: Inter
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
    letterSpacing: -0.015em
  headline-md:
    fontFamily: Inter
    fontSize: 20px
    fontWeight: '600'
    lineHeight: 28px
    letterSpacing: -0.015em
  headline-sm:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '600'
    lineHeight: 24px
    letterSpacing: -0.01em
  body-lg:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '400'
    lineHeight: 24px
  body-md:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '400'
    lineHeight: 20px
  body-sm:
    fontFamily: Inter
    fontSize: 12px
    fontWeight: '400'
    lineHeight: 18px
  label-md:
    fontFamily: JetBrains Mono
    fontSize: 13px
    fontWeight: '500'
    lineHeight: 16px
    letterSpacing: -0.01em
  label-sm:
    fontFamily: JetBrains Mono
    fontSize: 11px
    fontWeight: '500'
    lineHeight: 14px
    letterSpacing: 0.02em
rounded:
  sm: 0.25rem
  DEFAULT: 0.5rem
  md: 0.75rem
  lg: 1rem
  xl: 1.5rem
  full: 9999px
spacing:
  gutter: 1.5rem
  gutter-sm: 1rem
  margin: 2rem
  margin-sm: 1rem
  space-xs: 0.25rem
  space-sm: 0.5rem
  space-md: 1rem
  space-lg: 1.5rem
  space-xl: 2rem
---

## Brand & Style
The design system targets enterprise technical teams, AI operators, and operations managers orchestrating complex autonomous agent workflows. The aesthetic projects clarity, quiet authority, and computational precision. It merges contemporary enterprise SaaS ergonomics with functional minimalism: generous structural breathing room, sharp typographic rhythm, and deliberate chromatic signals that prevent cognitive overload across dense analytical views.

Visual communication is anchored in low-friction scanning. Rather than decorative artifacts, value is communicated through structural clarity, disciplined information hierarchies, and predictable spatial pacing.

## Colors
The palette balances authoritative brand anchors against a calibrated palette of semantic and architectural neutrals. 

- **Primary & Secondary:** `Indigo-600` (`#4f46e5`) serves as the dominant structural and interactive anchor, with `Violet-600` (`#7c3aed`) reserved for secondary focal points and contextual agent orchestrations.
- **Canvas & Surfaces:**
  - **Light Mode:** Canvas defaults to `slate-50` (`#f8fafc`), with container elements and cards rendered in pure `#ffffff`. Structural borders utilize `slate-200` (`#e2e8f0`).
  - **Dark Mode:** Canvas transitions to `slate-900` (`#0f172a`), layered surfaces utilize `slate-800` (`#1e293b`), and raised popovers/modals utilize `slate-800/90` or `slate-750`. Dividing borders rest on `slate-700` (`#334155`).
- **Semantic Badges & Indicators:**
  - **Active / Operational:** `emerald-500` text on `emerald-50` background (dark: `emerald-400` on `emerald-950/40`, border `emerald-800/40`).
  - **Inactive / Dormant:** `slate-600` text on `slate-100` background (dark: `slate-400` on `slate-800`, border `slate-700`).
  - **Error / Failing:** `rose-600` text on `rose-50` background (dark: `rose-400` on `rose-950/40`, border `rose-800/40`).
  - **Pending / In Queue:** `amber-600` text on `amber-50` background (dark: `amber-400` on `amber-950/40`, border `amber-800/40`).

## Typography
The system uses `Inter` across all structural narrative layers, titles, and body content for maximum neutrality and horizontal balance at micro-sizes. For system identifiers, timestamps, metrics, model versions, and token allocations, `JetBrains Mono` provides tabular numeric alignment and clear character differentiation.

- Titles utilize negative letter-spacing (`tracking-tight`) to condense header space and establish hierarchy over dense data matrices.
- Numeric displays in tables and key metric cards must enforce tabular figures (`font-variant-numeric: tabular-nums`) to avoid layout jitter during real-time streaming updates.

## Layout & Spacing
The layout model employs a fixed persistent shell with a fluid internal data workspace.

- **Shell Architecture:**
  - **Sidebar:** Fixed width of `16rem` (`256px`) on desktop views (`lg:` viewport breakpoint), collapsing to an off-canvas drawer controlled by overlay mechanics beneath `1024px`.
  - **Header:** Sticky top bar at a fixed height of `4rem` (`64px`), spanning the remainder of the viewport width.
  - **Main Canvas:** Fluid workspace with standard viewport edge margins (`margin-sm: 1rem` on mobile, scaling to `margin: 2rem` on wide desktop arrays).
- **Responsive Adaptations:**
  - **Desktop (1024px+):** Multi-column dashboard grids (typically 12 columns with `1.5rem` gutters) allowing 4-column summary metric cards and 8/4 split layouts for tables and real-time activity streams.
  - **Tablet (768px - 1023px):** Data tables transition to horizontally scrollable viewports; grid metrics wrap to 2-column bands.
  - **Mobile (<768px):** Single-column stacks; gutters tighten to `1rem`. Secondary data attributes in lists collapse into contextual disclosure accordions.

## Elevation & Depth
Depth is constructed through subtle tonal transitions complemented by fine, low-contrast hairline borders. Deep drop shadows are avoided in favor of focused perimeter definition.

- **Level 0 (Base Canvas):** Flat `slate-50` (dark: `slate-900`) with no depth.
- **Level 1 (Card & Content Panels):** Surface rendered in `white` (dark: `slate-800`), bordered by `1px solid slate-200` (dark: `1px solid slate-700/80`). Subtle elevation is provided by an ambient ground shadow: `0 1px 2px 0 rgba(0, 0, 0, 0.05)`.
- **Level 2 (Popovers, Flyouts, Dropdowns):** Floating panels surface with `0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -4px rgba(0, 0, 0, 0.1)` (dark: `0 10px 20px -5px rgba(0, 0, 0, 0.5)`), bounded by `slate-200` (dark: `slate-700`).
- **Level 3 (Modal Overlays):** Modals feature `0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 8px 10px -6px rgba(0, 0, 0, 0.1)` on top of a `slate-900/60` backdrop blur (`backdrop-blur-sm`).

## Shapes
The shape language is controlled and geometric (`roundedness: 2`). Standard interface elements—such as buttons, inputs, table cell enclosures, and cards—utilize `rounded-lg` (`0.5rem` / `8px`). 

Inner elements nested directly inside containers step down to `rounded-md` (`0.375rem` / `6px`) to preserve concentric corner geometry. Badges, pill indicators, and avatars alone break this constraint by leveraging full continuous curvature (`rounded-full`).

## Components

### Buttons
- **Primary:** `bg-indigo-600 hover:bg-indigo-700 text-white font-medium text-sm px-4 py-2 rounded-lg shadow-sm transition-colors focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 dark:focus:ring-offset-slate-900`.
- **Secondary / Subtle:** `bg-white dark:bg-slate-800 text-slate-700 dark:text-slate-200 border border-slate-300 dark:border-slate-700 hover:bg-slate-50 dark:hover:bg-slate-700/60 font-medium text-sm px-4 py-2 rounded-lg transition-colors`.
- **Destructive:** `bg-rose-50 dark:bg-rose-950/40 text-rose-600 dark:text-rose-400 border border-rose-200 dark:border-rose-800/40 hover:bg-rose-100 font-medium text-sm px-4 py-2 rounded-lg transition-colors`.

### Semantic Badges & Status Chips
- Height: `1.5rem` (`24px`).
- Shape: `rounded-full px-2.5 py-0.5 text-xs font-medium inline-flex items-center gap-1.5`.
- Active states feature a pulsing `1.5` unit dot indicator (`h-1.5 w-1.5 rounded-full bg-emerald-500`).

### Form Inputs & Selectors
- Standard base: `w-full rounded-lg border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-800 text-slate-900 dark:text-slate-100 px-3.5 py-2 text-sm shadow-sm placeholder:text-slate-400 focus:border-indigo-500 focus:ring-1 focus:ring-indigo-500 outline-none`.
- Monospace variant for API keys, cron syntax, and model paths: injects `font-mono text-xs`.

### Checkboxes & Radios
- Size: `h-4 w-4 rounded border-slate-300 dark:border-slate-700 text-indigo-600 focus:ring-indigo-500 dark:focus:ring-offset-slate-900 bg-white dark:bg-slate-800`.

### Data Tables
- Container: Surface wrapper `bg-white dark:bg-slate-800 rounded-lg border border-slate-200 dark:border-slate-700 overflow-hidden`.
- Header: `bg-slate-50 dark:bg-slate-850 px-4 py-3 text-left text-xs font-semibold text-slate-500 dark:text-slate-400 uppercase tracking-wider border-b border-slate-200 dark:border-slate-700`.
- Rows: `hover:bg-slate-50/75 dark:hover:bg-slate-700/40 transition-colors border-b border-slate-100 dark:border-slate-700/50 last:border-b-0`.
- Cell alignment: Vertical centering with `px-4 py-3.5 text-sm text-slate-700 dark:text-slate-300`. Actions column anchored right with a persistent 3-dot dropdown trigger.

### Navigation Shell Components
- **Sidebar Nav Item:** Standard `flex items-center gap-3 px-3 py-2 text-sm font-medium rounded-lg text-slate-600 dark:text-slate-400 hover:text-slate-900 dark:hover:text-slate-100 hover:bg-slate-100 dark:hover:bg-slate-800 transition-colors`.
- **Active Sidebar Nav Item:** `text-indigo-600 dark:text-indigo-400 bg-indigo-50 dark:bg-indigo-950/50 font-semibold relative before:absolute before:left-0 before:top-1.5 before:bottom-1.5 before:w-1 before:bg-indigo-600 before:rounded-r`.
- **Header:** Flex container with dynamic page title, global search bar, dark/light theme toggle, and user profile popover trigger.

### Modal Dialogs
- Overlay: Fixed viewport inset with `bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4`.
- Dialog Body: `bg-white dark:bg-slate-800 rounded-xl border border-slate-200 dark:border-slate-700 shadow-xl max-w-lg w-full overflow-hidden transform transition-all`.
- Header/Footer: Clean spatial segregation using `px-6 py-4 border-b (header) / border-t (footer) border-slate-100 dark:border-slate-700`.