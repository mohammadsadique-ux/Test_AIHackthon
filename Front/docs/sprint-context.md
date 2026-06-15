# Sprint Context

**Sprint [N] — [Sprint Name/Theme]**

| Sprint Number | [N] |
| :---- | :---- |
| **Sprint Goal** | [One clear sentence] |
| **Start Date** | YYYY-MM-DD |
| **End Date** | YYYY-MM-DD |
| **Team Velocity** | [Points/Stories from last sprint] |

---

## Sprint Goal

[Expand on the one-sentence goal with 2-3 sentences providing context about what the team is trying to achieve this sprint and why it matters to the business/product.]

**Success Criteria:**
- [ ] [Measurable outcome 1]
- [ ] [Measurable outcome 2]
- [ ] [Measurable outcome 3]

---

## Key Decisions for This Sprint

[Decisions made during planning that affect how AI agents should execute stories]

### Decision 1: [Title]
- **What:** [The decision]
- **Why:** [Reasoning]
- **Impact on AI:** [How this affects implementation - what AI should do differently]
- **Related:** [Link to ADR if applicable]

### Decision 2: [Title]
- **What:** ...
- **Why:** ...
- **Impact on AI:** ...

**Example:**
### Decision 1: Use Optimistic Locking for Concurrent Updates
- **What:** All entity updates will use version-based optimistic locking
- **Why:** To prevent lost updates when multiple users edit the same resource
- **Impact on AI:** 
  - ALWAYS include version field in update requests
  - HANDLE 409 Conflict responses when version mismatch occurs
  - ADD retry logic with fresh version fetch on conflict
- **Related:** docs/architecture/adr/ADR-015-optimistic-locking.md

---

## Patterns Established Last Sprint (AI Must Follow)

[Patterns that worked well in Sprint N-1 and should be used consistently in Sprint N]

### Pattern 1: [Pattern Name]
- **Description:** [What the pattern is]
- **When to use:** [Scenarios where this applies]
- **Reference implementation:** [File path]
- **Why it matters:** [Impact if not followed]

**Example:**
### Pattern 1: Pagination for List Endpoints
- **Description:** All list endpoints return paginated results with metadata
- **When to use:** Any endpoint returning multiple items
- **Reference implementation:** src/modules/users/user.controller.ts - getUserList()
- **Response format:**
  ```json
  {
    "data": [...],
    "pagination": {
      "page": 1,
      "limit": 50,
      "total": 150,
      "totalPages": 3,
      "hasNext": true,
      "hasPrev": false
    }
  }
  ```
- **Why it matters:** Consistent pagination format across all APIs; frontend expects this exact structure

---

## Things AI Got Wrong Last Sprint (Watch For)

[Common mistakes from Sprint N-1 that need special attention in Sprint N]

### Issue 1: [Description]
- **What happened:** [The mistake AI made]
- **Stories affected:** [Story IDs]
- **Root cause:** [Why AI made this mistake]
- **How to prevent:** [Specific instruction or check]
- **Fixed in:** [copilot-instructions.md update / prompt / story template]

**Example:**
### Issue 1: Currency Format Confusion
- **What happened:** AI stored currency as float (₹ 123.45) instead of integer (12345 paise)
- **Stories affected:** US-085, US-092, US-098
- **Root cause:** copilot-instructions.md didn't specify currency storage format
- **How to prevent:** 
  - ALWAYS store currency amounts as integers in smallest unit (paise, cents, etc.)
  - ADD validation to reject decimal values in currency fields
  - DIVIDE by 100 only when displaying to user
- **Fixed in:** copilot-instructions.md Section 3 - Added "Currency Handling" rule

---

## New Libraries / APIs Introduced This Sprint

[New dependencies or external services being used for the first time]

### Library: [Name]
- **Purpose:** [What it does]
- **Version:** [Version number]
- **When to use:** [Use cases]
- **When NOT to use:** [Scenarios where it shouldn't be used]
- **Key patterns:**
  ```[language]
  // Example usage
  ```
- **Documentation:** [Link]
- **Approved by:** [Architect name, date]

**Example:**
### Library: date-fns
- **Purpose:** Date manipulation and formatting
- **Version:** 2.30.0
- **When to use:** All date calculations, formatting, parsing
- **When NOT to use:** Don't use for timezone-aware calculations (use date-fns-tz)
- **Key patterns:**
  ```javascript
  import { format, addDays, parseISO } from 'date-fns';

  // Format date for display
  const formatted = format(new Date(), 'yyyy-MM-dd');

  // Add days to date
  const futureDate = addDays(new Date(), 7);
  ```
- **Documentation:** https://date-fns.org/
- **Approved by:** John Architect, 2024-01-10

---

## API Contracts Frozen for This Sprint

[API contracts that are locked and cannot be changed during parallel development]

| Contract | Status | Backend Owner | Frontend Owner | Notes |
|----------|--------|---------------|----------------|-------|
| [Service/Feature] | Frozen | [Name] | [Name] | [Any important notes] |

**Example:**
| Contract | Status | Owners | Notes |
|----------|--------|--------|-------|
| User Profile API | Frozen | Backend Team | Frontend Team | Contract in docs/api-contracts/sprint-5-contracts.md |
| Payment Processing | Frozen | Payment Team | Checkout Team | Rate limit: 10 req/min per user |

**Rule:** Frozen contracts cannot be changed without Tech Lead approval and team re-sync.

---

## Architecture Changes This Sprint

[Any architectural changes, new modules, or structural updates]

### Change 1: [Title]
- **What's changing:** [Description]
- **Why:** [Reason]
- **Impact:** [What developers need to know]
- **Migration required:** [Yes/No - if yes, describe]
- **Effective:** [When this takes effect]

**Example:**
### Change 1: New Notification Service Module
- **What's changing:** Extracting all notification logic into separate service module
- **Why:** Multiple features need notifications; centralize to avoid duplication
- **Impact:** 
  - NEW module: src/modules/notifications/
  - DO NOT send emails directly from feature code
  - USE NotificationService.send() for all notifications
- **Migration required:** No (new module, doesn't affect existing code)
- **Effective:** Immediately - all new features must use this

---

## Focus Areas & Priorities

### High Priority
- [Feature/Area 1] - [Why it's high priority]
- [Feature/Area 2] - [Why it's high priority]

### Medium Priority
- [Feature/Area 3]

### Low Priority / Stretch Goals
- [Feature/Area 4]

### Technical Debt This Sprint
- [Debt item 1] - [Estimated effort]
- [Debt item 2] - [Estimated effort]

---

## Dependencies & Blockers

### External Dependencies
| Dependency | Owner | ETA | Status | Mitigation |
|------------|-------|-----|--------|------------|
| [External API/Service] | [Team/Person] | [Date] | [Status] | [Plan if delayed] |

### Cross-Team Dependencies
| Dependent Story | Depends On | Owner | Status | Notes |
|-----------------|------------|-------|--------|-------|
| [Story ID] | [Other Story ID] | [Team] | [Status] | [Notes] |

### Known Blockers
- [Blocker description] - [Owner] - [ETA for resolution]

---

## Testing & Quality Focus

### Test Coverage Targets
- **Unit tests:** ≥ [X]%
- **Integration tests:** [Required/Optional for which features]
- **E2E tests:** [Required for which features]

### Special Testing Considerations
- [Consideration 1 - e.g., "All payment flows must have E2E tests"]
- [Consideration 2 - e.g., "Performance testing required for bulk import feature"]

### Quality Gates
- [ ] All unit tests pass
- [ ] Code coverage ≥ threshold
- [ ] No security vulnerabilities (SAST scan)
- [ ] No critical/blocker code quality issues
- [ ] All API endpoints have contract tests
- [ ] [Additional gate specific to this sprint]

---

## Security & Compliance

### Security Requirements This Sprint
- [Requirement 1]
- [Requirement 2]

### Compliance Considerations
- [GDPR / PCI-DSS / HIPAA / etc. - specific requirements]

### Security Review Required For
- [Feature 1 - e.g., "Payment processing stories"]
- [Feature 2 - e.g., "User data export feature"]

---

## Performance Requirements

### Performance Targets
| Feature | Metric | Target | How Measured |
|---------|--------|--------|--------------|
| [Feature] | [Metric] | [Target] | [Tool/Method] |

**Example:**
| Feature | Metric | Target | How Measured |
|---------|--------|--------|--------------|
| Search API | P95 response time | < 150ms | APM tool |
| Report generation | Max time | < 5s | Manual testing |

---

## Monitoring & Observability

### New Metrics to Track
- [Metric 1 - what to measure and why]
- [Metric 2]

### New Alerts to Configure
- [Alert 1 - condition and threshold]
- [Alert 2]

### Dashboards to Update
- [Dashboard 1 - what to add]

---

## Team Capacity & Availability

### Team Composition
- **Developers:** [Count]
- **Tech Lead:** [Name]
- **Architect:** [Name (% availability)]

### Planned Absences
- [Name] - [Dates] - [Impact]

### Adjusted Velocity
- **Standard velocity:** [Points/Stories]
- **This sprint:** [Adjusted number]
- **Reason:** [Why different]

---

## Sprint Rituals & Meetings

### Daily Standup
- **Time:** [Time]
- **Duration:** 15 minutes
- **Focus:** Blockers, dependencies, AI agent issues

### Mid-Sprint Check-in
- **When:** [Day/Date]
- **Purpose:** Progress review, adjust if needed

### Sprint Review
- **When:** [Day/Date]
- **Attendees:** [List]
- **Demos:** [What will be demonstrated]

### Sprint Retrospective
- **When:** [Day/Date]
- **Focus:** AI agent maturity, prompt effectiveness, story quality

---

## AI Agent Metrics Target This Sprint

| Metric | Last Sprint | Target This Sprint |
|--------|-------------|-------------------|
| % AI-completed stories (no manual fix) | [X]% | [Y]% |
| Avg corrections per story | [X] | [Y] |
| Stories requiring manual code | [X]% | [Y]% |
| % stories completed in one pass | [X]% | [Y]% |

---

## Known Issues & Workarounds

### Issue 1: [Description]
- **Impact:** [Who/what is affected]
- **Workaround:** [Temporary solution]
- **Permanent fix:** [Planned solution and ETA]

---

## Resources & References

### Documentation Updated This Sprint
- [Document 1] - [What changed]
- [Document 2] - [What changed]

### External Resources
- [Resource 1] - [Description and link]
- [Resource 2] - [Description and link]

### Training Materials
- [Topic 1] - [Link to training]

---

## Notes from Sprint Planning

[Any additional context, decisions, or discussions from planning that don't fit above categories]

---

## Sprint Retrospective (End of Sprint)

[This section is filled at sprint end during retrospective]

### What Went Well
- [Success 1]
- [Success 2]

### What Needs Improvement
- [Issue 1]
- [Issue 2]

### Action Items for Next Sprint
- [ ] [Action 1] - Owner: [Name]
- [ ] [Action 2] - Owner: [Name]

### AI Agent Maturity
- **Actual % AI-completed:** [X]%
- **copilot-instructions.md updates:** [Count - brief description]
- **Prompt library additions:** [Count - brief description]
- **Key learning:** [Most important takeaway about AI effectiveness]

---

## Document History

| Date | Author | Changes |
|------|--------|---------|
| YYYY-MM-DD | [Name] | Sprint [N] context created |
| YYYY-MM-DD | [Name] | Updated with mid-sprint changes |
| YYYY-MM-DD | [Name] | Sprint retrospective added |

---

## Related Documents

- `.github/copilot-instructions.md` - Project-wide AI rules
- `.github/project-architecture.md` - Architecture design
- `docs/user-stories/` - Stories for this sprint
- `docs/api-contracts/` - API contracts frozen for this sprint
- `docs/prompt-library.md` - Reusable prompts
- `docs/agent-feedback/sprint-[N]/` - Feedback logs
- `docs/architecture/adr/` - Architecture decisions

---

## Quick Reference for Developers

**Before starting any story today:**
1. ✅ Read this sprint context file
2. ✅ Note any new patterns to follow
3. ✅ Check "Things AI Got Wrong" section
4. ✅ Verify your story references any new libraries correctly
5. ✅ Check dependencies/blockers section

**Red flags - escalate immediately:**
- 🚨 Story depends on blocked item
- 🚨 Need to change a frozen API contract
- 🚨 AI repeatedly fails on pattern from "Things AI Got Wrong"
- 🚨 Discovered security issue
