# Architecture Decision Records (ADR)

This directory contains all Architecture Decision Records for the project.

## What is an ADR?

An Architecture Decision Record (ADR) documents an important architectural decision, the context that led to it, and the consequences of the decision. In AI-driven development, ADRs are critical because they inform AI agents about past decisions and constraints.

## ADR Lifecycle

```
[Proposed] → [Accepted] → [Implemented] → [Superseded/Deprecated]
```

## Naming Convention

ADRs are numbered sequentially and use kebab-case:

```
ADR-001-use-postgresql-database.md
ADR-002-implement-jwt-authentication.md
ADR-003-adopt-clean-architecture-pattern.md
```

## Index of ADRs

| ADR # | Title | Status | Date | Owner |
|-------|-------|--------|------|-------|
| [001](./ADR-001-example.md) | Example ADR Template | Proposed | YYYY-MM-DD | [Name] |

*Add new ADRs to this index table when created*

## ADR Template

Copy `ADR-000-template.md` to create a new ADR.

## Critical Section: "Constraints for AI"

Every ADR MUST include a "Constraints for AI" section. This is what makes an ADR actionable for AI agents.

**Good Example:**
```markdown
## Constraints for AI
- ALWAYS use the PaymentService wrapper class when processing payments
- NEVER call the Stripe SDK directly from controllers or services
- WHEN handling payment errors THEN use PaymentException with specific error codes
- ALL payment amounts MUST be stored in the smallest currency unit (paise, not rupees)
```

**Poor Example:**
```markdown
## Constraints for AI
- Consider using the payment service
- Be careful with payment processing
```

## Review Process

1. **Author** creates ADR and commits with status "Proposed"
2. **Architect** reviews and discusses with team
3. **Team** agrees or proposes alternatives
4. **Architect** updates status to "Accepted" and date
5. **Implementation** team references ADR during development
6. **Retrospective** check if ADR needs updates

## When to Create an ADR

Create an ADR when:
- Choosing between architectural patterns
- Selecting major libraries or frameworks
- Defining integration patterns with external systems
- Establishing security or compliance approaches
- Making technology stack decisions
- Defining data architecture patterns
- Establishing module boundaries
- Making decisions that affect multiple teams/sprints

## When NOT to Create an ADR

Do NOT create an ADR for:
- Minor implementation details
- Decisions that only affect a single story
- Temporary workarounds
- Styling or naming conventions (use copilot-instructions.md instead)
- Sprint-specific tactical decisions

## Related Documents

- `.github/copilot-instructions.md` - AI behavior and coding standards
- `.github/project-architecture.md` - Overall architecture design
- `docs/sprint-context.md` - Current sprint context
