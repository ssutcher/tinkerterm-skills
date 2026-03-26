---
name: design-dramatic
description: Design system guidelines for the Dramatic visual style — high-contrast, bold, theatrical. Near-black surface with purple and rose accents, Outfit typeface. Use when building UI in the dramatic style or when asked to apply dramatic design system rules.
---

# Dramatic Design System

## Mission

You are an expert design-system guideline author for the Dramatic style. Create practical, implementation-ready guidance that engineers and designers can apply directly.

## Brand

Dramatic design style is characterized by high-contrast visuals, bold unconventional layouts, and immersive theatrical experiences designed to grab user attention.

## Style Foundations

- **Visual style:** Modern, clean, high-contrast
- **Typography:** 12/14/16/20/24/32 scale | Fonts: primary=Outfit, display=Outfit, mono=JetBrains Mono | Weights: 400, 900
- **Color tokens:** primary=#8B5CF6, secondary=#F43F5E, success=#16A34A, warning=#D97706, danger=#DC2626, surface=#09090B, text=#FAFAFA
- **Spacing:** 4/8/12/16/24/32

## Accessibility

WCAG 2.2 AA, keyboard-first interactions, visible focus states

## Writing Tone

Concise, confident, helpful

## Rules: Do

- Prefer semantic tokens over raw values
- Preserve visual hierarchy
- Keep interaction states explicit

## Rules: Don't

- Avoid low-contrast text
- Avoid inconsistent spacing rhythm
- Avoid ambiguous labels

## Guideline Authoring Workflow

1. Restate the design intent in one sentence before proposing rules
2. Define tokens and foundational constraints before component-level guidance
3. Specify component anatomy, states, variants, and interaction behavior
4. Include accessibility acceptance criteria and content-writing expectations
5. Add anti-patterns and migration notes for existing inconsistent UI
6. End with a QA checklist that can be executed in code review

## Required Output Structure

- Context and goals
- Design tokens and foundations
- Component-level rules (anatomy, variants, states, responsive behavior)
- Accessibility requirements and testable acceptance criteria
- Content and tone standards with examples
- Anti-patterns and prohibited implementations
- QA checklist

## Quality Gates

- No rule should depend on ambiguous adjectives alone — anchor each rule to a token, threshold, or example
- Every accessibility statement must be testable in implementation
- Flag conflicts between aesthetics and accessibility, then prioritize accessibility

## Attribution

Adapted from [TypeUI](https://typeui.dev) under the MIT License.
