# ADR-000: Template for Architecture Decision Records

**Date:** YYYY-MM-DD  
**Status:** Template  
**Deciders:** [Names of decision makers]  
**Technical Story:** [Link to user story, epic, or issue]

---

## Context

[Describe the context and background that led to this decision. What is the issue or problem we're facing? What factors and constraints are driving this decision?]

**Example:**
> We need to choose a database system for our new microservices architecture. The system must handle 10,000 transactions per second, support ACID compliance for financial data, and scale horizontally. Our team has experience with both PostgreSQL and MongoDB.

---

## Decision

[State the decision clearly and concisely. What is the change we're proposing or have agreed to implement?]

**Example:**
> We will use PostgreSQL as our primary database system for all microservices that require transactional consistency.

---

## Reasoning

[Explain why this decision was made. What are the key factors that led to choosing this option?]

**Example:**
> - PostgreSQL provides ACID compliance required for financial transactions
> - Our team has 5+ years of production experience with PostgreSQL
> - Excellent support for complex queries and reporting requirements
> - Strong ecosystem and community support
> - Built-in replication and high availability features

---

## Alternatives Considered

### Alternative 1: [Name]
**Description:** [Brief description]  
**Pros:**
- [Advantage 1]
- [Advantage 2]

**Cons:**
- [Disadvantage 1]
- [Disadvantage 2]

**Why Rejected:** [Explanation]

### Alternative 2: [Name]
**Description:** [Brief description]  
**Pros:**
- [Advantage 1]

**Cons:**
- [Disadvantage 1]

**Why Rejected:** [Explanation]

---

## Constraints for AI

[THIS IS THE MOST CRITICAL SECTION - Explicit rules for AI agents to follow]

**Format: Use clear, actionable rules**

- **ALWAYS** [specific action the AI must take]
- **NEVER** [specific action the AI must avoid]
- **WHEN** [condition] **THEN** [action]
- **ALL** [entity type] **MUST** [requirement]

**Example:**
```markdown
## Constraints for AI
- ALWAYS use parameterized queries when interacting with PostgreSQL
- NEVER use string concatenation to build SQL queries
- WHEN creating a new database table THEN include a migration script with both up() and down() methods
- ALL database connection strings MUST be stored in Azure Key Vault, never in configuration files
- ALWAYS use connection pooling with minimum 5 and maximum 20 connections per service
- WHEN handling database errors THEN catch specific exceptions (e.g., UniqueViolationError) not generic Exception
- ALL tables MUST have a primary key named 'id' of type UUID
- NEVER expose database error details to API responses (map to generic error codes)
```

---

## Consequences

### Positive
- [Benefit 1]
- [Benefit 2]
- [Benefit 3]

### Negative
- [Trade-off 1]
- [Trade-off 2]

### Risks and Mitigation
| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| [Risk description] | [High/Medium/Low] | [High/Medium/Low] | [How we'll address it] |

---

## Implementation Notes

[Technical details about how this decision should be implemented. Include links to documentation, configuration examples, or code patterns.]

**Example:**
```
Configuration pattern:
- Use Sequelize ORM for PostgreSQL access
- Connection string stored in Azure Key Vault reference: ${KeyVault:DbConnectionString}
- Migration files in src/migrations/ using naming: YYYYMMDDHHMMSS-description.js
```

---

## Related Decisions

- [ADR-XXX]: [Related decision title] - [Brief explanation of relationship]
- [ADR-YYY]: [Another related decision]

---

## References

- [Link to documentation]
- [Link to proof of concept]
- [Link to benchmark results]
- [Link to team discussion]

---

## Revision History

| Date | Author | Change |
|------|--------|--------|
| YYYY-MM-DD | [Name] | Initial creation |
| YYYY-MM-DD | [Name] | Updated status to Accepted |

---

## Notes for Architects

### Before Creating an ADR:
1. ✅ Is this a significant architectural decision?
2. ✅ Will this affect multiple teams or sprints?
3. ✅ Does this need team consensus?
4. ✅ Will AI agents need to follow specific rules based on this?

### Writing "Constraints for AI" Section:
- Be specific and actionable (not "consider using X" but "ALWAYS use X when Y")
- Use consistent keywords: ALWAYS, NEVER, WHEN...THEN, ALL...MUST
- Include concrete examples where helpful
- Think: "What would prevent an AI from making the wrong choice?"
- Test: "Could an AI agent follow this rule without human judgment?"

### After ADR is Accepted:
1. ✅ Update `.github/copilot-instructions.md` if rules apply globally
2. ✅ Update `.github/project-architecture.md` if it affects architecture overview
3. ✅ Add reference in relevant user story templates
4. ✅ Communicate to Tech Leads and Developers
5. ✅ Add to ADR index in docs/architecture/adr/README.md
