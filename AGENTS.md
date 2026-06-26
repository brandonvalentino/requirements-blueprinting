# Requirements Blueprinting — Agent Guide

## Repo Purpose

A skill for AI agents to produce predictable, structured requirements documents (BRD, FSD, TSD) from project context. The skill is model-invoked — agents fire on keywords like "BRD", "FSD", "TSD", "requirements documentation".

## Structure

```
skills/
└── requirements-blueprinting/
    ├── SKILL.md           # Main skill — 4-phase process, 3 branches, model-invoked
    ├── BRD-TEMPLATE.md    # BRD blueprint (13 sections with interview prompts)
    ├── FSD-TEMPLATE.md    # FSD blueprint (process flows, business rules, screens, NFRs)
    ├── TSD-TEMPLATE.md    # TSD blueprint (architecture, DB, API, security, deployment)
    └── GLOSSARY.md        # Single source: ID convention, traceability, boilerplate
AGENTS.md                  # This file — agent rules and conventions
README.md                  # Human-facing documentation
```

## Design Conventions

- **Leading words** — the skill uses four: Blueprint (the template), Excavation (gathering requirements + interview protocol), Composition (writing the document), Craftsmanship (quality checks).
- **One ID home** — GLOSSARY.md is the single source of truth for the ID prefix convention (BO, SM, RI, AS, DE, FE, LI, UC). SKILL.md and template files point there; they never restate the list.
- **No external skill dependency** — the interview protocol (hypothesize + confidence, one-at-a-time with guesses, restate-and-confirm) is inlined in SKILL.md Phase 1. It does not reference the `interview-me` skill.
- **Three branches** — BRD, FSD, TSD. Each loads its own template from a sibling file. One document per invocation. All branches share the same 4-phase process.
- **Mermaid diagrams** — embedded as code blocks in the output document. Conventions table in SKILL.md maps diagram type to Mermaid flavor.
- **Traceability IDs** — enforced. The BRD defines them (BO-1, FE-3, etc.). FSD and TSD carry them forward. Craftsmanship Phase 4 checks for dangling references.

## AGENTS.md is the Rules File

This is Level 1 context (always loaded, project-wide). See [Context Engineering skill](https://github.com/brandonvalentino/requirements-blueprinting) for the hierarchy.

## Commands

- `git push` to deploy changes
- No build, test, or lint steps — this repo is pure markdown
- Validate: ensure all context pointers in SKILL.md resolve to sibling files

## Boundaries

- **Do not** restate the ID convention anywhere outside GLOSSARY.md. That's the single source.
- **Do not** add external skill dependencies. Any pattern the skill needs must be inlined in SKILL.md or one of its template siblings.
- **Do not** add code or scripts to this repo — it's a skill, not an application.
- **Do not** change the leading words without updating all four template references consistently.
- **Do not** add a fourth branch without also adding its `-TEMPLATE.md` sibling file.
- **Do not** remove the Craftsmanship phase — it's the quality gate. Every check must pass before yielding.

## Confusion Management

If a future change touches the ID convention, the interview protocol, or the phase structure, surface the conflict explicitly and ask before acting. These are load-bearing design decisions that affect every invocation.

## Patterns

The skill was built following the writing-great-skills conventions (`.agents/skills/writing-great-skills/SKILL.md` in the original project). Key patterns:
- Each phase has a clear **completion criterion** that is checkable (not vague).
- **Progressive disclosure** — template files are loaded only when their branch fires, not all at once.
- **Reference** is pushed to sibling files (BRD-TEMPLATE.md, etc.) — SKILL.md contains only the process flow.
- **Leading words** are defined once at the top and reused throughout the text.
