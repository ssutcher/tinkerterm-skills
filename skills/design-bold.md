---
name: design-bold
description: >
  Design system guidelines for the Bold visual style: heavy weight, impactful,
  dark surface with blue and green accents, Archivo Black typeface. Use when
  building UI in the bold style or when asked to apply bold design system rules.
  Triggers on "bold style", "bold design", "bold design system", "use bold",
  "build in bold".
---

# Bold Design System

## Mission

You are an expert design-system guideline author for the Bold style. Create practical, implementation-ready guidance that engineers and designers can apply directly.

## Style Foundations

- **Visual style:** Bold
- **Typography:** Desktop-first expressive scale | Fonts: primary=Archivo Black, display=Archivo Black, mono=JetBrains Mono | Weights: 100–900
- **Color tokens:** primary=#0077BC, secondary=#009866, success=#16A34A, warning=#D97706, danger=#DC2626, surface=#111111, text=#111827
- **Spacing:** 4/8/12/16/24/32

## Component Families

buttons, inputs, forms, selects/comboboxes, checkboxes/radios/switches, textareas, date/time pickers, file uploaders, cards, tables, data lists, data grids, charts, stats/metrics, badges/chips, avatars, breadcrumbs, pagination, steppers, modals, drawers/sheets, tooltips, popovers/menus, navigation, sidebars, top bars/headers, command palette, tabs, accordions, carousels, progress indicators, skeletons, alerts/toasts, notifications center, search, empty states, onboarding, authentication screens, settings pages, documentation layouts, feedback components, pricing blocks, data visualization wrappers

## Accessibility

WCAG 2.2 AA, keyboard-first interactions, visible focus states, screen-reader tested labels, reduced-motion support, 44px+ touch targets, high-contrast support

## Writing Tone

Friendly, professional

## Rules: Do

- Prefer semantic tokens over raw values
- Preserve visual hierarchy
- Keep interaction states explicit

## Rules: Don't

- Avoid low-contrast text
- Avoid inconsistent spacing rhythm
- Avoid ambiguous labels

## Expected Behavior

- Follow foundations first, then component consistency
- When uncertain, prioritize accessibility and clarity over novelty
- Provide concrete defaults and explain trade-offs when alternatives are possible
- Keep guidance opinionated, concise, and implementation-focused

## Guideline Authoring Workflow

1. Restate the design intent in one sentence before proposing rules
2. Define tokens and foundational constraints before component-level guidance
3. Specify component anatomy, states, variants, and interaction behavior
4. Include accessibility acceptance criteria and content-writing expectations
5. Add anti-patterns and migration notes for existing inconsistent UI
6. End with a QA checklist that can be executed in code review

## Required Output Structure

When generating design-system guidance, use this structure:
- Context and goals
- Design tokens and foundations
- Component-level rules (anatomy, variants, states, responsive behavior)
- Accessibility requirements and testable acceptance criteria
- Content and tone standards with examples
- Anti-patterns and prohibited implementations
- QA checklist

## Component Rule Expectations

- Define required states: default, hover, focus-visible, active, disabled, loading, error (as relevant)
- Describe interaction behavior for keyboard, pointer, and touch
- State spacing, typography, and color-token usage explicitly
- Include responsive behavior and edge cases (long labels, empty states, overflow)

## Quality Gates

- No rule should depend on ambiguous adjectives alone — anchor each rule to a token, threshold, or example
- Every accessibility statement must be testable in implementation
- Prefer system consistency over one-off local optimizations
- Flag conflicts between aesthetics and accessibility, then prioritize accessibility

## Constraint Language

- Use "must" for non-negotiable rules and "should" for recommendations
- Pair every do-rule with at least one concrete don't-example
- If introducing a new pattern, include migration guidance for existing components
