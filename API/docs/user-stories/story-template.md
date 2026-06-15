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
- **ADR:** [Link to relevant ADR if applicable]
- **API Contract:** [Link to contract in docs/api-contracts/]
- **Design:** [Link to design docs/mockups if applicable]

## Definition of Done
- [ ] All acceptance criteria met
- [ ] Unit tests written and passing (coverage ≥ threshold)
- [ ] Integration tests written (if applicable)
- [ ] Code follows patterns in .github/copilot-instructions.md
- [ ] No security vulnerabilities introduced
- [ ] API documentation updated (if API changes)
- [ ] PR reviewed and approved
- [ ] Feedback log submitted

---

## Notes for Story Authors

### Making Stories AI-Ready

**Intent Section:**
- Keep to 1-2 sentences
- Focus on business outcome, not technical approach
- Good: "Enable users to update their profile information with validation"
- Poor: "Add a PUT endpoint using Express and validate with Joi"

**Acceptance Criteria:**
- Must be specific and testable
- Include exact data types, formats, status codes
- Specify error behavior explicitly
- Good: "Returns 400 with { code: 'VALIDATION_ERROR', field: 'email' } if email format invalid"
- Poor: "Returns an error if email is wrong"

**Technical Context:**
- List EXACT file paths (src/services/user.service.ts, not "user service")
- Specify which files to read vs. modify
- Identify files that are off-limits
- Name database tables precisely

**Agent Execution Notes:**
- Reference a similar past story for pattern guidance
- Specify THE library to use (not "a validation library" but "express-validator")
- List the 2 most likely mistakes and how to avoid them
- Specify file creation order if dependencies exist

### Story Readiness Checklist

Before marking a story as "ready for AI execution":

- [ ] Intent is clear in 1-2 sentences
- [ ] User story follows "As a / I want / So that" format
- [ ] All ACs are specific and testable
- [ ] All ACs include data types/formats
- [ ] Technical Context has exact file paths
- [ ] APIs and DB tables are named
- [ ] "Must NOT change" section is populated
- [ ] NFRs include at least performance and security
- [ ] Agent Execution Notes reference a similar story
- [ ] A specific library is named (from approved list)
- [ ] No place where AI would need to guess

### Common Story Mistakes

| Mistake | Why It's Bad | How to Fix |
|---------|--------------|------------|
| "Validate input" | Doesn't specify what/how | "Validate email using express-validator. Return 400 with field-level errors if invalid." |
| "Handle errors" | Too vague | "Catch ValidationError → 400, AuthError → 401, NotFoundError → 404. Log all errors with request ID." |
| "Update the database" | Doesn't specify table/columns | "Update users table: set name, email columns. Do NOT modify password_hash." |
| "Similar to previous work" | Doesn't specify which | "Follow the pattern in story-US-075 for API structure and error handling." |
| "Should be fast" | No measurable target | "API response time < 200ms for 95th percentile under 1000 req/min load." |
| No "Must NOT change" | AI modifies wrong files | List all files/folders that are off-limits (legacy/, migrations/, etc.) |

### Example Transformation

**Before (Not AI-Ready):**
```markdown
# Story: Add user profile update

As a user, I want to update my profile.

Acceptance Criteria:
- User can update name and email
- Changes are saved
```

**After (AI-Ready):**
```markdown
# Story: US-089 — User Profile Update

## Intent
Allow authenticated users to update their display name and email with validation and duplicate detection.

## User Story
As a registered user, I want to update my profile name and email so that my account information stays current.

## Acceptance Criteria
- [ ] AC1: PATCH /api/v1/users/:id accepts { name?: string, email?: string }. Returns 200 with updated user object.
- [ ] AC2: Email uniqueness validated. Returns 409 with { code: "EMAIL_IN_USE", field: "email" } if duplicate.
- [ ] AC3: Name must be 2-50 characters. Returns 400 with { code: "VALIDATION_ERROR", field: "name" } if invalid.
- [ ] AC4: Unauthenticated requests return 401.
- [ ] AC5: Users cannot update another user's profile - returns 403.
- [ ] AC6: updated_at timestamp is automatically set on successful update.

## Technical Context
- **Relevant files:**
  - src/modules/users/user.controller.ts (modify)
  - src/modules/users/user.service.ts (modify)
  - src/modules/users/user.repository.ts (read - for uniqueness check)
- **APIs involved:**
  - PATCH /api/v1/users/:id (new endpoint)
- **DB tables:**
  - users (id, name, email, updated_at)
- **Dependencies:** None
- **Must NOT change:**
  - src/models/User.ts (schema locked until migration)
  - src/modules/users/user.validation.ts (existing validation - reuse it)

## Non-Functional Requirements
- **Performance:** < 200ms response for 95th percentile
- **Security:**
  - Validate email format using express-validator
  - Check user owns the resource (id matches authenticated user)
  - Sanitize all inputs before database update
- **Coverage:** ≥ 85% for user.service.ts modifications

## Agent Execution Notes
- **Reference pattern:** story-US-072 (address update) - same pattern
- **Library to use:** express-validator (already approved)
- **Common mistakes to avoid:**
  1. Forgetting the 403 check (user can only update own profile)
  2. Not updating the updated_at timestamp
- **File creation order:**
  1. user.controller.ts (add PATCH endpoint)
  2. user.service.ts (add updateProfile method)
  3. user.controller.test.ts (unit tests)
  4. user.integration.test.ts (API tests for all status codes)

## Related Documentation
- **API Contract:** docs/api-contracts/users-api-contract.md
- **ADR:** docs/architecture/adr/ADR-005-user-profile-validation.md

## Definition of Done
- [ ] All 6 acceptance criteria verified
- [ ] Unit tests ≥ 85% coverage
- [ ] Integration tests cover all status codes (200, 400, 401, 403, 409)
- [ ] Email uniqueness check queries database correctly
- [ ] Ownership check prevents cross-user updates
- [ ] PR reviewed and approved
- [ ] Feedback log submitted
```

---

## Related Documents

- `docs/user-stories/README.md` - Story authoring guidelines
- `.github/copilot-instructions.md` - Coding standards for implementation
- `docs/sprint-context.md` - Current sprint context
- `docs/prompt-library.md` - Prompts for story execution
