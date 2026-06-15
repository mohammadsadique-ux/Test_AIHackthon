# Agent Feedback

This directory contains feedback logs from AI agent executions.

## Purpose

Feedback logs are the **primary input for sprint retrospectives and agent improvement**. Every correction, deviation, or issue encountered during AI execution is captured here and used to improve prompts, CLAUDE.md/copilot-instructions.md, and story templates.

**Rule:** Every story must have a feedback log. No exceptions.

## Directory Structure

```
agent-feedback/
├── README.md                           # This file
├── feedback-template.md                # Template for feedback logs
├── overrides.md                        # Log of manual code overrides
├── sprint-1/
│   ├── story-US-100-feedback.md
│   ├── story-US-101-feedback.md
│   └── ...
├── sprint-2/
│   ├── story-US-200-feedback.md
│   └── ...
└── analysis/
    ├── sprint-1-retrospective.md       # Consolidated analysis
    ├── sprint-2-retrospective.md
    └── ...
```

## Feedback Log Naming

```
story-[ID]-feedback.md

Examples:
story-US-042-feedback.md
story-JIRA-1234-feedback.md
```

Match the story ID exactly.

## Feedback Template

```markdown
# Feedback: Story [ID] — [Title]

**Developer:** [Your Name]  
**Date:** YYYY-MM-DD  
**Story Status:** [Completed / Completed with Manual Fix / Failed]  
**Time Spent:** [Total hours]  

---

## AI Execution Summary

### AI Contribution
- **AI-generated code:** [percentage or line count]
- **Manual corrections:** [percentage or line count]
- **Manual additions:** [percentage or line count]

### Session Metrics
- **Total messages to AI:** [count]
- **Plan iterations:** [how many times plan was regenerated]
- **Correction loops:** [count]
- **Session resets:** [count - if any]

---

## What AI Got Right

[List specific things the AI did correctly]

1. [Positive outcome 1]
2. [Positive outcome 2]
3. [Pattern AI followed successfully]

**Example:**
- AI correctly implemented the validation pattern from copilot-instructions.md
- Test coverage was generated automatically and met the threshold
- Error handling followed the standard pattern without correction

---

## What Needed Correction

[For each correction, document the specifics]

### Correction 1: [Brief Title]
- **What AI produced:** [Describe the output]
- **Why it was wrong:** [Explain the issue]
- **What I did:** [The correction made]
- **Root cause:** [Missing context / Wrong prompt / AI limitation]
- **How to prevent:** [Specific fix - prompt change, copilot-instructions.md rule, story template improvement]

### Correction 2: [Brief Title]
- **What AI produced:** ...
- **Why it was wrong:** ...
- **What I did:** ...
- **Root cause:** ...
- **How to prevent:** ...

**Example:**
### Correction 1: Wrong Import Path
- **What AI produced:** `import { UserService } from '../services/userService'`
- **Why it was wrong:** File is actually at `src/modules/users/user.service.ts`
- **What I did:** Corrected the import path manually
- **Root cause:** Story file listed wrong path
- **How to prevent:** Verify all file paths before triggering AI (add to pre-execution checklist)

---

## Context Gaps

[Things the AI didn't know that it should have]

1. [Gap 1] → Should be in [copilot-instructions.md / story file / sprint-context.md]
2. [Gap 2] → Should be in [document]

**Example:**
- AI didn't know we use `paise` not `rupees` for currency amounts
  → Add to copilot-instructions.md Section 3 (Code Conventions)
- AI didn't know story-US-080 already implemented email validation pattern
  → Add reference in Agent Execution Notes

---

## Prompt Effectiveness

### Prompts That Worked Well
- [Prompt or pattern that produced good results]
- [Another effective prompt]

### Prompts That Failed
- [Prompt that didn't work]
  - **Why it failed:** [Reason]
  - **Better alternative:** [Improved prompt]

**Example:**
**Worked:** "Follow the pattern in src/modules/auth/auth.service.ts for error handling"
**Failed:** "Handle errors properly" - Too vague, AI implemented generic try-catch

---

## Manual Overrides

[If you wrote code manually instead of using AI]

### Override 1: [Component Name]
- **Why manual:** [Reason - AI failed after 3 attempts / Complex business logic / etc.]
- **Code written:** [File and function]
- **AI's issue:** [What AI couldn't do correctly]
- **Learning:** [What constraint or pattern needs to be documented]

**Example:**
- **Why manual:** AI failed to understand complex date calculation logic after 3 attempts
- **Code written:** src/utils/date-calculator.ts - calculateBusinessDays()
- **AI's issue:** Kept miscounting weekends and holidays
- **Learning:** Complex date logic should be in a separate utility with clear test cases. Add example to prompt library.

---

## Story Quality Assessment

### Was the Story AI-Ready?
[Yes / Mostly / No]

### Issues with Story File
- [ ] Missing file paths
- [ ] Ambiguous acceptance criteria
- [ ] Unclear technical context
- [ ] Missing Agent Execution Notes
- [ ] NFRs not specific enough
- [ ] [Other issue]

### Story Improvements Needed
[Specific changes to make this story template better]

**Example:**
- Add explicit note about currency format (paise vs rupees)
- Link to API contract doc for response format
- Specify exact validation library method to use

---

## Recommendations

### For copilot-instructions.md
[Specific rules to add or update]

**Example:**
- Add to Section 6 (Approved Libraries): "For date manipulation, ALWAYS use date-fns, never moment.js"
- Add to Section 5 (Never Do): "NEVER use floating point for currency - use integers in smallest unit"

### For Prompt Library
[New prompts to add or existing prompts to improve]

**Example:**
- Add prompt: "Payment Processing Implementation" with specific constraints for currency handling

### For Sprint Context
[Patterns or learnings for next sprint]

**Example:**
- All payment-related stories should reference the currency format rule explicitly

### For Story Template
[Improvements to story structure]

**Example:**
- Add "Data Format Notes" section to Technical Context for stories involving currency, dates, or complex data types

---

## Token Efficiency

### Estimated Tokens Used
- **Context load:** ~[number]
- **Plan generation:** ~[number]
- **Implementation:** ~[number]
- **Corrections:** ~[number]
- **Total:** ~[number]

### Could This Have Been More Efficient?
[Yes / No]

If yes, how:
[Specific optimization]

**Example:**
- Instead of pasting 300 lines of existing code in prompt, should have told AI "Read src/services/payment.service.ts"
- Estimated saving: ~400 tokens

---

## Overall Assessment

### Story Complexity
[Simple / Medium / Complex]

### AI Performance
[Excellent / Good / Fair / Poor]

### Would I Use AI for Similar Stories?
[Yes / Yes with better prompt / No - too complex]

### Key Takeaway
[One sentence summary of the most important learning]

**Example:**
- AI excels at CRUD operations when file paths and patterns are explicit, but struggles with complex business logic that requires domain understanding.

---

## Next Steps

[Actions to take based on this feedback]

- [ ] Update copilot-instructions.md with [specific rule]
- [ ] Add prompt to prompt library: [prompt name]
- [ ] Update story template with [improvement]
- [ ] Create ADR for [decision that emerged]
- [ ] Discuss with Tech Lead: [issue or pattern]

---

## Related Documents

- Story: docs/user-stories/story-[ID].md
- PR: [Link to pull request]
- Sprint Context: docs/sprint-context.md
```

## Feedback Submission Process

### When to Submit
**Immediately after story completion** - while details are fresh.

### How to Submit
1. Copy `feedback-template.md`
2. Rename to `story-[ID]-feedback.md`
3. Fill out all sections completely
4. Save to `agent-feedback/sprint-[N]/`
5. Commit with message: `Add feedback for story [ID]`

### Minimum Required Sections
Even for simple stories, you MUST complete:
- AI Execution Summary
- What AI Got Right (at least 2 items)
- What Needed Correction (if any)
- Recommendations (at least one)
- Overall Assessment

## Overrides Log

When you write code manually (AI couldn't do it), also log it in `overrides.md`:

```markdown
# Manual Code Overrides

This file tracks instances where developers wrote code manually instead of using AI.

## Sprint [N]

### Story [ID] - [Component]
- **Date:** YYYY-MM-DD
- **Developer:** [Name]
- **What was written:** [File and function/class]
- **Why manual:** [Reason AI couldn't do it]
- **AI's issue:** [Specific problem AI had]
- **Pattern to document:** [What rule or pattern would prevent this in future]

---
```

## Sprint Retrospective Process

### At End of Sprint

**Tech Lead runs this process:**

1. **Collect all feedback logs** from `sprint-[N]/`
2. **Read overrides.md** for manual coding patterns
3. **Run analysis prompt:**
   ```
   Review these developer feedback logs: [paste all logs]

   Identify patterns across all stories:
   1. Top 5 prompt improvements (specific before/after text)
   2. copilot-instructions.md rules to add (exact wording)
   3. New slash commands to create (full prompt text)
   4. Anti-patterns to document
   5. Success patterns to reinforce

   Be specific and actionable. For each item, cite which story(ies) revealed this pattern.
   ```

4. **Generate retrospective document** in `analysis/sprint-[N]-retrospective.md`
5. **Apply improvements:**
   - Update copilot-instructions.md (get Architect approval)
   - Update prompt library
   - Update story template if needed
   - Share learnings with team

## Feedback Analysis Categories

### Category 1: Context Gaps
Things AI should have known but didn't
→ **Fix:** Add to copilot-instructions.md or memory files

### Category 2: Prompt Issues
Prompts that didn't work well
→ **Fix:** Update prompt library with better versions

### Category 3: Story Quality
Story files missing information
→ **Fix:** Update story template, improve Tech Lead story prep process

### Category 4: Agent Limitations
Things AI fundamentally struggles with
→ **Fix:** Document as "use manual coding for [pattern]"

### Category 5: Success Patterns
Things AI did exceptionally well
→ **Fix:** Document and reinforce in copilot-instructions.md

## Metrics to Track

Track these across sprints to measure improvement:

| Metric | Sprint N-2 | Sprint N-1 | Sprint N | Target |
|--------|------------|------------|----------|--------|
| % AI-completed stories (no manual fix) | | | | ≥ 70% |
| Average corrections per story | | | | < 2 |
| Stories requiring manual code | | | | < 10% |
| Average session reset count | | | | < 0.2 |
| % stories completed in one pass | | | | ≥ 70% |

## Red Flags

If you see these patterns in feedback, escalate immediately:

- ⚠️ **Same correction** needed in 3+ stories → copilot-instructions.md gap
- ⚠️ **Same AI mistake** repeated across sprint → prompt library issue
- ⚠️ **Manual overrides** > 30% in a story → Story too complex or poorly specified
- ⚠️ **Session resets** > 2 per story → Fundamental context problem

## Related Documents

- `.github/copilot-instructions.md` - Gets updated based on feedback
- `docs/prompt-library.md` - Gets updated based on feedback
- `docs/sprint-context.md` - Captures sprint-level patterns
- `docs/user-stories/README.md` - Story template improvements
