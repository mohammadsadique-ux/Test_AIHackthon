# AI-Driven Development - Quick Reference Card

**One-page guide for all roles**

---

## 🏗️ Architect Quick Reference

### Your Core Files
- `.github/copilot-instructions.md` - The AI's rulebook (keep < 1,500 tokens)
- `.github/project-architecture.md` - Architecture design
- `docs/architecture/adr/` - Architecture decisions

### Before Each Sprint
- [ ] Review copilot-instructions.md for needed updates
- [ ] Create ADRs for new architectural decisions
- [ ] Verify NFRs are explicit for new features
- [ ] Check token budget

### During Sprint
- [ ] Review architecture-level AI-generated code
- [ ] Block PRs that violate boundaries
- [ ] Update docs when patterns change

### After Sprint
- [ ] Architecture health check
- [ ] Approve copilot-instructions.md updates
- [ ] Update ADRs based on learnings

### Red Flags 🚨
- copilot-instructions.md > 2,000 tokens
- Same architectural violation in 3+ stories
- AI repeatedly ignores documented constraint

---

## 🎯 Tech Lead Quick Reference

### Your Core Files
- `docs/sprint-context.md` - Update before each sprint
- `docs/user-stories/` - Transform raw stories to AI-ready
- `docs/prompt-library.md` - Maintain validated prompts
- `docs/api-contracts/` - Create and freeze contracts

### Story Refinement (3 Prompts)
1. **Technical Context:** Files, APIs, DB tables, dependencies
2. **AC Sharpening:** Make specific, testable, with data types
3. **Agent Execution Notes:** Reference pattern, library, common mistakes

### Daily Activities
- [ ] Review AI output quality
- [ ] Handle escalations (AI failed 3+ times)
- [ ] Update prompt library if patterns emerge

### Sprint Retrospective
1. Collect all feedback from `docs/agent-feedback/sprint-N/`
2. Run analysis prompt (see prompt-library.md 5.1)
3. Update prompt library
4. Submit copilot-instructions.md updates to Architect

### Red Flags 🚨
- Developer spends >30 min on single AI failure
- Same correction needed in 3+ stories
- Story quality issues causing AI confusion

---

## 💻 Developer Quick Reference

### Your Morning Routine
1. Read `docs/sprint-context.md`
2. Review assigned story in `docs/user-stories/current-sprint/`
3. Run 15-minute pre-execution ritual

### Pre-Execution Ritual (15 min)
- [ ] Read story completely
- [ ] Verify all file paths exist
- [ ] Check dependencies (merged or need mocks?)
- [ ] Ask: "If I were the AI, would I have everything?"

### Story Execution Flow
```
1. Load Context (use prompt from library)
   ↓
2. Review Plan (approve or redirect ONCE specifically)
   ↓
3. Monitor Execution (watch scope, libraries, patterns)
   ↓
4. Validate (run tests, check each AC)
   ↓
5. Create PR (AI generates description)
   ↓
6. Submit Feedback (always, no exceptions)
```

### The Golden Rules
1. **Always load context first** - Never one-line task prompts
2. **Always review the plan** - Catch errors before code written
3. **Stop on scope drift** - Out-of-scope file touched = STOP
4. **Escalate at 3 failures** - After 3 attempts, call Tech Lead
5. **Log every correction** - Feedback drives improvement

### When to Intervene
| Signal | Action |
|--------|--------|
| Scope drift / unapproved library | STOP immediately |
| Wrong pattern / questionable tests | PAUSE and redirect |
| Minor style difference | Let continue |

### Escalation Triggers
- 🚨 AI fails 3+ times → Tech Lead
- 🚨 AI modifies out-of-scope files → Stop & redirect
- 🚨 Security issue found → Block PR, Tech Lead
- 🚨 >30 min manual coding → Escalate

---

## 📝 Prompt Anti-Patterns (All Roles)

| ❌ Don't Do This | ✅ Do This Instead |
|------------------|-------------------|
| "Fix this" | "Test auth.test.ts:47 fails with [error]. Read auth.ts and fix only that assertion." |
| "Make it better" | "Refactor getUserById in user.service.ts:82 to remove N+1 query. Follow pattern at order.service.ts:45." |
| Paste 500 lines inline | "Read [file path]" |
| "Continue" after wrong output | "Stop. Revert [file]. Correct approach is [specific]. Revise." |
| Skip context load | Always use prompt 1.1 from library first |
| No gate instruction | Always: "Wait for my confirmation" |

---

## 📊 Success Metrics (All Roles)

| Metric | Target | Who Tracks |
|--------|--------|------------|
| AI-completed stories | ≥ 70% | Tech Lead |
| Avg corrections/story | < 2 | Tech Lead |
| Stories with manual code | < 10% | Tech Lead |
| Stories in one pass | ≥ 70% | Tech Lead |
| copilot-instructions.md size | < 1,500 tokens | Architect |

---

## 🔄 The Learning Loop

```
Execute Story
    ↓
Submit Feedback (docs/agent-feedback/sprint-N/story-ID-feedback.md)
    ↓
Sprint Retrospective (Tech Lead analyzes all feedback)
    ↓
Update Documentation
    - copilot-instructions.md (Architect approves)
    - prompt-library.md (Tech Lead)
    - sprint-context.md (Tech Lead)
    ↓
Next Sprint Improves (AI makes fewer mistakes)
```

---

## 📂 File Quick Access

| Need to... | Go to... |
|------------|----------|
| Know AI behavior rules | `.github/copilot-instructions.md` |
| Understand architecture | `.github/project-architecture.md` |
| Get sprint context | `docs/sprint-context.md` |
| Read a story | `docs/user-stories/current-sprint/story-[ID].md` |
| Find a prompt | `docs/prompt-library.md` |
| Submit feedback | `docs/agent-feedback/sprint-N/story-[ID]-feedback.md` |
| Check API contract | `docs/api-contracts/` |
| Read an ADR | `docs/architecture/adr/ADR-[NNN]-[title].md` |

---

## 🆘 Emergency Procedures

### AI Won't Stop Modifying Wrong Files
1. STOP immediately
2. Revert changes: "Revert all changes to [files]"
3. Clarify scope: "Only modify: [list from story]"
4. Restart if needed

### AI Failed 3+ Times
1. Stop correction loop
2. Ask AI to show: failing test, error, root cause understanding
3. Diagnose yourself (10 min max)
4. If still stuck → Escalate to Tech Lead
5. Log in feedback

### Story Unclear
1. DO NOT guess or assume
2. Ping Tech Lead immediately
3. Tech Lead updates story file
4. Restart with clarified story

### Can't Find Pattern Reference
1. Check `docs/prompt-library.md`
2. Search codebase for similar functionality
3. Ask Tech Lead for reference
4. Document gap in feedback log

---

## 💡 Pro Tips

**For Architects:**
- One good rule prevents 100 corrections
- Move history to ADRs, keep copilot-instructions.md lean
- "Constraints for AI" is the most important ADR section

**For Tech Leads:**
- Invest 20 min in story prep → saves 2 hours in corrections
- Freeze API contracts before parallel work starts
- Prompt library is your team's most valuable asset

**For Developers:**
- Read story completely before starting (5 min investment)
- File paths wrong = AI reads wrong file = wasted hour
- Feedback logs are not optional - they're how we improve

---

## 📞 Who to Contact

| Issue | Contact |
|-------|---------|
| Architectural question | Architect |
| Story unclear | Tech Lead |
| AI failed 3+ times | Tech Lead |
| Process question | Tech Lead |
| Security concern | Tech Lead → Architect → Security Team |

---

**Keep this card handy during development!**

Print or bookmark: `quick-reference.md`

---

**Version:** 1.0  
**Based on:** SOP-AI-Driven-Development.md v1.0  
**Last Updated:** [DATE]
