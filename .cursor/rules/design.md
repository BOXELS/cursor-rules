---
description: Design system, visual standards, component behavior, and interaction patterns. Applies to all UI work.
globs:
alwaysApply: true
---

# Design Rules

## Component library

- [Base component library, e.g. "shadcn/ui", "Material UI", "Ant Design", "Vuetify", "DaisyUI", "custom components"]. Extend existing components — never rebuild from scratch what the library already provides.
- Icons: [icon set, e.g. "Lucide React", "Heroicons", "Material Icons", "Font Awesome"]. [Defaults, e.g. "20px default size, 1.5px stroke weight."]
- Animations: [animation library, e.g. "Framer Motion", "GSAP", "CSS transitions only", "Svelte transitions"]. [Constraint, e.g. "Max 300ms for UI transitions. No animations on first paint."]
- Dropdowns, popovers, and overlays: [approach, e.g. "Radix primitives via shadcn", "Headless UI", "native library components"]. Must have proper keyboard navigation and dismiss on outside click.
- Dialogs: [approach, e.g. "shadcn Dialog", "Material Dialog", "custom modal component"]. Never use alert(), window.confirm(), or browser-native dialogs.

## States

Every interactive component must account for all of its states. Don't ship a "happy path only" UI.

- **Loading**: Every async operation needs a loading indicator. [Approach, e.g. "Skeleton loaders for content areas", "Spinner inside buttons during actions", "Progress bars for uploads"]. Never show blank screens while data loads.
- **Empty**: Every list, table, and feed needs a designed empty state — [approach, e.g. "illustration + message + call-to-action", "helpful prompt to get started", "minimal text"]. Never show a blank container.
- **Error**: [Approach, e.g. "Inline error messages below fields", "Toast notifications for action failures", "Error boundaries for component crashes"]. Errors should explain what happened and offer a path forward.
- **Interactive**: All interactive elements need hover, focus, active, and disabled states. No element should feel unresponsive.
- **Buttons**: [Loading behavior, e.g. "Show spinner inside the button during async actions. Disable while loading. Never allow double-submit."]

## Specifications

- [Spacing scale, e.g. "Between sections: 64px. Between components: 24px. Between elements: 8px." or "Use the 4px grid: 4, 8, 12, 16, 24, 32, 48, 64." or "Follow the framework's spacing scale."] Don't introduce one-off spacing values without asking.
- [Border radius, e.g. "Cards: 12px. Buttons: 8px. Inputs: 6px." or "Use the design system's radius tokens."]
- [Typography, e.g. "Use only the defined font sizes from the design system. Never introduce a one-off size." Include font family if decided, e.g. "Inter for body, Cal Sans for headings."]
- [Responsive breakpoints, e.g. "640px (mobile), 768px (tablet), 1024px (desktop), 1280px (wide)" or "Use the framework's default breakpoints."]

## Color and tokens

- [Color approach, e.g. "All colors defined as CSS custom properties in globals.css", "Tailwind theme colors only", "SCSS variables", "design tokens in a theme file."]
- [Dark mode status, e.g. "Dark mode uses semantic tokens — never hardcode colors", "Dark mode is not yet supported — don't add it", "System preference detection with manual toggle."]
- [Key palette if defined, e.g. "Primary: #2563EB, Secondary: #7C3AED, Destructive: #DC2626" or "See the theme configuration file." Remove this line if not yet decided.]

## Patterns

- Notifications: [approach, e.g. "Toast notifications via sonner, bottom-right, auto-dismiss after 4 seconds", "Snackbar via Material UI, bottom-center"]. Use for success/error feedback on user actions.
- Forms: [approach, e.g. "react-hook-form + zod", "Formik + yup", "native form validation", "VeeValidate"]. [Validation timing, e.g. "Inline validation on blur. Error messages below the field, not in toasts."]. [Submit behavior, e.g. "Disable submit button while processing. Show loading state. Prevent double submission."]
- Modals: Must have a clear close action — [requirements, e.g. "X button + click outside + Escape key"]. Never trap the user in a modal.
- Tables: [approach, e.g. "Sticky header, horizontal scroll on mobile, row hover highlight", "Use TanStack Table for sorting and filtering"]. Never break the table layout on small screens.
- Images: [approach, e.g. "Always set width and height attributes. Use next/image with proper sizing", "Use lazy loading for below-fold images", "Always include alt text"]. Never cause layout shift on load.
- Scrollable areas: [approach, e.g. "Visible scroll indicators on content that overflows", "Custom scrollbar styling via the design system"]. Never hide scrollbars on overflowing content.

## Accessibility

- [Target conformance level, e.g. "WCAG 2.1 AA", "Best-effort accessibility", "Full WCAG 2.1 AAA"]. [Remove this section entirely if accessibility requirements are not yet defined.]
- All interactive elements must be keyboard-navigable. Tab order must be logical.
- Color contrast must meet [standard, e.g. "4.5:1 for normal text, 3:1 for large text (AA)", "7:1 (AAA)"].
- [Motion, e.g. "Respect prefers-reduced-motion — disable non-essential animations when set", "All animations are optional and purely decorative."]
- Images must have descriptive alt text. Decorative images use empty alt="".
- Form fields must have associated labels. Never use placeholder text as the only label.
