# AI-Driven Development - Complete Documentation Index

**Navigation guide for all project documentation**

---

## 📋 Start Here

| Document | Purpose | Audience |
|----------|---------|----------|
| **SETUP-COMPLETE.md** | Overview and next steps | All roles - read first |
| **QUICK-REFERENCE.md** | One-page cheat sheet | All roles - keep handy |
| **FOLDER-STRUCTURE.md** | Complete structure overview | All roles - reference |

---

## 🎯 By Role

### 👔 Architects
**Primary Documents:**
1. `.github/copilot-instructions.md` - AI behavior rules (maintain)
2. `.github/project-architecture.md` - Architecture design (maintain)
3. `docs/architecture/adr/` - Architecture decisions (create)

**Reference:**
- `docs/architecture/adr/README.md` - ADR guidelines
- `docs/architecture/adr/ADR-000-template.md` - ADR template
- `docs/architecture/diagrams/README.md` - Diagram guidelines

**Training:**
- SOP Section 8.1 - Architect SOP
- Training Manual Module B1 - Designing Agent Systems
- Training Manual Module D1 - Token Governance

### 🎓 Technical Leads
**Primary Documents:**
1. `docs/sprint-context.md` - Current sprint context (update per sprint)
2. `docs/user-stories/` - AI-ready stories (create per story)
3. `docs/prompt-library.md` - Reusable prompts (maintain)
4. `docs/api-contracts/` - API specifications (create/freeze)

**Reference:**
- `docs/user-stories/README.md` - Story authoring guidelines
- `docs/user-stories/story-template.md` - Story template
- `docs/api-contracts/README.md` - Contract guidelines
- `docs/agent-feedback/README.md` - Feedback analysis process

**Training:**
- SOP Section 8.2 - Technical Lead SOP
- Training Manual Module A2 - Planning with Copilot
- Training Manual Module B2 - Building Agent Toolkit
- Training Manual Module C2 - Orchestrating the Sprint

### 💻 Developers
**Primary Documents:**
1. `docs/sprint-context.md` - Read daily
2. `docs/user-stories/current-sprint/` - Your assigned stories
3. `docs/prompt-library.md` - Effective prompts to use
4. `docs/agent-feedback/sprint-N/` - Submit after each story

**Reference:**
- `docs/user-stories/README.md` - Pre-execution ritual
- `docs/agent-feedback/feedback-template.md` - Feedback template
- `.github/copilot-instructions.md` - Project rules

**Training:**
- SOP Section 8.3 - Developer SOP
- Training Manual Module B3 - Operating Agents
- Training Manual Module C3 - Your Role in Orchestration
- Training Manual Module D3 - Token Efficiency

---

## 📚 By Document Type

### Configuration Files
| File | Purpose | Owner | Update Frequency |
|------|---------|-------|------------------|
| `.github/copilot-instructions.md` | AI behavior rules | Architect | Per sprint / monthly |
| `.github/project-architecture.md` | Architecture design | Architect | Monthly / as needed |

### Architecture Documentation
| File/Folder | Purpose | Owner | Update Frequency |
|-------------|---------|-------|------------------|
| `docs/architecture/adr/` | Architecture decisions | Architect | Per major decision |
| `docs/architecture/adr/README.md` | ADR guidelines | Architect | Rarely |
| `docs/architecture/adr/ADR-000-template.md` | ADR template | Architect | Rarely |
| `docs/architecture/diagrams/` | Visual architecture | Architect | Per architectural change |

### API Contracts
| File/Folder | Purpose | Owner | Update Frequency |
|-------------|---------|-------|------------------|
| `docs/api-contracts/README.md` | Contract guidelines | Tech Lead | Rarely |
| `docs/api-contracts/sprint-N-contracts.md` | Sprint contracts | Tech Lead | Per sprint |
| `docs/api-contracts/[service]-api-contract.md` | Service contracts | Tech Lead | As needed |

### User Stories
| File/Folder | Purpose | Owner | Update Frequency |
|-------------|---------|-------|------------------|
| `docs/user-stories/README.md` | Story guidelines | Tech Lead | Quarterly |
| `docs/user-stories/story-template.md` | Story template | Tech Lead | Per improvement |
| `docs/user-stories/current-sprint/` | Active stories | Tech Lead | Per sprint |
| `docs/user-stories/next-sprint/` | Prepared stories | Tech Lead | Sprint planning |
| `docs/user-stories/backlog/` | Future stories | Tech Lead | As needed |

### Agent Feedback
| File/Folder | Purpose | Owner | Update Frequency |
|-------------|---------|-------|------------------|
| `docs/agent-feedback/README.md` | Feedback guidelines | Tech Lead | Rarely |
| `docs/agent-feedback/feedback-template.md` | Feedback template | Tech Lead | Rarely |
| `docs/agent-feedback/overrides.md` | Manual code log | Developer/Tech Lead | Per override |
| `docs/agent-feedback/sprint-N/` | Sprint feedback | Developer | Per story |
| `docs/agent-feedback/analysis/` | Retrospectives | Tech Lead | Per sprint |

### Operational Documents
| File | Purpose | Owner | Update Frequency |
|------|---------|-------|------------------|
| `docs/prompt-library.md` | Reusable prompts | Tech Lead | Weekly/per sprint |
| `docs/sprint-context.md` | Current sprint context | Tech Lead | Per sprint |

### Reference Documentation
| File | Purpose | Audience | When to Read |
|------|---------|----------|--------------|
| `SETUP-COMPLETE.md` | Setup overview | All | After initial setup |
| `QUICK-REFERENCE.md` | Cheat sheet | All | Keep handy |
| `FOLDER-STRUCTURE.md` | Structure guide | All | Reference as needed |
| `INDEX.md` | This file | All | Navigation |

---

## 🔍 By Activity

### Setting Up a New Project
1. Read `SETUP-COMPLETE.md`
2. Fill in `.github/copilot-instructions.md`
3. Fill in `.github/project-architecture.md`
4. Create initial ADRs in `docs/architecture/adr/`
5. Seed `docs/prompt-library.md`
6. Validate with team

### Starting a New Sprint
1. Update `docs/sprint-context.md` (Tech Lead)
2. Create stories in `docs/user-stories/current-sprint/` (Tech Lead)
3. Create/freeze API contracts in `docs/api-contracts/` (Tech Lead)
4. Team reviews sprint plan

### Executing a Story
1. Read `docs/sprint-context.md` (Developer)
2. Read story in `docs/user-stories/current-sprint/` (Developer)
3. Use prompts from `docs/prompt-library.md` (Developer)
4. Execute with AI agent (Developer)
5. Submit feedback to `docs/agent-feedback/sprint-N/` (Developer)

### Conducting Sprint Retrospective
1. Collect feedback from `docs/agent-feedback/sprint-N/` (Tech Lead)
2. Run analysis (use prompt 5.1 from `docs/prompt-library.md`) (Tech Lead)
3. Create retrospective in `docs/agent-feedback/analysis/` (Tech Lead)
4. Update `docs/prompt-library.md` (Tech Lead)
5. Submit updates to `.github/copilot-instructions.md` (Tech Lead → Architect review)

### Onboarding New Team Member
1. Read `SETUP-COMPLETE.md`
2. Read `.github/copilot-instructions.md`
3. Read `.github/project-architecture.md` overview
4. Review last 3 ADRs
5. Read current `docs/sprint-context.md`
6. Review top 5 prompts in `docs/prompt-library.md`
7. Shadow a story execution
8. Execute first story with supervision

### Creating an ADR
1. Read `docs/architecture/adr/README.md`
2. Copy `docs/architecture/adr/ADR-000-template.md`
3. Fill in all sections (especially "Constraints for AI")
4. Submit for Architect review
5. Update index in `docs/architecture/adr/README.md`

### Creating an API Contract
1. Read `docs/api-contracts/README.md`
2. Use template from README
3. Fill in all endpoints, request/response schemas
4. Include "Constraints for AI" section
5. Mark as "Frozen" before parallel work starts
6. Enforce freeze protocol during sprint

---

## 🎓 Training Resources

### Standard Operating Procedure
- **File:** `SOP-AI-Driven-Development_document.md`
- **Sections:**
  - Section 3: Roles & Responsibilities (RACI matrix)
  - Section 4: System Architecture Overview
  - Section 5: AI Agent Design
  - Section 6: End-to-End Development Workflow
  - Section 7: User Story Lifecycle
  - Section 8: Role-Specific SOPs (Architect, Tech Lead, Developer)
  - Section 10: Quality Gates
  - Section 11: Continuous Learning
  - Section 12: Metrics & Success Criteria

### Training Manual
- **File:** `AI-Development-Training-Manual.md`
- **Modules:**
  - Module A: Good Planning in GitHub Copilot
  - Module B: Developing AI Agents
  - Module C: Agent Orchestration
  - Module D: Optimising Token Spend
  - Final Assessment

---

## 📊 Metrics & Reporting

### Sprint Metrics (Track in `docs/sprint-context.md`)
- % AI-completed stories (target: ≥ 70%)
- Average corrections per story (target: < 2)
- Stories requiring manual code (target: < 10%)
- Stories completed in one pass (target: ≥ 70%)

### Documentation Health (Architect responsibility)
- copilot-instructions.md token count (target: < 1,500)
- ADRs with "Constraints for AI" (target: 100%)
- Stories AI-ready before assignment (target: 100%)
- Feedback logs submitted (target: 100%)

### Improvement Trends (Track sprint-over-sprint)
- AI effectiveness increasing
- Correction count decreasing
- Manual overrides decreasing
- Token efficiency improving

---

## 🔗 Document Relationships

```
copilot-instructions.md (Global Rules)
         ↓ informs
project-architecture.md (Architecture Design)
         ↓ referenced by
ADRs (Specific Decisions)
         ↓ referenced by
sprint-context.md (Sprint Context)
         ↓ provides context for
user-stories/*.md (Task Definition)
         ↓ executed using
prompt-library.md (Execution Patterns)
         ↓ produces
agent-feedback/*.md (Learnings)
         ↓ improves (feedback loop)
copilot-instructions.md (Updated Rules)
```

---

## ✅ Document Maintenance Schedule

### Daily
- Read `docs/sprint-context.md` (Developers)

### Per Story
- Create AI-ready story in `docs/user-stories/` (Tech Lead)
- Submit feedback in `docs/agent-feedback/` (Developer)

### Weekly
- Review feedback patterns (Tech Lead)
- Update `docs/prompt-library.md` if needed (Tech Lead)

### End of Sprint
- Retrospective analysis (Tech Lead)
- Update all docs based on learnings (Tech Lead + Architect)
- Update `docs/sprint-context.md` for next sprint (Tech Lead)

### Monthly
- Architecture health check (Architect)
- Review ADRs (Architect)
- Token budget review (Architect)
- Prune stale documentation (All)

### Quarterly
- Major prompt library revision (Tech Lead)
- Comprehensive copilot-instructions.md review (Architect)
- Team training on new patterns (Tech Lead)

---

## 🆘 Quick Help

**Can't find something?** Use this table:

| Looking for... | Check... |
|----------------|----------|
| AI behavior rules | `.github/copilot-instructions.md` |
| Architecture design | `.github/project-architecture.md` |
| Current sprint info | `docs/sprint-context.md` |
| A specific story | `docs/user-stories/current-sprint/` |
| How to write a prompt | `docs/prompt-library.md` |
| How to give feedback | `docs/agent-feedback/README.md` |
| API contract format | `docs/api-contracts/README.md` |
| ADR format | `docs/architecture/adr/ADR-000-template.md` |
| Story format | `docs/user-stories/story-template.md` |
| Your role's tasks | `QUICK-REFERENCE.md` |
| Setup instructions | `SETUP-COMPLETE.md` |
| Folder overview | `FOLDER-STRUCTURE.md` |

---

## 📞 Support Contacts

- **Architecture Questions:** [Architect Name/Contact]
- **Process Questions:** [Tech Lead Name/Contact]
- **Tool Issues:** [DevOps/Tools Team]
- **Training Requests:** [Training Coordinator]
- **Documentation Issues:** [Documentation Owner]

---

**Document Version:** 1.0  
**Created:** [DATE]  
**Maintained By:** Architecture Team  
**Next Review:** [DATE]

---

**Navigation:** [Top](#) | [By Role](#-by-role) | [By Type](#-by-document-type) | [By Activity](#-by-activity) | [Training](#-training-resources)
