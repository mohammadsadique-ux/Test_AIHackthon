# User Stories

This directory contains AI-ready user story files for implementation.

## Purpose

User stories in this folder are **formatted specifically for AI agent execution**. They contain all the context, technical details, and constraints needed for an AI agent to implement the story without ambiguity.

## Story File Naming

```
story-[ID].md

Examples:
story-US-042.md
story-JIRA-1234.md
story-001.md
```

Match the ID to your project management tool (Jira, Azure DevOps, etc.)

## AI-Ready Story Template

Every story file MUST follow this structure:

```markdown
# Story: [ID] — [Title]

## Intent
[1-2 sentences: What business outcome does this deliver?]

## User Story
As a [role], I want to [action] so that [outcome].

## Acceptance Criteria
- [ ] AC1: [Specific, testable criterion with exact data types/formats]
- [ ] AC2: [Include error behavior where applicable]
- [ ] AC3: [Make it objectively verifiable by automated test]
- [ ] AC4: [Each AC should have PASS/FAIL outcome]

## Technical Context
- **Relevant files:** [list exact file paths that need to be read/modified]
- **APIs involved:** [list endpoints that will be created/modified]
- **DB tables:** [list tables affected]
- **Dependencies:** [list story IDs this depends on]
- **Must NOT change:** [list files/modules that are off-limits]

## Non-Functional Requirements
- **Performance:** [e.g., API response < 200ms for 95th percentile]
- **Security:** [e.g., validate and sanitize all inputs, use parameterized queries]
- **Coverage:** [e.g., ≥ 85% unit test coverage for new code]
- **Accessibility:** [if applicable]
- **Compliance:** [if applicable - GDPR, PCI-DSS, etc.]

## Agent Execution Notes
[Hints for AI: known patterns, past similar stories, specific library to use]

- **Reference pattern:** See story-[previous-ID] for similar implementation
- **Library to use:** [Specific library from approved list]
- **Common mistakes to avoid:**
  1. [Likely error 1 and how to avoid it]
  2. [Likely error 2 and how to avoid it]
- **File creation order:** [Specify order if it matters]
- **Integration notes:** [Any special considerations for external systems]

## Related Documentation
- ADR: [Link to relevant ADR if applicable]
- API Contract: [Link to contract in docs/api-contracts/]
- Design: [Link to design docs/mockups if applicable]

## Definition of Done
- [ ] All acceptance criteria met
- [ ] Unit tests written and passing (coverage ≥ threshold)
- [ ] Integration tests written (if applicable)
- [ ] Code follows patterns in copilot-instructions.md
- [ ] No security vulnerabilities introduced
- [ ] API documentation updated (if API changes)
- [ ] PR reviewed and approved
- [ ] Feedback log submitted
```

## Story Readiness Checklist

Before assigning a story to a developer, verify:

| Check | Description |
|-------|-------------|
| ☐ **Intent Clear** | Business outcome stated in 1-2 sentences |
| ☐ **User Story Format** | Follows "As a / I want / So that" structure |
| ☐ **ACs Testable** | Each AC can be objectively verified (PASS/FAIL) |
| ☐ **ACs Specific** | Data types, formats, error behaviors specified |
| ☐ **File Paths Listed** | All relevant files explicitly listed in Technical Context |
| ☐ **APIs Named** | Endpoints specified with methods (GET, POST, etc.) |
| ☐ **DB Tables Listed** | All affected tables named |
| ☐ **Off-Limits Specified** | "Must NOT change" section populated |
| ☐ **NFRs Present** | At least performance and security NFRs specified |
| ☐ **Pattern Reference** | Similar past story referenced for consistency |
| ☐ **Library Specified** | Specific approved library named (not generic) |
| ☐ **No Ambiguities** | No place where AI would need to guess |

**Rule:** If any checkbox is unchecked, the story is NOT ready for AI execution.

## Story Quality Examples

### ❌ Poor Story (Not AI-Ready)

```markdown
# Story: US-100 — Add login

As a user, I want to login.

## Acceptance Criteria
- User can login
- User sees error if password wrong
```

**Problems:**
- No intent statement
- No technical context
- ACs not specific or testable
- No file paths, APIs, or database info
- No NFRs
- No agent execution notes

### ✅ Good Story (AI-Ready)

```markdown
# Story: US-100 — User Authentication with JWT

## Intent
Enable users to authenticate via email/password and receive a JWT token for subsequent API calls.

## User Story
As a registered user, I want to login with my email and password so that I can access protected features.

## Acceptance Criteria
- [ ] AC1: POST /api/v1/auth/login accepts { email: string, password: string }. Returns 200 with { token: string, expiresAt: ISO8601 } on success.
- [ ] AC2: Returns 400 with { code: "VALIDATION_ERROR", field: "email" } if email format invalid.
- [ ] AC3: Returns 401 with { code: "INVALID_CREDENTIALS" } if email/password combination incorrect.
- [ ] AC4: JWT token expires after 24 hours (configurable via JWT_EXPIRY_HOURS env var).
- [ ] AC5: Password is checked using bcrypt.compare() against hashed password in database.
- [ ] AC6: Failed login attempts are logged with user's email (not password) for security monitoring.

## Technical Context
- **Relevant files:**
  - src/modules/auth/auth.controller.ts (create)
  - src/modules/auth/auth.service.ts (create)
  - src/modules/users/user.repository.ts (read only - for user lookup)
  - src/middleware/validation.middleware.ts (read - for input validation)
  - src/config/jwt.config.ts (read - for JWT settings)
- **APIs involved:**
  - POST /api/v1/auth/login (new endpoint)
- **DB tables:**
  - users (id, email, password_hash, created_at, updated_at)
- **Dependencies:** None
- **Must NOT change:**
  - src/models/User.ts (schema is locked until next migration)
  - Any files in src/legacy/

## Non-Functional Requirements
- **Performance:** Login endpoint must respond in < 300ms for 95th percentile
- **Security:**
  - ALWAYS validate email format before database lookup
  - NEVER log passwords in any form
  - Use bcrypt.compare() for password checking (constant-time comparison)
  - Rate limit: max 5 login attempts per IP per minute
- **Coverage:** ≥ 90% unit test coverage for auth.service.ts

## Agent Execution Notes
- **Reference pattern:** Follow the pattern in src/modules/users/user.controller.ts for controller structure (Module → Controller → Service)
- **Library to use:** 
  - express-validator for input validation (already in approved list)
  - jsonwebtoken for JWT generation (already installed)
  - bcrypt for password comparison (already installed)
- **Common mistakes to avoid:**
  1. Don't compare passwords with === (timing attack vulnerability) - use bcrypt.compare()
  2. Don't expose "user not found" vs "wrong password" - both should return same 401 error
  3. Don't forget to set JWT expiry in token payload
- **File creation order:**
  1. auth.service.ts (business logic)
  2. auth.controller.ts (API endpoint)
  3. auth.service.test.ts (unit tests)
  4. auth.integration.test.ts (API tests)
- **Integration notes:**
  - JWT secret is stored in environment variable JWT_SECRET
  - User repository is already implemented - just import and use

## Related Documentation
- ADR: docs/architecture/adr/ADR-002-jwt-authentication.md
- API Contract: docs/api-contracts/auth-api-contract.md

## Definition of Done
- [ ] All 6 acceptance criteria met and verified
- [ ] Unit tests ≥ 90% coverage for auth.service.ts
- [ ] Integration tests cover all status codes (200, 400, 401)
- [ ] No hardcoded secrets (JWT_SECRET from env)
- [ ] Password never appears in logs
- [ ] Rate limiting implemented and tested
- [ ] API contract updated with this endpoint
- [ ] PR reviewed by Tech Lead
- [ ] Feedback log submitted
```

## Directory Structure

```
user-stories/
├── README.md                    # This file
├── story-template.md            # Copy this for new stories
├── current-sprint/              # Stories for active sprint
│   ├── story-US-100.md
│   ├── story-US-101.md
│   └── ...
├── next-sprint/                 # Prepared for next sprint
│   └── story-US-200.md
└── backlog/                     # Future stories (may not be fully refined)
    └── story-US-300.md
```

## Story Lifecycle

```
[Backlog] → [Refined by Tech Lead] → [Ready for AI] → [In Progress] → [In Review] → [Done]
```

### States

| State | Location | Who Owns | AI-Ready? |
|-------|----------|----------|-----------|
| **Backlog** | backlog/ | Product Owner | No |
| **Refined** | current-sprint/ | Tech Lead | Yes |
| **In Progress** | current-sprint/ | Developer | (Executing) |
| **In Review** | current-sprint/ | Tech Lead | (Reviewing) |
| **Done** | (Move to done/ or delete) | — | (Archived) |

## Story Refinement Process

### For Tech Leads (Story Preparation)

**Three-Prompt Refinement Sequence:**

1. **Prompt 1: Technical Context Extraction**
   ```
   I have this raw user story: [paste story]

   My project tech stack and conventions are in .github/copilot-instructions.md.

   Identify:
   - Which files/modules would this touch?
   - What APIs would need to be created or modified?
   - What DB tables are involved?
   - What are the hidden technical dependencies?
   ```

2. **Prompt 2: AC Sharpening**
   ```
   These are the draft acceptance criteria: [paste ACs]

   This story will be implemented by an AI agent.
   Rewrite each AC so that:
   1. It is specific and objectively testable
   2. It includes exact data types or formats
   3. It specifies error behavior
   4. An automated test can verify it

   Add any ACs that are missing.
   ```

3. **Prompt 3: Agent Execution Notes**
   ```
   Here is the refined story: [paste]

   Here are patterns from previous similar stories: [paste]

   Write an "Agent Execution Notes" section that:
   - References the most relevant past story
   - Identifies the ONE specific library that MUST be used
   - Lists the top 2 places an AI is likely to go wrong
   - Specifies the order in which files should be created
   ```

### For Developers (Pre-Execution Verification)

**15-Minute Pre-Execution Ritual:**

1. ✅ Read story file completely
2. ✅ Verify all file paths exist (if wrong, correct before starting)
3. ✅ Check dependencies: Are they merged? If not, get API contract
4. ✅ Ask: "If I were the AI, would I have everything I need?"

## AI Agent Prompt for Story Execution

```
Before we start, read these files in this order:
1. .github/copilot-instructions.md
2. docs/sprint-context.md
3. docs/user-stories/story-[ID].md
4. [each file listed in Technical Context]

After reading, confirm by telling me:
(a) What this story accomplishes - one sentence
(b) Which files you will create or modify
(c) Any ambiguity or missing information

Do NOT start implementing. Wait for my confirmation.
```

## Related Documents

- `.github/copilot-instructions.md` - AI behavior rules
- `docs/sprint-context.md` - Current sprint context
- `docs/prompt-library.md` - Reusable prompts
- `docs/api-contracts/` - API specifications
- `docs/architecture/adr/` - Architecture decisions
