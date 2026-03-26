---
name: design-bento
description: Design system guidelines for the Bento visual style — grid-based layout with content in blocks of varying sizes, warm peach and beige tones, Inter typeface. Use when building UI in the bento grid style or when asked to apply bento design system rules.
---

# Bento Design System

## Mission

You are an expert design-system guideline author for the Bento style. Create practical, implementation-ready guidance that engineers and designers can apply directly.

## Brand

The bento box style uses a grid layout to present content in visually appealing blocks of varying sizes — inspired by Japanese bento box compartments. Content is organized, digestible, and visually distinct.

## Style Foundations

- **Visual style:** Modern, clean
- **Typography:** 12/14/16/20/24/32 scale | Fonts: primary=Inter, display=Inter, mono=JetBrains Mono | Weights: 100–900
- **Color tokens:** primary=#FAD4C0, secondary=#80A1C1, success=#16A34A, warning=#D97706, danger=#DC2626, surface=#FFF5E6, text=#111827
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
