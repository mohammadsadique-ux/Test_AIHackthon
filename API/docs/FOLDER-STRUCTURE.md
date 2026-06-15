# Folder Structure Overview

This document provides an overview of the complete folder structure for AI-driven development.

```
project-root/
│
├── .github/                                    # GitHub Copilot configuration
│   ├── copilot-instructions.md                # AI behavior rules and coding standards
│   └── project-architecture.md                # Detailed architecture design
│
├── docs/                                       # All project documentation
│   ├── README.md                              # Documentation guide
│   │
│   ├── architecture/                          # Architecture documentation
│   │   ├── adr/                               # Architecture Decision Records
│   │   │   ├── README.md                      # ADR guidelines and index
│   │   │   ├── ADR-000-template.md            # Template for new ADRs
│   │   │   └── ADR-001-xxx.md                 # Actual ADRs
│   │   │
│   │   └── diagrams/                          # Architecture diagrams
│   │       ├── README.md                      # Diagram guidelines
│   │       ├── system-context/                # High-level context diagrams
│   │       ├── containers/                    # Container/service diagrams
│   │       ├── components/                    # Component-level diagrams
│   │       ├── deployment/                    # Infrastructure diagrams
│   │       ├── data-flow/                     # Data flow diagrams
│   │       ├── integration/                   # Integration patterns
│   │       └── security/                      # Security architecture
│   │
│   ├── api-contracts/                         # API specifications
│   │   ├── README.md                          # Contract guidelines and templates
│   │   ├── sprint-N-contracts.md              # Sprint-specific frozen contracts
│   │   └── [service]-api-contract.md          # Individual service contracts
│   │
│   ├── user-stories/                          # AI-ready user stories
│   │   ├── README.md                          # Story authoring guidelines
│   │   ├── story-template.md                  # Template for new stories
│   │   ├── current-sprint/                    # Active sprint stories
│   │   │   ├── story-US-100.md
│   │   │   └── story-US-101.md
│   │   ├── next-sprint/                       # Prepared stories
│   │   └── backlog/                           # Future stories
│   │
│   ├── agent-feedback/                        # AI execution feedback
│   │   ├── README.md                          # Feedback guidelines
│   │   ├── feedback-template.md               # Template for feedback logs
│   │   ├── overrides.md                       # Manual code override tracking
│   │   ├── sprint-1/                          # Sprint 1 feedback
│   │   │   ├── story-US-100-feedback.md
│   │   │   └── story-US-101-feedback.md
│   │   ├── sprint-2/                          # Sprint 2 feedback
│   │   └── analysis/                          # Retrospective analysis
│   │       ├── sprint-1-retrospective.md
│   │       └── sprint-2-retrospective.md
│   │
│   ├── prompt-library.md                      # Reusable validated prompts
│   └── sprint-context.md                      # Current sprint goals and context
│
├── src/                                        # Source code
│   └── [your application structure]
│
└── tests/                                      # Test files
    ├── unit/
    ├── integration/
    └── e2e/
```

## Key Files by Role

### Architect
**Primary responsibilities:**
- `.github/copilot-instructions.md` - Author and maintain
- `.github/project-architecture.md` - Author and maintain
- `docs/architecture/adr/` - Create ADRs for major decisions
- `docs/architecture/diagrams/` - Create and update diagrams

**Review frequency:**
- Before each sprint (update for new features)
- Monthly (architecture health check)
- When major architectural decisions are made

### Technical Lead
**Primary responsibilities:**
- `docs/user-stories/` - Transform raw stories to AI-ready format
- `docs/prompt-library.md` - Maintain and update prompts
- `docs/sprint-context.md` - Update before each sprint
- `docs/api-contracts/` - Create and freeze contracts
- `docs/agent-feedback/analysis/` - Conduct retrospectives

**Review frequency:**
- Daily (sprint-context.md)
- Per story (create AI-ready stories)
- End of sprint (retrospective analysis)
- Weekly (prompt library updates)

### Developer
**Primary responsibilities:**
- `docs/user-stories/` - Read and verify before execution
- `docs/sprint-context.md` - Read daily
- `docs/agent-feedback/` - Submit feedback after every story
- `docs/prompt-library.md` - Reference for effective prompts

**Review frequency:**
- Daily (sprint-context.md)
- Before each story (user story file)
- After each story (submit feedback)
- Weekly (review prompt library for new patterns)

## File Relationships

```
copilot-instructions.md (GLOBAL RULES)
         ↓
         ↓ informs
         ↓
project-architecture.md (ARCHITECTURE DESIGN)
         ↓
         ↓ referenced by
         ↓
sprint-context.md (SPRINT-SPECIFIC CONTEXT)
         ↓
         ↓ provides context for
         ↓
user-stories/*.md (TASK DEFINITION)
         ↓
         ↓ executed using
         ↓
prompt-library.md (EXECUTION PATTERNS)
         ↓
         ↓ produces
         ↓
agent-feedback/*.md (LEARNINGS)
         ↓
         ↓ improves (feedback loop)
         ↓
copilot-instructions.md (UPDATED RULES)
```

## Workflow by Phase

### Phase 1: Project Setup (One-time)
1. **Architect** fills in `.github/copilot-instructions.md`
2. **Architect** fills in `.github/project-architecture.md`
3. **Architect** creates initial ADRs
4. **Tech Lead** seeds `docs/prompt-library.md` with initial prompts
5. **Team** reviews and validates setup

### Phase 2: Sprint Planning
1. **Tech Lead** updates `docs/sprint-context.md`
2. **Tech Lead** creates AI-ready stories in `docs/user-stories/current-sprint/`
3. **Architect** reviews architecture impact
4. **Tech Lead** creates/freezes API contracts in `docs/api-contracts/`
5. **Team** reviews sprint plan

### Phase 3: Sprint Execution
1. **Developer** reads `docs/sprint-context.md` daily
2. **Developer** reads story from `docs/user-stories/current-sprint/`
3. **Developer** uses prompts from `docs/prompt-library.md`
4. **Developer** executes with AI agent
5. **Developer** submits feedback to `docs/agent-feedback/sprint-N/`

### Phase 4: Sprint Retrospective
1. **Tech Lead** collects all feedback from `docs/agent-feedback/sprint-N/`
2. **Tech Lead** runs retrospective analysis (see prompt-library.md)
3. **Tech Lead** creates `docs/agent-feedback/analysis/sprint-N-retrospective.md`
4. **Tech Lead** updates `docs/prompt-library.md`
5. **Architect** reviews and approves updates to `.github/copilot-instructions.md`
6. **Team** discusses learnings and improvements

## Maintenance Schedule

### Daily
- [ ] Read `docs/sprint-context.md` (Developers)

### Per Story
- [ ] Create AI-ready story (Tech Lead)
- [ ] Submit feedback log (Developer)

### Weekly
- [ ] Review new feedback patterns (Tech Lead)
- [ ] Update prompt library if patterns emerge (Tech Lead)

### End of Sprint
- [ ] Conduct retrospective analysis (Tech Lead)
- [ ] Update all documentation based on learnings (Tech Lead + Architect)
- [ ] Update sprint-context.md for next sprint (Tech Lead)

### Monthly
- [ ] Architecture health check (Architect)
- [ ] Review and prune ADRs (Architect)
- [ ] Review token efficiency metrics (Architect)
- [ ] Update project-architecture.md (Architect)

### Quarterly
- [ ] Major prompt library revision (Tech Lead)
- [ ] copilot-instructions.md comprehensive review (Architect)
- [ ] Team training on new patterns (Tech Lead)

## Success Metrics by Document

| Document | Success Metric | How to Measure |
|----------|----------------|----------------|
| copilot-instructions.md | AI follows rules without violation | Feedback logs show <5 rule violations/sprint |
| project-architecture.md | Architecture drift minimal | PR reviews catch <3 boundary violations/sprint |
| sprint-context.md | Team aware of context | Survey: >90% read it before starting work |
| user-stories/*.md | Stories are AI-ready | <2 corrections needed due to missing context |
| prompt-library.md | Prompts are effective | >80% success rate for library prompts |
| agent-feedback/*.md | Feedback drives improvement | Measurable improvement in AI metrics sprint-over-sprint |

## Common Pitfalls

### Pitfall 1: Stale Documentation
**Problem:** Documents not updated, AI acts on outdated information  
**Solution:** Mandatory review schedule per role

### Pitfall 2: Missing Feedback
**Problem:** Developers skip feedback logs, no learning happens  
**Solution:** Feedback log required in Definition of Done

### Pitfall 3: Verbose copilot-instructions.md
**Problem:** File exceeds 2000 tokens, dilutes important rules  
**Solution:** Monthly pruning, move history to ADRs

### Pitfall 4: Poor Story Quality
**Problem:** Stories lack technical context, AI guesses wrong  
**Solution:** Tech Lead uses 3-prompt refinement process (see user-stories/README.md)

### Pitfall 5: Frozen Contracts Ignored
**Problem:** Developers change API contracts during parallel work  
**Solution:** Tech Lead enforces freeze protocol strictly

## Quick Start Checklist

**For new team members:**
- [ ] Read `.github/copilot-instructions.md` completely
- [ ] Read `.github/project-architecture.md` overview
- [ ] Review last 3 ADRs in `docs/architecture/adr/`
- [ ] Read current `docs/sprint-context.md`
- [ ] Review `docs/prompt-library.md` top 5 prompts
- [ ] Shadow a story execution (read story + feedback)
- [ ] Execute first story with Tech Lead supervision
- [ ] Submit first feedback log
- [ ] Ready for independent work ✅

## Related Documents

- **SOP-AI-Driven-Development.md** - Full standard operating procedure
- **AI-Development-Training-Manual.md** - Self-learning training program
- `.github/copilot-instructions.md` - AI behavior configuration
- `.github/project-architecture.md` - Architecture design

## Questions?

- **Architectural questions:** Contact [Architect Name]
- **Process questions:** Contact [Tech Lead Name]
- **Tool issues:** Contact [DevOps/Tools Team]
- **Feedback/Improvements:** Submit via [process - Slack channel / email / etc.]
