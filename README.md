# Requirements Blueprinting

A skill for AI agents to produce predictable, structured requirements documents — **BRD** (Business Requirement Document), **FSD** (Functional Specification Document), and **TSD** (Technical Design Document) — from project context.

## Structure

```
skills/
└── requirements-blueprinting/
    ├── SKILL.md           # Main skill — model-invoked, 4-phase process, branching
    ├── BRD-TEMPLATE.md    # BRD blueprint reference (13 sections with interview guidance)
    ├── FSD-TEMPLATE.md    # FSD blueprint (process flows, business rules, UI, NFRs)
    ├── TSD-TEMPLATE.md    # TSD blueprint (architecture, DB, API, security, deployment)
    └── GLOSSARY.md        # Single source: ID convention, traceability, boilerplate
```

## Usage

Copy the `skills/requirements-blueprinting/` directory into the target project's `.agents/skills/` directory. The agent discovers it automatically.

Or invoke by name: `requirements-blueprinting`

### Branches

| Branch | Output |
|--------|--------|
| BRD | Business context, objectives, scope, risks, success metrics, use cases |
| FSD | Functional behavior, user roles, process flows, screen designs, business rules, NFRs |
| TSD | System architecture, data model, API contracts, security, deployment, infrastructure |

## Process

Every branch runs four phases:

1. **Excavation** — scan repo + interview user on gaps (hypothesis + confidence, one-at-a-time, restate-and-confirm)
2. **Blueprint** — load template, build document skeleton, initialize ID counters
3. **Composition** — fill each section, assign traceability IDs, embed Mermaid diagrams
4. **Craftsmanship** — traceability scan, coverage check, formatting pass, language consistency

## ID Convention

| Prefix | Stands For |
|--------|------------|
| BO-# | Business Objective |
| SM-# | Success Metric |
| RI-# | Risk |
| AS-# | Assumption |
| DE-# | Dependency |
| FE-# | Feature |
| LI-# | Limitation / Exclusion |
| UC-# | Use Case |

## License

MIT
