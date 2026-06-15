# Prompt Library

**Reusable, Validated Prompts for AI-Driven Development**

| Document Version | 1.0 |
| :---- | :---- |
| **Last Updated** | [DATE] |
| **Owner** | Technical Lead |
| **Status** | Living Document |

---

## Purpose

This library contains **validated, reusable prompts** that have been proven effective in AI-driven development. Each prompt is categorized, documented with success metrics, and refined over multiple sprints.

**Rule:** Any prompt used successfully 3+ times should be added to this library.

---

## How to Use This Library

### For Tech Leads
- Maintain and update this library after each sprint retrospective
- Add new prompts discovered during the sprint
- Update existing prompts based on feedback logs
- Archive or remove prompts that consistently fail

### For Developers
- Reference this library before crafting your own prompts
- Use slash command versions where available
- Submit new prompts that work well via feedback logs
- Report prompts that fail so they can be improved

### For Architects
- Review prompt quality during monthly governance
- Ensure prompts align with copilot-instructions.md
- Validate that security and architecture constraints are embedded

---

## Prompt Categories

1. [Feature Implementation](#category-1-feature-implementation)
2. [Bug Diagnosis & Fix](#category-2-bug-diagnosis--fix)
3. [Code Refactoring](#category-3-code-refactoring)
4. [Code Review & Validation](#category-4-code-review--validation)
5. [Sprint Operations](#category-5-sprint-operations)

---

## Category 1: Feature Implementation

### 1.1 - Full Story Implementation (Standard)

**When to use:** Start of any user story  
**Validated:** Yes — Sprint [N], 15+ stories  
**Token estimate:** 300-500 (context load) + variable  
**Success rate:** 85%

```
Before we start, read these files in this order:
1. .github/copilot-instructions.md
2. docs/sprint-context.md
3. docs/user-stories/story-[ID].md
4. [each file listed in Technical Context section of the story]

After reading all of them, confirm by telling me:
(a) What this story needs to accomplish — one sentence
(b) Which specific files you will create or modify
(c) Any ambiguity or missing information you spotted

Do NOT start implementing. Wait for my confirmation.
```

**Typical follow-up after confirmation:**
```
Plan approved. Proceed with implementation. Remember to:
- Run tests after completing each file
- Follow the pattern referenced in Agent Execution Notes
- Stop if you encounter any ambiguity and ask before proceeding
```

---

### 1.2 - API Endpoint Implementation

**When to use:** Creating new REST API endpoint  
**Validated:** Yes — Sprint [N], 8 stories  
**Token estimate:** 200-400  
**Success rate:** 90%

```
Implement a new API endpoint based on this specification:

Endpoint: [METHOD] [PATH]
Story file: docs/user-stories/story-[ID].md
API contract: docs/api-contracts/[contract-file].md

Follow these patterns:
1. Controller structure: [reference file]
2. Service layer: [reference file]
3. Validation: [reference file]
4. Error handling: [reference file]

Implementation checklist:
- [ ] Input validation using [validation library]
- [ ] Authentication check (unless public endpoint)
- [ ] Authorization check (if resource-specific)
- [ ] Service layer method
- [ ] Error responses for all status codes in contract
- [ ] Unit tests for service layer (≥ [threshold]% coverage)
- [ ] Integration tests for all status codes

Generate implementation plan first. Wait for approval before coding.
```

---

### 1.3 - Database Model & Migration

**When to use:** Creating or modifying database schema  
**Validated:** Yes — Sprint [N], 5 stories  
**Token estimate:** 250-400  
**Success rate:** 80%

```
Create a database migration for this requirement:

Story: docs/user-stories/story-[ID].md
Database: [PostgreSQL / MySQL / etc.]
ORM: [Sequelize / TypeORM / Entity Framework / etc.]

Requirements:
- Table(s): [list]
- Columns: [list with types]
- Relationships: [describe]
- Indexes: [specify]
- Constraints: [specify]

Follow these patterns:
1. Migration structure: [reference existing migration file]
2. Naming convention: YYYYMMDDHHMMSS_[description]
3. MUST include both up() and down() methods
4. Add comments explaining each change

Before generating code:
1. Show me the table structure diagram
2. List all indexes to be created
3. Explain rollback strategy

Wait for approval before generating migration file.
```

---

### 1.4 - Unit Test Generation

**When to use:** Adding tests to existing code  
**Validated:** Yes — Sprint [N], 12 stories  
**Token estimate:** 200-350  
**Success rate:** 88%

```
Generate comprehensive unit tests for this file:

File: [path/to/file]
Testing framework: [Jest / xUnit / pytest / etc.]
Mocking library: [library name]

Requirements from copilot-instructions.md:
- Coverage threshold: ≥ [X]%
- Test naming: [convention]
- Test structure: Arrange-Act-Assert

Focus on:
1. Happy path scenarios
2. Edge cases: [list specific edge cases from story]
3. Error handling: [list expected errors]
4. Boundary conditions

For each test:
- Use descriptive test names following our convention
- Mock external dependencies (database, APIs, etc.)
- Include meaningful assertions (not just code coverage)
- Add comments for complex test setups

Show me the test plan (test names and what each tests) first.
Wait for approval before generating tests.
```

---

## Category 2: Bug Diagnosis & Fix

### 2.1 - Test Failure Diagnosis

**When to use:** When test is failing  
**Validated:** Yes — Sprint [N], 10 instances  
**Token estimate:** 150-300  
**Success rate:** 85%

```
Diagnose this test failure:

Test file: [path/to/test]
Failing test: [test name or line number]
Error message: [exact error message]

Read the following:
1. The test file: [path]
2. The implementation file: [path]
3. Any mocked dependencies: [list]

Analyze:
- What is the test expecting?
- What is the actual behavior?
- What is the root cause?
- Is this a test issue or implementation issue?

Provide:
1. Root cause analysis
2. Proposed fix (test or implementation)
3. Explanation of why this happened

Do NOT fix anything yet. Wait for my confirmation of the diagnosis.
```

---

### 2.2 - Bug Fix from Issue Report

**When to use:** Fixing reported bug  
**Validated:** Yes — Sprint [N], 7 bugs  
**Token estimate:** 200-400  
**Success rate:** 82%

```
Fix this reported bug:

Bug report: [description or link]
Expected behavior: [describe]
Actual behavior: [describe]
Steps to reproduce: [list]

Investigation scope:
1. Read relevant files: [list]
2. Check related tests: [list]
3. Review recent changes: [git commit range if known]

Process:
1. First, reproduce the bug (write a failing test)
2. Identify root cause
3. Propose fix
4. Verify fix doesn't break other functionality

Provide:
- Root cause analysis
- Proposed fix
- Test that verifies fix
- Impact analysis (what else might be affected)

Wait for approval before implementing fix.
```

---

### 2.3 - Performance Issue Diagnosis

**When to use:** Slow query or endpoint  
**Validated:** Yes — Sprint [N], 4 issues  
**Token estimate:** 250-450  
**Success rate:** 75%

```
Diagnose this performance issue:

Component: [endpoint / function / query]
Current performance: [metric]
Expected performance: [metric]
Profiling data: [if available]

Read:
1. Implementation: [file path]
2. Related database queries: [list]
3. NFR requirements: [from story or copilot-instructions.md]

Analyze:
- Is this a database query issue? (N+1, missing indexes, inefficient joins)
- Is this an algorithm issue? (inefficient loops, unnecessary operations)
- Is this a caching issue? (repeated expensive operations)

Provide:
1. Root cause with evidence
2. Proposed optimization
3. Expected performance improvement
4. Risk assessment (does optimization add complexity?)

Wait for approval before implementing optimization.
```

---

## Category 3: Code Refactoring

### 3.1 - Extract Common Pattern

**When to use:** Duplicated code across files  
**Validated:** Yes — Sprint [N], 6 refactors  
**Token estimate:** 300-500  
**Success rate:** 88%

```
Refactor duplicated code into reusable pattern:

Duplicate code location 1: [file:function]
Duplicate code location 2: [file:function]
[Additional locations if applicable]

Read all affected files:
[list file paths]

Requirements:
- Extract to: [utility / service / helper - specify location]
- Maintain exact same behavior (no functional changes)
- Update all call sites
- Add appropriate tests for extracted function
- Update any affected tests

Process:
1. Show me the common pattern you identified
2. Show me the proposed extracted function signature
3. Show me how each call site will change

Wait for approval before refactoring.

IMPORTANT: Do NOT change behavior. This is pure refactoring.
```

---

### 3.2 - Simplify Complex Function

**When to use:** Function >50 lines or high complexity  
**Validated:** Partial — Sprint [N], 3 refactors (mixed results)  
**Token estimate:** 250-450  
**Success rate:** 70%

```
Simplify this complex function:

File: [path]
Function: [name]
Current complexity: [cyclomatic complexity if known]
Current length: [lines]

Read:
1. The file containing the function
2. Tests for this function: [path]
3. Pattern reference: [similar well-structured function]

Goals:
- Reduce function length to < [target] lines
- Reduce cyclomatic complexity to < [target]
- Improve readability
- Maintain exact same behavior

Approach:
1. Extract helper functions for logical sub-steps
2. Use early returns to reduce nesting
3. Extract complex conditionals into named boolean variables
4. Consider strategy pattern if multiple conditional branches

Process:
1. Show me the refactoring plan (what gets extracted)
2. Show me proposed function signatures
3. Confirm all tests still pass

Wait for approval before refactoring.
```

---

## Category 4: Code Review & Validation

### 4.1 - Self-Review Against Acceptance Criteria

**When to use:** Before submitting PR  
**Validated:** Yes — Sprint [N], 20+ uses  
**Token estimate:** 200-400  
**Success rate:** 92%

```
Review the current changes against acceptance criteria:

Story: docs/user-stories/story-[ID].md
Changes: [git diff or file list]

For each acceptance criterion in the story:
1. State the AC
2. Mark as: PASS / FAIL / NOT VERIFIABLE
3. Provide evidence (code location or test name)

Also check:
- [ ] Architectural violations (module boundaries from copilot-instructions.md)
- [ ] Security issues (input validation, secrets, error exposure)
- [ ] Test quality (meaningful assertions vs padding)
- [ ] Hardcoded values that should be configurable
- [ ] Error handling completeness

Output format:
## Acceptance Criteria Check
[Table with AC# | Status | Evidence]

## Architecture & Quality Check
[List of findings with severity: BLOCKER / CRITICAL / MAJOR / INFO]

## Recommended Actions
[Specific fixes needed before PR submission]
```

---

### 4.2 - Security Review

**When to use:** Before merging sensitive code  
**Validated:** Yes — Sprint [N], 8 reviews  
**Token estimate:** 300-500  
**Success rate:** 85%

```
Review these changes for security vulnerabilities:

Changes: [git diff or file list]
Focus areas: [authentication / payment / data access / etc.]

Check specifically for:

1. **Injection Vulnerabilities**
   - [ ] All database queries use parameterized queries
   - [ ] No SQL string concatenation
   - [ ] No eval() or similar dynamic execution

2. **Authentication & Authorization**
   - [ ] All protected endpoints have auth check
   - [ ] User cannot access another user's resources
   - [ ] Role-based access is enforced

3. **Data Exposure**
   - [ ] No sensitive data in error responses
   - [ ] No sensitive data in logs (passwords, tokens, PII)
   - [ ] API responses don't include internal details

4. **Input Validation**
   - [ ] All user inputs are validated
   - [ ] All inputs are sanitized before use
   - [ ] File uploads have type and size restrictions

5. **Secrets Management**
   - [ ] No hardcoded credentials
   - [ ] No API keys in code
   - [ ] Secrets come from environment or key vault

6. **OWASP Top 10**
   - [ ] Check against: [list relevant OWASP items]

Output format:
| Severity | File:Line | Issue | Recommendation |
[BLOCKER / CRITICAL / MAJOR / INFO]

All BLOCKERs must be fixed before merge.
```

---

## Category 5: Sprint Operations

### 5.1 - Sprint Retrospective Analysis

**When to use:** End of every sprint  
**Validated:** Yes — Every sprint since adoption  
**Token estimate:** 500-800  
**Success rate:** 95%

```
Review these developer feedback logs and analyze patterns:

Files to read:
docs/agent-feedback/sprint-[N]/story-*.md
docs/agent-feedback/overrides.md (Sprint [N] section)

Analyze across all stories:

1. **Prompt Improvements**
   - What prompts consistently failed?
   - What prompts worked well?
   - Suggest specific improvements (before/after text)

2. **copilot-instructions.md Updates**
   - What rules were the AI unaware of?
   - What context gaps appeared repeatedly?
   - Provide exact wording for new rules

3. **New Slash Commands**
   - What prompt patterns were repeated 3+ times?
   - Generate full command text for each

4. **Anti-Patterns**
   - What mistakes did AI make repeatedly?
   - Format for anti-patterns.md

5. **Success Patterns**
   - What did AI consistently do well?
   - How to reinforce in project-patterns.md

Output:
- Top 5 prompt improvements with specific text
- 3-5 copilot-instructions.md additions with exact wording
- 2-3 new slash commands with full prompt
- Anti-patterns for memory file (formatted for docs)
- Success patterns to reinforce (formatted for docs)

For each item, cite which story feedback(s) revealed this pattern.
```

---

### 5.2 - Story Breakdown for AI Readiness

**When to use:** Converting raw PO story to AI-ready  
**Validated:** Yes — Sprint [N], 18 stories  
**Token estimate:** 400-600  
**Success rate:** 90%

```
Transform this raw user story into an AI-ready story file:

Raw story: [paste from backlog]
Target template: docs/user-stories/story-template.md
Project context: .github/copilot-instructions.md

Run this three-step process:

**Step 1: Technical Context Extraction**
Based on our tech stack and conventions in copilot-instructions.md:
- Which files/modules would this touch?
- What APIs need creation or modification?
- What DB tables are involved?
- What are hidden technical dependencies?

**Step 2: AC Sharpening**
For each acceptance criterion:
- Make it specific and testable
- Include exact data types and formats
- Specify error behavior
- Ensure automated test can verify it
Add any missing ACs an AI would need.

**Step 3: Agent Execution Notes**
- Reference the most relevant past story (from our history)
- Specify THE library to use (from approved list)
- List top 2 places AI is likely to go wrong
- Specify file creation order

Output: Complete story file using our template structure.
```

---

### 5.3 - API Contract Generation

**When to use:** Before sprint with parallel work  
**Validated:** Yes — Sprint [N], 4 contracts  
**Token estimate:** 500-800  
**Success rate:** 88%

```
Generate a complete API contract for this feature:

Story/Epic: [description]
Endpoints involved: [list]
Team context: [backend/frontend/both]

Use our contract template: docs/api-contracts/README.md

Include:
1. All endpoints with methods
2. Complete request schemas with validation rules
3. Complete response schemas (success + all error cases)
4. All status codes with when each is used
5. Authentication requirements
6. Examples for each endpoint

CRITICAL: "Constraints for AI" section must include:
- Backend: How to implement (validation, auth checks, error handling)
- Frontend: How to consume (error handling, field usage, auth headers)

Process:
1. Show me list of endpoints first
2. For each endpoint, show request/response structure
3. Wait for approval
4. Generate full contract document

Mark as Status: Frozen once approved (no changes during sprint).
```

---

## Prompt Effectiveness Metrics

Track these for each prompt in the library:

| Prompt ID | Success Rate | Avg Tokens | Avg Corrections | Last Updated |
|-----------|--------------|------------|-----------------|--------------|
| 1.1 | 85% | 400 | 1.2 | YYYY-MM-DD |
| 1.2 | 90% | 300 | 0.8 | YYYY-MM-DD |
| 2.1 | 85% | 250 | 1.1 | YYYY-MM-DD |
| ... | ... | ... | ... | ... |

**Criteria for keeping a prompt:**
- Success rate ≥ 70%
- Used in last 2 sprints
- Positive feedback from developers

**Criteria for archiving:**
- Success rate < 50% for 2 consecutive sprints
- Not used in last 3 sprints
- Consistently negative feedback

---

## Prompt Anti-Patterns

### ❌ Don't Do This

| Anti-Pattern | Why It Fails | Better Approach |
|--------------|--------------|-----------------|
| "Fix this bug" | No context, no file, no error message | Use prompt 2.2 with specifics |
| "Make it better" | "Better" is undefined | Specify exact improvement (performance, readability, etc.) |
| Paste 500 lines inline | Wastes tokens, hard to parse | "Read [file path]" |
| "Continue" after wrong output | Compounds errors | "Stop. Revert. Here's the correct approach: [specific]" |
| Skipping context load | AI doesn't know project rules | Always use prompt 1.1 first |
| No gate instruction | AI proceeds without approval | Always: "Wait for my confirmation" |

---

## Version History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | YYYY-MM-DD | [Name] | Initial library creation |
| 1.1 | YYYY-MM-DD | [Name] | Added 3 new prompts from Sprint [N] |

---

## Related Documents

- `.github/copilot-instructions.md` - Project rules that prompts reference
- `docs/sprint-context.md` - Current sprint context
- `docs/user-stories/story-template.md` - Story structure
- `docs/agent-feedback/` - Source of prompt improvements
- `docs/architecture/adr/` - Architecture decisions

---

## Maintenance Schedule

- **Weekly:** Add new prompts discovered during sprint
- **Sprint End:** Review all feedback logs for prompt issues
- **Sprint Retrospective:** Update success rates and metrics
- **Monthly:** Archive unused prompts, validate effectiveness
- **Quarterly:** Major revision based on accumulated learnings
