# Documentation Directory

This directory contains all project documentation for AI-driven development.

## Directory Structure

```
docs/
├── architecture/           # Architecture documentation and decisions
│   ├── adr/               # Architecture Decision Records
│   └── diagrams/          # Architecture diagrams and visuals
├── api-contracts/         # API specifications and contracts
├── user-stories/          # AI-ready user story files
├── agent-feedback/        # Feedback logs from AI agent executions
│   └── sprint-[N]/        # Per-sprint feedback organization
├── prompt-library.md      # Reusable validated prompts
└── sprint-context.md      # Current sprint goals and context
```

## Key Files

### sprint-context.md
Updated before each sprint. Contains:
- Sprint goal
- Key decisions for this sprint
- Patterns established last sprint
- Issues AI got wrong (to watch for)
- New libraries/APIs introduced

### prompt-library.md
Collection of validated, reusable prompts organized by category:
1. Feature Implementation
2. Bug & Diagnosis
3. Refactoring
4. Code Review
5. Sprint Operations

## Usage Guidelines

### For Architects
- Create ADRs in `architecture/adr/` for all major decisions
- Update architecture diagrams in `architecture/diagrams/`
- Review and approve all architectural documentation

### For Technical Leads
- Author AI-ready user stories in `user-stories/`
- Maintain and update `prompt-library.md`
- Update `sprint-context.md` before each sprint
- Consolidate feedback from `agent-feedback/` during retrospectives

### For Developers
- Read `sprint-context.md` at the start of each day
- Submit feedback logs to `agent-feedback/sprint-[N]/` after every story
- Reference `prompt-library.md` for validated prompt patterns
- Use API contracts from `api-contracts/` for parallel development

## Document Naming Conventions

- **ADRs:** `ADR-[NNN]-[kebab-case-title].md`
- **User Stories:** `story-[ID].md`
- **API Contracts:** `sprint-[N]-contracts.md` or `[service-name]-api-contract.md`
- **Feedback Logs:** `story-[ID]-feedback.md`
- **Diagrams:** `[diagram-name]-[YYYY-MM-DD].png` or `.svg`

## Maintenance Schedule

- **Daily:** Read sprint-context.md
- **Per Story:** Submit feedback log
- **Weekly:** Tech Lead reviews feedback patterns
- **End of Sprint:** Retrospective updates prompt library and sprint context
- **Monthly:** Architect reviews and prunes ADRs and architecture docs
