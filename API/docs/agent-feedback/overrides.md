# Manual Code Overrides

This file tracks instances where developers wrote code manually instead of using AI agents.

**Purpose:** Understanding when and why AI fails helps improve prompts, copilot-instructions.md, and story preparation. Every manual override is a learning opportunity.

---

## Sprint [N]

### Story [ID] - [Component Name]
- **Date:** YYYY-MM-DD
- **Developer:** [Name]
- **What was written:** [File path and function/class name]
- **Lines of code:** [Approximate count]
- **Why manual:** [Reason AI couldn't do it]
- **AI's issue:** [Specific problem AI had - e.g., couldn't understand business logic, wrong pattern after 3 attempts, etc.]
- **Attempts made:** [Number of times AI was tried before manual override]
- **Pattern to document:** [What rule, pattern, or example would prevent this in future]
- **Recommended action:** [Update copilot-instructions.md / Create new prompt / Add to story template / etc.]

---

### Example Entry

### Story US-120 - Complex Date Calculation Logic
- **Date:** 2024-01-15
- **Developer:** John Doe
- **What was written:** src/utils/business-days-calculator.ts - calculateBusinessDays()
- **Lines of code:** ~80
- **Why manual:** AI failed to correctly implement business day calculation with holiday handling after 3 correction attempts
- **AI's issue:** Kept miscounting weekends; couldn't integrate holiday calendar lookup correctly; test coverage was incomplete
- **Attempts made:** 4 (initial + 3 corrections)
- **Pattern to document:** Complex date/time logic with multiple conditions and edge cases should have explicit test cases in story file. AI needs examples of expected behavior for edge cases.
- **Recommended action:** 
  - Add to copilot-instructions.md: "For date calculations, provide explicit test cases for edge cases (weekends, holidays, month boundaries)"
  - Add to prompt library: "Date/Time Calculation Pattern" with example structure
  - Story template: Add "Edge Cases & Examples" subsection to Agent Execution Notes

---

## Sprint Retrospective Summary

[Filled by Tech Lead at end of sprint]

### Total Manual Overrides This Sprint: [count]
### Percentage of Stories with Manual Code: [percentage]

### Patterns Identified:
1. [Pattern 1 - e.g., "Complex business calculations with many edge cases"]
   - Stories affected: [IDs]
   - Recommendation: [Action to take]

2. [Pattern 2]
   - Stories affected: [IDs]
   - Recommendation: [Action to take]

### Actions Taken:
- [ ] copilot-instructions.md updated with [specific rule]
- [ ] Prompt library updated with [new prompt]
- [ ] Story template improved with [change]
- [ ] Team training on [topic]

---

## Historical Trends

| Sprint | Total Stories | Manual Overrides | % Manual | Trend |
|--------|---------------|------------------|----------|-------|
| Sprint N-3 | 12 | 5 | 42% | ↓ |
| Sprint N-2 | 15 | 4 | 27% | ↓ |
| Sprint N-1 | 14 | 2 | 14% | ↓ |
| Sprint N | 16 | [?] | [?]% | [?] |

**Target:** < 10% of stories require manual code overrides

---

## Categories of Manual Overrides

### Category 1: Complex Business Logic
- AI struggles with multi-step domain logic requiring business understanding
- **Pattern:** Domain calculations with multiple conditional branches
- **When to use manual:** If business logic has >5 conditional paths or requires domain expertise
- **How to improve:** Add detailed pseudo-code or flowcharts to story file

### Category 2: Performance Optimization
- AI produces functionally correct but inefficient code
- **Pattern:** N+1 queries, missing indexes, unoptimized loops
- **When to use manual:** When profiling reveals performance bottleneck
- **How to improve:** Add performance profiling to AI workflow, specify optimization in NFRs

### Category 3: Integration with Legacy Systems
- AI doesn't understand undocumented legacy system behavior
- **Pattern:** Interfacing with old code lacking documentation
- **When to use manual:** When legacy system has quirks not in documentation
- **How to improve:** Document legacy system patterns in ADRs

### Category 4: Security-Critical Code
- Developer prefers manual review for high-security components
- **Pattern:** Authentication, authorization, encryption, payment processing
- **When to use manual:** Mission-critical security functions
- **How to improve:** Create security review checklist, specialized security agent

### Category 5: Complex Algorithms
- AI produces incorrect or inefficient algorithmic solutions
- **Pattern:** Graph algorithms, optimization problems, complex data structures
- **When to use manual:** Advanced CS algorithms not in training data
- **How to improve:** Provide reference implementation or academic paper in story context

---

## Guidelines for Recording Overrides

### When to Record
Record an override whenever:
1. You write >20 lines of code manually after AI was attempted
2. You revert all AI code and start from scratch
3. AI fails after 3+ correction attempts

### What to Include
- **Be specific:** Not "AI couldn't do it" but "AI incorrectly handled timezone conversion in date calculations"
- **Include attempts:** How many times you tried redirecting AI
- **Identify root cause:** Was it missing context, wrong prompt, or genuine AI limitation?
- **Suggest prevention:** What would have made AI succeed?

### What NOT to Record
- Minor tweaks to AI code (<20 lines)
- Style/formatting changes
- Simple bug fixes in otherwise correct AI code

---

## Tech Lead Review Process

### Weekly Review (During Sprint)
- Review new overrides
- Identify emerging patterns
- Escalate to Architect if architectural implications
- Update copilot-instructions.md if clear pattern emerges

### Sprint Retrospective (End of Sprint)
1. Count total overrides and calculate percentage
2. Categorize all overrides
3. Identify top 3 patterns
4. Generate recommendations for next sprint
5. Update relevant documentation
6. Share learnings with team

---

## Related Documents

- `.github/copilot-instructions.md` - Update with learned patterns
- `docs/prompt-library.md` - Add prompts for manual override scenarios
- `docs/agent-feedback/` - Individual story feedback logs
- `docs/sprint-context.md` - Sprint-level pattern documentation
