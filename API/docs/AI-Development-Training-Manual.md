# AI-Driven Development — Training Manual

## Self-Learning Programme for Engineers

Engineering Excellence / AI Adoption Team — Kellton

2026-05-27

Table of Contents

# **AI-Driven Development Training Manual**

**Self-Learning Programme for Engineers**

| Version | 1.0 |
| :---- | :---- |
| **Date** | 2026-05-27 |
| **Audience** | Architects · Technical Leads · Developers |
| **Format** | Self-Paced Learning |
| **Duration** | 6–8 hours (complete programme) |
| **Owner** | Engineering Excellence / AI Adoption Team |

---

## **Welcome**

This manual is your self-contained guide to working effectively in an AI-driven engineering team. It is designed so you can learn at your own pace, validate your understanding through knowledge checks, and apply what you learn immediately in your daily work.

You do not need a trainer to complete this programme. Everything you need is in this document and the supporting SOP.

---

## **Prerequisites**

Before starting, confirm you have the following:

* Read **SOP-AI-Driven-Development.md** (v1.1)

* Installed **Claude Code** (CLI or desktop app)

* Installed **GitHub Copilot** in your IDE

* Access to your project repository

* Access to the docs/ folder in your project

If any of these are missing, contact your Tech Lead before proceeding.

---

## **How This Manual Is Organised**

| Module | Topic | Estimated Time |
| :---- | :---- | :---- |
| **Module A** | Good Planning in GitHub Copilot | 90 minutes |
| **Module B** | Developing AI Agents | 90 minutes |
| **Module C** | Agent Orchestration | 75 minutes |
| **Module D** | Optimising Token Spend | 60 minutes |
| **Assessment** | Final Knowledge Check | 30 minutes |
| **Glossary** | Key Terms Reference | Reference |

### **Learning Elements Used in This Manual**

| Symbol | Type | Purpose |
| :---- | :---- | :---- |
| **CONCEPT** | Core idea | The principle explained simply |
| **HOW-TO** | Step-by-step | Instructions you can follow today |
| **EXAMPLE** | Worked example | The concept demonstrated in context |
| **EXERCISE** | Your task | Apply the learning in your own project |
| **CHECK ✓** | Knowledge check | Answer before moving to the next section |

---

# **Module A — Good Planning in GitHub Copilot**

***Core Principle:** Copilot produces precise output only when given precise input. Planning is where you build that precision — before any code is written.*

**By the end of this module you will be able to:**

* Use Copilot to analyse an epic for architecture impact

* Decompose raw stories into AI-ready stories using a three-prompt sequence

* Verify story readiness before triggering any agent

* Identify and avoid the four most common planning anti-patterns

---

## **\[ALL ROLES\] — What Good Planning Means in AI-Driven Development**

### **CONCEPT — Why Planning Is Different Now**

In a traditional team, a developer reads a story and starts coding. Ambiguities get resolved through trial and error, and the developer’s experience fills in the gaps.

In an AI-driven team, an agent reads the story and starts coding. **The agent has no intuition. It cannot fill gaps. It will execute whatever it infers — and it will infer confidently.**

This means planning is no longer about estimating effort. It is about **eliminating ambiguity before the agent starts**.

| Traditional Planning Goal | AI-Driven Planning Goal |
| :---- | :---- |
| “Do we know enough to start?” | “Does the story have zero ambiguity that an AI could misinterpret?” |
| **Gap filled by:** Developer judgment, team discussions, code review corrections | **Gap filled by:** The story file itself, CLAUDE.md rules, Agent Execution Notes |

The investment you make in planning directly determines how many correction loops you need during execution. Better planning \= fewer corrections \= faster delivery.

---

## **A1 — Architect: Planning with Copilot**

### **CONCEPT — Your Planning Artifacts Are the AI’s Firmware**

Everything the AI agent believes about your project comes from artifacts you author. Think of them as firmware that programs the agent’s behaviour.

| Your Artifact | What It Controls in the Agent |
| :---- | :---- |
| CLAUDE.md | Behaviour guardrails for every session |
| Architecture Decision Records (ADRs) | AI’s awareness of past decisions — it won’t re-debate closed questions |
| .github/copilot-instructions.md | Copilot’s inline suggestion bias in the IDE |
| NFR specifications | Non-negotiable constraints (security, performance, compliance) |
| Epic architecture note | Scope boundaries for this sprint |

If any of these are missing or out of date, the AI will guess — and it will guess consistently, making the same wrong decision across every story in the sprint.

---

### **HOW-TO — Three-Step Epic Review with Copilot**

Run this before every sprint planning meeting. It takes 30–45 minutes and prevents hours of agent corrections.

**Step 1 — Epic Impact Scan**

Open Copilot Chat and run:

Act as a Solution Architect reviewing this epic for technical impact.

Epic: \[paste epic title and description\]  
Current architecture: \[paste CLAUDE.md Sections 1 and 2\]

Identify:  
1\. New external dependencies this epic introduces  
2\. Module boundaries that will be crossed  
3\. Security or compliance implications  
4\. Data model changes needed  
5\. NFRs that must be explicit in story templates

Output as a checklist I can verify item by item.

For each item Copilot returns, ask yourself: Is this already captured in CLAUDE.md? If not, it becomes a CLAUDE.md update task.

**Step 2 — Draft ADRs with Copilot**

For any decision triggered by this epic:

Draft an Architecture Decision Record for this decision:  
Decision needed: \[describe the choice\]  
Context: \[constraints and options\]  
Existing ADRs for reference: \[paste titles \+ one-line decisions\]

Format:  
\#\# ADR-NNN: \[Title\]  
Date: \[today\] | Status: Draft  
\#\# Context  
\#\# Decision  
\#\# Constraints for AI: \[bullet list of rules for agents to follow\]  
\#\# Consequences

***Critical:** The “Constraints for AI” section is what makes an ADR useful to the agent. Without it, an ADR is history — not instruction.*

**Step 3 — CLAUDE.md Pre-Sprint Validation**

Review these CLAUDE.md sections for gaps given the upcoming sprint:

\[Paste Section 2: Architecture Rules\]  
\[Paste Section 5: AI Behavior Instructions\]

The sprint will cover: \[paste sprint goal\]

What additions would prevent the AI from making wrong assumptions  
about module boundaries, security approach, or approved libraries?

Apply Copilot’s suggested additions and commit the updated CLAUDE.md before sprint planning begins.

---

### **EXAMPLE — Good vs. Poor Pre-Sprint Preparation**

| Aspect | Poor Preparation | Good Preparation |
| :---- | :---- | :---- |
| CLAUDE.md | Last updated 3 sprints ago | Reviewed and updated for this sprint |
| ADR coverage | No ADR for the new payment gateway integration | ADR-007 drafted: “Always use PaymentService wrapper, never call Stripe SDK directly” |
| NFR clarity | NFR says “be secure” | NFR says “Validate all inputs using express-validator. Rate-limit payment endpoints to 10 req/min” |
| Copilot config | copilot-instructions.md not updated | Updated: “Payment module added. Use currency amounts in paise, not ₹” |
| **Result** | AI guesses approach, uses wrong library, security gap found in PR review. 2 stories reworked. | AI follows ADR, uses correct wrapper, validates correctly on first pass. |

---

### **EXERCISE — A1**

***Your task:** Take the epic your team will work on in the next sprint. Run Step 1 (Impact Scan) above. List every item Copilot identified. For each item, answer: Is this already in CLAUDE.md? If not — write the specific CLAUDE.md line or ADR section that would cover it.*

---

### **CHECK ✓ — A1 Knowledge Check**

Answer these before moving on.

**Q1.** An ADR describes an architectural decision but has no “Constraints for AI” section. What does this mean for the agent?

**Q2.** Which is the PRIMARY purpose of updating CLAUDE.md before a sprint?

* 

  1) To document what the team decided in the last retrospective

* 

  2) To eliminate ambiguities the AI would otherwise have to guess at

* 

  3) To track sprint velocity and story count

* 

  4) To replace the need for story-level acceptance criteria

**Q3.** True or False: Copilot can infer security constraints from the codebase without them being written in CLAUDE.md.

---

## **A2 — Technical Lead: Planning with Copilot**

### **CONCEPT — Your Job Is to Make Stories AI-Executable**

You receive raw stories from the Product Owner. Your job is to transform them into documents that an AI agent can execute without guessing. This is not editing — it is a structured enrichment process.

A raw story has business intent. An AI-ready story has business intent **plus** technical context, testable ACs, file paths, boundaries, and execution notes.

---

### **HOW-TO — The Three-Prompt Story Refinement Sequence**

Run these three prompts in sequence for every story. Save the result as docs/user-stories/story-\[ID\].md.

**Prompt 1 — Technical Context Extraction**

I have this raw user story:  
\[paste story from backlog\]

My project tech stack and conventions are in CLAUDE.md:  
\[paste CLAUDE.md Sections 1 and 2\]

Identify:  
\- Which files/modules in a typical \[stack\] app would this touch?  
\- What APIs would need to be created or modified?  
\- What DB tables are likely involved?  
\- What are the most likely hidden technical dependencies?

Use the output to populate the **Technical Context** section of the story file.

**Prompt 2 — Acceptance Criteria Sharpening**

These are the draft acceptance criteria for a user story:  
\[paste raw ACs\]

This story will be implemented by an AI coding agent.  
Rewrite each AC so that:  
1\. It is specific and objectively testable  
2\. It includes the exact data type or format expected in outputs  
3\. It specifies error behaviour where applicable  
4\. An automated test can verify it

Add any ACs the AI would need that are currently missing.

**Prompt 3 — Agent Execution Notes**

Here is the refined user story:  
\[paste story with technical context and sharpened ACs\]

Here are patterns from previous similar stories:  
\[paste 1–2 relevant patterns from prompt-library.md\]

Write an 'Agent Execution Notes' section that:  
\- References the most relevant past story for pattern guidance  
\- Identifies the ONE specific library or pattern that MUST be used  
\- Lists the top 2 places an AI is likely to go wrong on this story  
\- Specifies the order in which files should be created

---

### **EXAMPLE — Before and After Story Refinement**

**Before (Raw Story from Backlog)**

*Story: Add user profile update functionality AC1: User can update their name and email AC2: Changes are saved to the database AC3: User sees a success message*

**After (AI-Ready Story)**

\#\# Story: US-089 — User Profile Update

\#\# Intent  
Allow authenticated users to update their display name and email  
address, with validation and duplicate email detection.

\#\# Acceptance Criteria  
\- \[ \] AC1: PATCH /api/users/:id accepts { name: string, email: string }.  
           Returns 200 with updated user object on success.  
\- \[ \] AC2: Email uniqueness validated before save. Returns 409 with  
           { code: "EMAIL\_IN\_USE", field: "email" } on conflict.  
\- \[ \] AC3: Name must be 2–50 characters. Returns 400 with  
           { code: "VALIDATION\_ERROR", field: "name" } if invalid.  
\- \[ \] AC4: Unauthenticated requests return 401\.  
\- \[ \] AC5: Users cannot update another user's profile — return 403\.

\#\# Technical Context  
\- Relevant files: src/modules/users/, src/services/user.service.ts  
\- DB table: users (id, name, email, updated\_at)  
\- Must NOT change: src/models/User.ts (schema locked until migration)  
\- Pattern reference: See US-072 (address update) for layer structure

\#\# Agent Execution Notes  
\- Follow Module → Servlet → Service pattern (same as US-072)  
\- Use express-validator for input validation (not manual checks)  
\- Most likely errors: (1) skipping the 403 ownership check,  
                      (2) not updating updated\_at timestamp  
\- File order: user.module.ts → user.servlet.ts → user.service.ts → tests

The gap between these two versions is where agent failures happen.

---

### **EXERCISE — A2**

***Your task:** Pick one story currently in your backlog. Run all three prompts above. Open the Story Readiness Checklist from SOP Appendix C. Count how many items were missing before you ran the prompts. Save the AI-ready version to docs/user-stories/.*

---

### **CHECK ✓ — A2 Knowledge Check**

**Q4.** What is the purpose of the “Agent Execution Notes” section in a story file?

**Q5.** A developer tells you “AC2 says the email should be saved.” Is this AC sufficient for an AI agent? What is missing?

**Q6.** Which item, if missing from a story, is most likely to cause scope drift by the agent?

* 

  1) The sprint goal

* 

  2) The “Must NOT change” section

* 

  3) The story’s business justification

* 

  4) The developer’s name

---

## **A3 — Developer: Planning with Copilot**

### **CONCEPT — Your Planning Role Is Verification, Not Creation**

By the time a story reaches you, the Tech Lead has enriched it. Your job in planning is not to add more content — it is to **verify that the content is accurate and complete** before you trigger the agent.

A story with a wrong file path is worse than a story with no file paths. The agent will confidently read the wrong file and proceed.

---

### **HOW-TO — The 15-Minute Pre-Execution Ritual**

Do this before triggering any Claude Code session.

| Step | Time | Action |
| :---- | :---- | :---- |
| **1\. Read the story in full** | 5 min | Read story-\[ID\].md completely. Ask: “If I were the AI, would I have everything I need?” |
| **2\. Verify file paths** | 2 min | For every file in Technical Context: confirm it exists at that exact path. Correct any wrong paths before proceeding. |
| **3\. Copilot context check** | 5 min | Open the most relevant file. Ask Copilot Chat: “What patterns should the implementation follow? Any conventions the AI should respect?” Add anything new to Agent Execution Notes. |
| **4\. Dependency check** | 3 min | Does this story depend on something not yet merged? If yes: ask Tech Lead for the API contract and implement using mocks. |

---

### **EXAMPLE — What Happens Without This Ritual**

**Scenario:** Developer skips path verification.

* Story says: src/services/userService.ts

* Actual file: src/services/user.service.ts (renamed last sprint)

* Agent reads CLAUDE.md ✓ then tries to read the wrong path ✗

* Agent finds src/legacy/userService.ts (old, deprecated)

* Agent builds on deprecated patterns

* PR review catches it — story sent back for rework

* **Time lost: \~3 hours. Cause: a 2-minute step was skipped.**

---

### **EXERCISE — A3**

***Your task:** Before your next story execution, complete all four steps of the pre-execution ritual. Write down one thing you found that was missing or incorrect in the story. Add it to the story file and note it in your feedback log.*

---

### **CHECK ✓ — A3 Knowledge Check**

**Q7.** A story file lists a file path that doesn’t exist. What should you do before triggering the agent?

**Q8.** Your story depends on an API endpoint that another developer is building and hasn’t merged yet. What is the correct approach?

* 

  1) Wait for their PR to merge before starting

* 

  2) Ask the Tech Lead for the API contract and implement against a mock

* 

  3) Implement your story without any dependency on that endpoint

* 

  4) Implement the API yourself and combine both stories

**Q9.** You ask Copilot about the current file’s patterns. Copilot surfaces a validation convention not mentioned in the story. What do you do?

---

# **Module B — Developing AI Agents**

***Core Principle:** An agent is not a chat session. It is a configured, context-loaded, instruction-following system that behaves predictably and gets better with each sprint.*

**By the end of this module you will be able to:**

* Design the three-layer agent identity model

* Write a complete CLAUDE.md with all required sections

* Build and maintain a prompt library with five categories

* Create slash commands for your most-used prompts

* Apply the four-type agent failure recovery protocol

---

## **\[ALL ROLES\] — What Makes an Agent Different From a Chat Session**

### **CONCEPT — The Agent vs. Chatbot Distinction**

| Dimension | Chatbot Session | AI Agent (Claude Code) |
| :---- | :---- | :---- |
| **Memory** | None (per message) | Persistent (memory files, CLAUDE.md, sprint context) |
| **Tools** | Text only | Reads files, runs commands, writes code, runs tests |
| **Scope** | One answer | Multi-file, multi-step tasks across an entire story |
| **Improvement** | Start over each time | Gets better each sprint as memory and prompts are refined |

This is why setup work (CLAUDE.md, memory files, prompt library) pays off: you are building a system that improves, not a session you restart.

---

## **B1 — Architect: Designing the Agent System**

### **CONCEPT — The Three-Layer Agent Design Model**

Every agent has three layers of identity. Architects design the first two. Tech Leads and Developers inject the third.

| Layer | Description | Lives In | Changes |
| :---- | :---- | :---- | :---- |
| **Layer 1: Identity** | “Who this agent always is, regardless of task” | CLAUDE.md Section 5 — AI Behavior Instructions | Never (or very rarely) |
| **Layer 2: Project Persona** | “What this agent knows about this specific project” | CLAUDE.md Sections 1–4 | Per epic or sprint |
| **Layer 3: Task Persona** | “What this agent knows about the current task” | Story file \+ sprint-context.md | Per story |

**Layer 1 Example (Identity):** \> “You are a backend engineer in a fintech application. You prioritise security above performance. You never bypass validation. You ask before modifying files outside the story’s defined scope.”

**Layer 2 Example (Project Persona):** \> “This project uses Node.js 20, Express, Sequelize on Postgres. All APIs follow Module → Servlet → Service layering. Auth uses JWT stored in httpOnly cookies.”

**Layer 3 Example (Task Persona):** \> “This story adds a KYC verification endpoint. Follow the AML check pattern at src/compliance/aml.ts. Integrate with the Onfido SDK (already installed).”

---

### **HOW-TO — Writing the CLAUDE.md AI Behavior Section**

Section 5 of CLAUDE.md is the most critical. Use this template:

**\#\# Section 5: AI Behavior Instructions**

**\#\#\# Always Do**  
\- Read CLAUDE.md and docs/sprint-context.md before starting any task  
\- Generate an implementation plan and wait for explicit approval  
  before writing any code  
\- Run tests after completing each file — not only at the end  
\- Ask explicitly if a requirement is ambiguous; do not assume  
\- Follow the layered architecture: *\[*Module*\]* → *\[*Servlet*\]* → *\[*Service*\]*

**\#\#\# Never Do**  
\- Modify files in /legacy or migrations already applied  
\- Add packages not listed in the Approved Libraries section  
\- Commit or suggest hardcoded secrets, API keys, or passwords  
\- Bypass input validation for any reason  
\- Modify files outside the scope defined in the current story

**\#\#\# When Uncertain**  
\- State the ambiguity explicitly before proceeding  
\- Propose two options and ask which to follow  
\- Default to the most restrictive interpretation of security requirements

**\#\#\# Approved Libraries**  
*\[*Group by category: HTTP client, ORM, testing, auth, validation*\]*

**\#\#\# Architecture Boundaries**  
*\[*Define what may import from what — module isolation rules*\]*

---

### **HOW-TO — Agent Memory File Structure**

Create this folder structure at the start of every project:

.claude/memory/  
├── project-patterns.md      (established patterns)  
├── anti-patterns.md         (things AI must never repeat)  
├── domain-glossary.md       (domain terms mapped to code)  
├── api-contracts.md         (key API shapes and fields)  
└── team-preferences.md      (style preferences beyond linting)

**Memory file formats:**

project-patterns.md entry format:

\# Pattern: \[Name\]  
Context: \[when to use this pattern\]  
Example: \[code snippet or pseudo-code\]  
Source: \[story ID or ADR\]

anti-patterns.md entry format:

\# Anti-pattern: \[Name\]  
What AI did wrong: \[description\]  
Why it's wrong: \[explanation\]  
Correct approach: \[description or snippet\]  
First seen in: \[story ID\]

**First-sprint seeding prompt for Copilot:**

I am setting up AI agent memory files for a new project.  
Project: \[description\]  
Stack: \[list\]  
Domain: \[fintech / e-commerce / healthcare / etc.\]  
Key architecture patterns: \[list 3–5\]

Generate initial content for:  
1\. project-patterns.md — 5 core patterns this stack uses  
2\. domain-glossary.md — 10 domain terms for this app type  
3\. team-preferences.md — 5 common style preference entries

I will review and edit each before committing.

---

### **EXERCISE — B1**

***Your task:** Open your project’s CLAUDE.md. Check Section 5\. Does it have all three sub-sections (Always Do, Never Do, When Uncertain)? For each missing entry, write the specific rule based on your project’s actual constraints. Commit the updated CLAUDE.md.*

---

### **CHECK ✓ — B1 Knowledge Check**

**Q10.** Which layer of the agent design model do Architects own permanently?

**Q11.** An agent consistently adds a library that is not approved. Which CLAUDE.md sub-section should contain the rule to stop this?

**Q12.** The anti-patterns.md memory file contains a mistake the AI made in Sprint 3\. Why is this valuable — what does it do for future sessions?

---

## **B2 — Technical Lead: Building Your Agent Toolkit**

### **CONCEPT — The Prompt Library Is Your Team’s Most Valuable Asset**

A prompt that works well is repeatable, shareable, and improvable. Your prompt library transforms individual discoveries into team capability. Every validated prompt in it makes every developer more effective — immediately.

---

### **HOW-TO — Prompt Library Structure**

Save your library at docs/prompt-library.md. Each entry must have:

**\#\# CATEGORY: \[Category Name\]**

**\#\#\# \[prompt-name\]**  
\*\*When to use:\*\* *\[*Specific scenario*\]*  
\*\*Variables:\*\* $STORY\_PATH, $CONTEXT\_FILES  
\*\*Validated:\*\* Yes — Sprint *\[*N*\]*, Story *\[*ID*\]*  
\*\*Token estimate:\*\* *\[*range*\]*

*\[*The full prompt text*\]*  
\---

**The five required prompt categories:**

| Category | What It Covers |
| :---- | :---- |
| **1\. Feature Implementation** | Implementing new stories end-to-end (plan, code, tests) |
| **2\. Bug & Diagnosis** | Test failures, reported bugs, regression investigation |
| **3\. Refactoring** | Restructuring code without changing behaviour or API |
| **4\. Code Review** | Pre-PR self-review, AC verification, security spot-check |
| **5\. Sprint Operations** | Retrospective, planning breakdown, sprint-context.md updates |

---

### **HOW-TO — The Three Core Slash Commands**

Every project must have these three commands in .claude/commands/:

**implement-story.md**

Read .claude/CLAUDE.md, docs/sprint-context.md, and  
docs/user-stories/$ARGUMENTS.md plus all technical context  
files listed in the story. Summarise your understanding.  
Generate an implementation plan with files, functions, and  
test strategy. Wait for my approval. Then implement fully,  
running tests after each file. Report final results.

**review-output.md**

Review the current git diff against the acceptance criteria  
in docs/user-stories/$ARGUMENTS.md. For each AC, state:  
PASS / FAIL / NOT VERIFIABLE.  
Also check for: architectural violations, security issues,  
test quality (meaningful assertions vs. padding), hardcoded  
values. Output a summary table then specific fixes.

**sprint-retro.md**

Read all feedback files in docs/agent-feedback/sprint-$ARGUMENTS/.  
Analyse patterns across all stories. Output:  
1\. Top 5 prompt improvements (specific before/after text)  
2\. CLAUDE.md rules to add or update (exact wording)  
3\. New slash commands to create (full prompt text)  
4\. Anti-patterns to add to anti-patterns.md  
5\. Success patterns to reinforce in project-patterns.md  
Be specific and actionable.

---

### **HOW-TO — Specialised Agent Commands**

**Security Review Agent** (.claude/commands/security-review.md)

Review the current git diff for security vulnerabilities.  
Check specifically for:  
1\. SQL/NoSQL injection — all query construction  
2\. Authentication bypass — all auth middleware  
3\. Insecure direct object references — all ID-based lookups  
4\. Sensitive data in logs or API responses  
5\. Input validation gaps — all request body and param handling  
6\. Hardcoded credentials or API keys  
7\. OWASP Top 10 items relevant to our stack: \[list\]

Output a severity table: BLOCKER | CRITICAL | MAJOR | INFO  
For each finding: file:line | description | recommended fix

**DB Migration Agent** (.claude/commands/create-migration.md)

Generate a database migration for: $ARGUMENTS  
Follow the convention in \[path to existing migration\].  
Include:  
\- up() function with all schema changes  
\- down() function that fully reverses all changes  
\- Comments explaining each change  
\- Index additions for new or modified columns  
Naming: YYYYMMDDHHMMSS-\[description\].\[ext\]  
Show the migration for review before running anything.

---

### **EXERCISE — B2**

***Your task:** Count the prompts currently in your team’s prompt library. If fewer than 10, use Copilot to generate prompts for the missing categories. Add them to docs/prompt-library.md. Then create (or verify) the three core slash commands in .claude/commands/.*

---

### **CHECK ✓ — B2 Knowledge Check**

**Q13.** A developer finds a prompt that works well for API generation. They use it three times. What should happen next?

**Q14.** The /review-output command marks an AC as NOT VERIFIABLE. Why is this a valid and important outcome?

**Q15.** True or False: The security review agent should be run in the same Claude Code session as the implementation, so it has full context about decisions made.

---

## **B3 — Developer: Operating AI Agents Effectively**

### **CONCEPT — What the Agent Sees (And What It Doesn’t)**

| Can Access | Cannot Access |
| :---- | :---- |
| Your message right now | Your entire codebase (reads only files you point to) |
| \~/.claude/CLAUDE.md (global rules) | Slack messages or verbal conversations |
| .claude/CLAUDE.md (project rules) | Other developers’ Claude sessions |
| Files you explicitly tell it to read | Previous sessions (unless in memory files) |
| Files it finds by searching (when asked) | Jira — unless you paste the content |

**This means:** every piece of information the agent needs must be in a file it reads, or in your message. Nothing else exists from its perspective.

---

### **HOW-TO — The Golden Context Load Prompt**

Run this at the start of every story session:

Before we start, read these files in this order:  
1\. .claude/CLAUDE.md  
2\. docs/sprint-context.md  
3\. docs/user-stories/story-\[ID\].md  
4\. \[each file listed in Technical Context in the story\]

After reading all of them, confirm by telling me:  
(a) What this story needs to accomplish — one sentence  
(b) Which specific files you will create or modify  
(c) Any ambiguity or missing information you spotted

Do NOT start implementing. Wait for my confirmation.

**Why every part matters:**

| Part | Why It Matters |
| :---- | :---- |
| “read these files in order” | Ensures CLAUDE.md is read before the story, so rules are established before task context |
| “confirm by telling me (a)(b)(c)” | Forces Claude to demonstrate understanding. Catches misunderstandings before any code is written |
| “Do NOT start implementing” | Prevents eager execution before you’ve validated understanding |

---

### **HOW-TO — The Four Failure Recovery Protocols**

**Failure Type 1 — Wrong Approach**

*Symptom:* The implementation plan doesn’t match the architecture.

Stop. Do not implement this plan.

The issue with your approach: \[describe specifically\]  
The correct approach: \[describe\]  
The pattern to follow: \[file:function reference\]

Revise your plan with this correction and show me the  
updated plan before proceeding.

**Failure Type 2 — Scope Drift**

*Symptom:* Agent modified or plans to modify files outside the story’s scope.

Stop. You have modified \[filename\], which is outside  
this story's scope.

Revert all changes to \[filename\].  
The only files in scope for this story are: \[list from story file\].  
Continue implementation within these boundaries only.

**Failure Type 3 — Test Failure Loop**

*Symptom:* Agent has tried to fix a failing test 3 or more times.

Stop the self-correction loop.

Show me:  
(1) The exact test that is failing  
(2) The exact error message  
(3) Your current understanding of the root cause

Wait. I will diagnose and tell you the correct fix direction.

***Rule:** Never let the agent continue past 3 self-correction attempts. Escalate to Tech Lead if you cannot diagnose within 10 minutes.*

**Failure Type 4 — Missing Context**

*Symptom:* Agent asks about something the story should have specified.

Answer the question, then update the story file:

The answer is \[X\]. I am adding this to the story context now.  
Continue implementation using \[X\].

Then add that information to the story’s Technical Context section and log it in your feedback file.

---

### **The Five Golden Rules of Agent Operation**

| Rule | What It Means |
| :---- | :---- |
| **1\. Always load context first** | Never send a one-line task without first running the context load prompt |
| **2\. Always review the plan** | Never approve execution without reviewing the implementation plan |
| **3\. Stop on scope drift** | The moment an out-of-scope file is touched — stop immediately |
| **4\. Escalate at 3 failures** | After 3 self-correction failures, escalate to Tech Lead |
| **5\. Log every correction** | Your corrections feed the retrospective that improves the next sprint |

---

### **EXERCISE — B3**

***Your task:** Run the context load prompt on your current story. Before approving the plan, ask Claude: “What would you do if \[the most likely edge case for this story\]?” Evaluate the answer against the acceptance criteria. If it does not match — redirect before a single line of code is written.*

---

### **CHECK ✓ — B3 Knowledge Check**

**Q16.** Claude has tried three times to fix a failing test and keeps producing different errors. What is the correct action?

**Q17.** You discover mid-execution that Claude is importing an unapproved library. What do you do?

* 

  1) Let it continue and fix it in the PR review

* 

  2) Stop Claude immediately, check with Tech Lead, then redirect

* 

  3) Add the library to the approved list yourself

* 

  4) Ask Claude to use a different function from the same library

**Q18.** The context load prompt asks Claude to confirm “(c) Any ambiguity or missing information you spotted.” Claude lists two things it’s unsure about. What is the correct next step?

---

# **Module C — Agent Orchestration**

***Core Principle:** Orchestration is making multiple agents work in sequence or in parallel without losing coherence. Architects design the stage. Tech Leads conduct. Developers play their part.*

**By the end of this module you will be able to:**

* Identify the four orchestration patterns and when to use each

* Build a sprint orchestration map

* Apply the four multi-developer protocols

* Execute your role correctly in a parallel development flow

* Know when and how to intervene during agent execution

---

## **\[ALL ROLES\] — The Orchestration Mental Model**

### **CONCEPT — Humans as Conductors, Agents as Performers**

| Role | Analogy | Responsibilities |
| :---- | :---- | :---- |
| **Architect** | Writes the score | CLAUDE.md, ADRs, NFRs — defines what agents must always do |
| **Tech Lead** | Conducts the performance | Sprint map, protocols, convergence points — decides when each agent plays |
| **Developer** | Plays their part | Story execution, monitoring, escalation — executes one story cleanly |

Good orchestration means the outputs of agents combine into a coherent system — not a collection of individually correct but incompatible pieces.

---

## **C1 — Architect: Designing the Orchestration Architecture**

### **CONCEPT — The Four Orchestration Patterns**

**Pattern 1: Sequential Chain**

Use when: Each agent’s output is the next agent’s input.

\[Analysis Agent\] → \[Design Agent\] → \[Implementation Agent\] → \[Review Agent\]

*Your design task:* Define the output format of each stage so the next stage has a stable, predictable input. Document in docs/orchestration-flows/.

**Pattern 2: Parallel Agents**

Use when: Tasks are independent and can run simultaneously.

                ┌─► \[Backend Implementation Agent\]  ────┐  
\[Story Split\] ──┤                                         ├──► \[Integration Test Agent\]  
                └─► \[Frontend Implementation Agent\] ────┘

*Your design task:* Ensure the shared contract (API spec) is committed and frozen before parallel execution begins.

**Pattern 3: Review-Loop**

Use when: Quality assurance needs an independent AI perspective.

\[Implementation Agent\] → \[Review Agent\] → \[Fix Agent\] → ✓  
     (Session 1\)             (Session 2\)     (Session 1\)

*Your design task:* The review agent must be context-isolated from the implementation agent. A reviewer who remembers making the decisions cannot review them impartially.

**Pattern 4: Specialist Agents**

Use when: Different tasks require fundamentally different context and expertise.

\[General Agent\] ──► \[Security Review Specialist\]  
                ──► \[Performance Analyst Specialist\]  
                ──► \[Documentation Specialist\]

*Your design task:* Each specialist reads only the minimum context it needs. Do not load the full project history into every specialist.

---

### **HOW-TO — Orchestration Design Checklist**

Before finalising your sprint’s orchestration design:

| Check | Question |
| :---- | :---- |
| Stage handoff | Is the output format of Stage N the input format of Stage N+1? |
| Parallel independence | Are parallel tracks truly independent (no shared files being written)? |
| Convergence | Is there a defined merge point where parallel outputs come together? |
| Review isolation | Is the review agent context-isolated from the implementation agent? |
| Specialist scope | Do specialist agents read only the minimum context they need? |
| CLAUDE.md coverage | Does CLAUDE.md have rules covering each agent type in the flow? |
| Human gate | Is there at least one human decision gate before production impact? |

---

### **EXERCISE — C1**

***Your task:** Map last sprint’s development work against the four patterns. Which pattern does each phase fit? Were any sequential phases that could have been parallel? Document what you’d change for next sprint.*

---

### **CHECK ✓ — C1 Knowledge Check**

**Q19.** Two developers are running parallel Claude sessions on backend and frontend. The backend developer wants to change an API response field name. What should they do?

**Q20.** Why must the Review-Loop pattern use a new Claude session rather than continuing the implementation session?

---

## **C2 — Technical Lead: Orchestrating the Sprint**

### **CONCEPT — The Sprint Orchestration Map**

Before the sprint begins, you need a conductor’s score: a document mapping which agent runs when, what it produces, and where the human gates are. Create docs/sprint-\[N\]-orchestration.md at sprint kickoff.

---

### **HOW-TO — Sprint Orchestration Map Template**

**Week 1**

| Day | Pattern | Activity | Agent | Output | Gate |
| :---- | :---- | :---- | :---- | :---- | :---- |
| 1–2 | Sequential | API Contract Generation | Claude Code (Tech Lead) | docs/api-contracts/sprint-\[N\]-contracts.md | Architect sign-off |
| 2–5 | Parallel | Backend \+ Frontend Implementation | Developer A \+ Developer B | PRs to develop | G1–G4 per PR |

**Week 2**

| Day | Pattern | Activity | Agent | Output | Gate |
| :---- | :---- | :---- | :---- | :---- | :---- |
| 1 | Sequential | Integration Test Generation | Claude Code (Tech Lead) | docs/tests/integration-sprint-\[N\].md | Tech Lead confirms compatibility |
| 2–3 | Review-Loop | Security Review | /security-review per PR | Findings table | All BLOCKERs resolved |
| 4 | Parallel | Documentation \+ QA Handover Notes | Copilot per developer | Per-story handover docs | Async Tech Lead review |
| 5 | Sequential | Sprint Retrospective \+ Agent Tuning | /sprint-retro \[N\] | CLAUDE.md \+ prompt updates | Architect reviews CLAUDE.md changes |

---

### **HOW-TO — Four Multi-Developer Protocols**

| Protocol | Rule |
| :---- | :---- |
| **1\. Shared Context Rule** | Every Claude session reads the same committed CLAUDE.md. Never allow a locally-edited, uncommitted CLAUDE.md. CLAUDE.md changes go through PR and review like code. |
| **2\. API Contract Freeze** | When parallel tracks share an API boundary: contract must be committed and approved before parallel starts. Neither agent may modify the contract during parallel execution. Any change requires Tech Lead decision and both sides to re-sync. |
| **3\. Integration Gate** | Before running integration tests: each parallel track must have passed quality gates G1–G4 independently. Tech Lead confirms outputs are structurally compatible before integration agent runs. |
| **4\. Feedback Consolidation** | Before running /sprint-retro: collect all docs/agent-feedback/sprint-\[N\]/story-\*.md files and overrides.md. Run /sprint-retro \[N\]. Tech Lead applies judgment to recommendations. Architect reviews before CLAUDE.md changes are committed. |

---

### **EXERCISE — C2**

***Your task:** Create the sprint orchestration map for your current or next sprint. Classify each stage, define inputs and outputs, and mark human gates. Share it with your team at sprint kickoff.*

---

### **CHECK ✓ — C2 Knowledge Check**

**Q21.** A backend developer wants to add a new field to the API response on Day 3\. The contract was frozen at sprint start. What must happen before they can make this change?

**Q22.** Claude produces five CLAUDE.md update recommendations from /sprint-retro. What is the correct next step — who reviews them and how?

---

## **C3 — Developer: Your Role in the Orchestration**

### **CONCEPT — You Are the Orchestrator of One Agent**

| Phase | Who Acts | What Happens |
| :---- | :---- | :---- |
| Story Assignment | — | You receive the story |
| Context Verification | **You** | 15-minute pre-execution ritual |
| Context Load | **You** | Trigger Claude with context load prompt |
| Plan Review | **You** | Approve or redirect (once, specifically) |
| Execution | **Claude** | Writes code; you monitor |
| AC Validation | **You** | Run /review-output \[ID\] |
| PR Creation | **You** | Claude generates description; you review and submit |
| Feedback Log | **You** | Submit after every story — no exceptions |

You are the human-in-the-loop at every gate. You are not the coder. You are the quality controller for one AI agent on one story.

---

### **HOW-TO — Monitoring Agent Execution**

During Phase 3 (Claude is writing code), actively monitor for three things:

| What to Watch | Warning Sign | Intervention |
| :---- | :---- | :---- |
| **Files being written** | A new file appears that wasn’t in the approved plan | STOP: “Stop. \[filename\] was not in the approved plan. Why are you creating it? Show me your reasoning.” |
| **Libraries being imported** | A new import not on the approved list | STOP: “Stop. \[library\] is not in our approved list. Do not proceed. I will check with the Tech Lead.” |
| **Pattern consistency** | New code looks completely different from existing code in the same module | PAUSE: “Stop. The pattern you’re using doesn’t match \[existing file:function\]. Align your implementation.” |

**Intervention thresholds:**

| Signal | Action |
| :---- | :---- |
| Scope drift / unapproved library / security issue | Stop immediately |
| Wrong pattern / questionable test quality | Pause and redirect |
| Minor style difference / Claude self-correcting | Let continue |

---

### **HOW-TO — Working in Parallel Without Blocking**

When your story depends on an API another developer is building:

1. Get the API contract from docs/api-contracts/ (Tech Lead published it)

2. Tell Claude:

The \[endpoint\] API does not exist yet.  
Use the contract at docs/api-contracts/sprint-\[N\]-contracts.md.  
Create a mock in tests/mocks/ that implements this contract.  
My tests should use the mock, not the real endpoint.

3. Implement your story fully against the mock

4. When the real API merges, run integration tests to verify alignment

5. Fix any gaps — they will be small since both sides used the same contract

---

### **EXERCISE — C3**

***Your task:** On your next story execution, draw the six-phase flow on paper before you start. After completion, circle which phases needed intervention. Record what triggered each intervention in your feedback log.*

---

### **CHECK ✓ — C3 Knowledge Check**

**Q23.** During execution, you notice Claude created a file src/utils/payment-helper.ts that was not in the approved plan. What do you do?

**Q24.** True or False: If Claude’s code uses slightly different spacing and variable naming from the existing codebase, you should stop it and redirect immediately.

---

# **Module D — Optimising Token Spend**

***Core Principle:** Tokens are a measure of communication efficiency. A well-structured prompt that gets the right result in one pass is always better than five iterative refinements.*

**By the end of this module you will be able to:**

* Understand how design decisions drive token spend

* Build token-efficient prompts using the five-component structure

* Apply five practical token-saving techniques

* Identify and eliminate common token waste patterns

* Track prompt efficiency metrics each sprint

---

## **\[ALL ROLES\] — Understanding Token Spend**

### **CONCEPT — What Tokens Are and Why They Matter**

Every word in your prompt and every word in Claude’s response costs tokens. Poor prompting compounds the cost:

| Scenario | Tokens Used | Result |
| :---- | :---- | :---- |
| **Good prompt (one pass):** Prompt 400 \+ Plan 300 \+ Code 1,200 | \~1,900 tokens | Correct implementation |
| **Poor prompt (four correction loops):** Initial 50 \+ Wrong output 800 \+ Correction 1 (100) \+ Revision 900 \+ Correction 2 (200) \+ Revision 1,000 \+ Correction 3 (150) \+ Final revision 900 | \~4,100 tokens | Worse result |

This is not just a cost issue — it is a productivity issue. Every correction loop is 5–15 minutes of waiting and reviewing. A 90-minute story becomes a 4-hour story.

---

## **D1 — Architect: Token Governance**

### **CONCEPT — Your Decisions Have the Biggest Multiplier**

A single well-written CLAUDE.md rule prevents dozens of wasted correction loops across all stories in all sprints.

| Decision | Cost if Done Poorly | Cost if Done Well |
| :---- | :---- | :---- |
| Missing CLAUDE.md rule (e.g., “use express-validator”) | 3+ correction loops per story \= \~4,000 tokens/story | One clear rule: \~50 tokens. Saves 2,000–5,000 tokens/story |
| ADR without “Constraints for AI” | AI re-debates decided questions \= \~1,500 tokens/story | 2-line AI constraint block \= \~30 tokens. Saves \~1,500/story |
| Vague NFR (“be secure”) | AI implements minimal security, review catches gaps | Specific NFR text \= \~40 tokens. Saves \~1,000+/review |
| Unapproved library not in deny list | Wrong library used, full refactor needed \= \~10,000 tokens | Explicit deny list \= \~60 tokens. Saves entire re-implementation |

---

### **HOW-TO — The CLAUDE.md Token Budget**

| Section | Target Size |
| :---- | :---- |
| Section 1: Project Overview | 100–200 tokens |
| Section 2: Architecture Rules | 300–500 tokens |
| Section 3: Code Style | 200–300 tokens |
| Section 4: Testing Standards | 150–200 tokens |
| Section 5: AI Behavior | 200–300 tokens |
| **Total target** | **1,000–1,500 tokens** |

If CLAUDE.md exceeds 2,000 tokens:

* Move historical context to ADR files

* Move pattern examples to project-patterns.md (reference it, don’t inline it)

* Merge duplicate rules

* Delete rules for stack components no longer in use

---

### **EXERCISE — D1**

***Your task:** Measure your current CLAUDE.md. Copy-paste it into any token counter (Claude.ai works). If over 2,000 tokens, identify three sections that could be shortened or moved to ADR/memory files without losing any enforcement value. Make the changes and measure again.*

---

### **CHECK ✓ — D1 Knowledge Check**

**Q25.** Your CLAUDE.md has a 600-token section explaining the history of why the team chose PostgreSQL over MySQL, including meeting notes. What should happen to this content?

**Q26.** An ADR has this Constraints for AI section: “Consider security.” How would you rewrite this to be token-efficient and actionable?

---

## **D2 — Technical Lead: Token Efficiency in Prompt Engineering**

### **CONCEPT — The Prompt Efficiency Spectrum**

| Prompt | Interactions Needed | Tokens Used | Quality |
| :---- | :---- | :---- | :---- |
| "Help me with login" | 5+ back-and-forths | \~5,000 | Poor |
| "Write a login endpoint" | 3+ clarifications | \~3,000 | Mediocre |
| "Read story-042 and implement it" | 1–2 passes | \~2,000 | Good |
| "/implement-story story-042" | 1 pass | \~1,500 | Best |

The difference is not prompt length — it is **precision and pre-loaded context**.

---

### **HOW-TO — The Five-Component Efficient Prompt**

| Component | Tokens | Example | Why |
| :---- | :---- | :---- | :---- |
| **1\. Role Priming** | 10–20 | “Act as a backend engineer following our CLAUDE.md conventions.” | Sets operating mode without repeating all rules |
| **2\. Context Reference** | 5–15 | “Read the story file at docs/user-stories/story-042.md” | Claude reads files natively — pasting duplicates the cost |
| **3\. Task Scope** | 20–50 | “Implement only the backend. Do not touch frontend files.” | Prevents scope drift \= prevents correction loops |
| **4\. Output Format** | 10–30 | “Output as a table: File, Change, Reason” | Only when format genuinely helps — don’t add it reflexively |
| **5\. Gate Instruction** | 10–20 | “Show the plan first. Wait for approval before writing code.” | A plan costs 200 tokens to review; a wrong implementation costs 2,000+ to correct |

---

### **HOW-TO — Five Token-Saving Techniques**

| Technique | Expensive Version | Efficient Version | Saving |
| :---- | :---- | :---- | :---- |
| **1\. File reference vs. paste** | “Here is the user service: \[paste 300 lines\]” | “Read src/services/user.service.ts” | \~400 tokens |
| **2\. Pattern anchoring** | \[200-token explanation of the pattern\] | “Follow the pattern in src/services/order.service.ts” | \~180 tokens |
| **3\. Incremental confirmation** | One giant prompt → wrong output → re-explain everything | Load → confirm → plan → confirm → execute | Eliminates 2–5 correction loops |
| **4\. Slash commands** | Type the same 200-token prompt every story | /implement-story story-042 | \~150 tokens \+ developer time |
| **5\. Memory files** | “We use this pattern because \[300 tokens of history\]…” | “Read .claude/memory/project-patterns.md for our conventions” | \~250 tokens, reusable forever |

---

### **HOW-TO — The Sprint Efficiency Scorecard**

Track these every sprint. They should improve as CLAUDE.md and the prompt library mature.

| Metric | Target |
| :---- | :---- |
| Stories completed in one pass | \> 70% |
| Average correction loops per story | \< 2 |
| Stories using slash commands | \> 90% |
| Context loaded via file reference | \> 80% |
| Stories requiring full re-run | \< 5% |

**Sprint retrospective token analysis prompt:**

Review these developer feedback logs: \[paste all logs\]

Identify instances where:  
1\. AI was corrected for something CLAUDE.md should have specified  
2\. Developer repeated context already available in the story file  
3\. A correction prompt was longer than the original task prompt  
4\. AI asked for information that should have been in the story file

For each instance, suggest the specific fix:  
\- Exact CLAUDE.md rule to add  
\- Exact prompt library entry  
\- Story template addition  
\- New slash command

Estimate token savings per story if each fix were applied.

---

### **EXERCISE — D2**

***Your task:** Review three feedback logs from the last sprint. For every correction made, ask: “Was this avoidable with a better initial prompt or CLAUDE.md rule?” For each “yes” — write the specific fix. Add it to either CLAUDE.md or the prompt library.*

---

### **CHECK ✓ — D2 Knowledge Check**

**Q27.** A developer pastes 400 lines of the existing user service into their prompt “so Claude has full context.” What is the better approach and why?

**Q28.** Which of the five prompt components is always worth including even on a very short prompt?

* 

  1) Output format

* 

  2) Gate instruction

* 

  3) Role priming

* 

  4) Task scope

**Q29.** The sprint efficiency scorecard shows only 40% of stories complete in one pass. Where should you look first to fix this?

---

## **D3 — Developer: Token Efficiency in Daily Operation**

### **CONCEPT — The Token Cost of Common Daily Mistakes**

| Mistake | Extra Token Cost |
| :---- | :---- |
| Starting without context load | 3–5 correction exchanges \= \~2,000–5,000 tokens |
| Not reviewing the plan before approving | Wrong direction \= full re-run \= \~5,000–15,000 tokens |
| Sending a vague correction (“make it better”) | Vague fix → your explanation → re-generation \= \~1,000–3,000 tokens |
| Letting Claude continue after spotting wrong direction | Compounding on wrong foundation \= \~3,000–10,000 tokens |
| Pasting code blocks inline instead of referencing files | 50–500 tokens per paste avoided |

---

### **HOW-TO — Efficient vs. Inefficient Prompt Pairs**

| Inefficient | Efficient |
| :---- | :---- |
| “Fix this, it’s not working” | “Test auth.test.ts:47 fails with \[error\]. Read auth.ts and fix only that failing assertion.” |
| “Make the code better” | “Refactor getUserById in user.service.ts:82 to remove the N+1 query. Follow the pattern at order.service.ts:45.” |
| “Write the API” | /implement-story story-042 |
| “Here is the code: \[500 lines pasted inline\]…” | “Read src/services/user.service.ts and look at the getUserById function.” |
| “I don’t think that’s right” (no specifics) | “The pattern here is wrong. We use async/await not callbacks. See order.service.ts for reference.” |
| “Continue” (after wrong output) | “Stop. Revert \[file\]. The correct approach is \[specific\]. Revise and show me the new plan.” |

---

### **HOW-TO — The Session Reset Protocol**

When a Claude session has accumulated multiple corrections and the context is confused:

**Do not** keep adding more corrections to a broken session. Each correction adds noise to an already noisy context.

**Do this instead:**

1. Send: "Let's reset. Summarise the current state of the codebase changes made in this session."

2. Evaluate: Is the current code better or worse than where you started?

3. If worse: "Revert all changes made in this session. We will start fresh."

4. Open a new Claude Code session

5. Run the context load prompt again — add to Agent Execution Notes the specific thing that caused confusion in the previous session

6. Log the failure type in your feedback file

*A session reset is not a failure. It is the correct decision. The failure was in the original context setup.*

---

### **EXERCISE — D3**

***Your task:** On your next story, count every message you send to Claude. After the story is complete, review each message. Mark it as (E) Efficient or (I) Inefficient. For each (I), write the efficient version. Set a target: complete the next story in ≤12 total messages.*

---

### **CHECK ✓ — D3 Knowledge Check**

**Q30.** You are on your fifth correction loop with Claude on a single story. The session is 30 messages long and growing more confused. What is the correct action?

**Q31.** Which is the most token-efficient prompt for fixing a failing test?

* 

  1) “The tests are failing, please fix them”

* 

  2) “Something is wrong with the auth tests”

* 

  3) “Test auth.test.ts:47 fails with ‘Cannot read property id of undefined’. Read auth.service.ts and fix only that assertion.”

* 

  4) “Here is the full test file: \[paste 200 lines\]. Fix the failures.”

**Q32.** True or False: “Plan approved. Proceed.” is a good response when approving Claude’s implementation plan.

---

# **Final Assessment**

***Instructions:** Complete the full assessment for your role. Score yourself using the Answer Key. Passing score is **80%** (26 or more correct out of 32). If below 80%, revisit the relevant module and re-attempt.*

---

## **Part 1 — Scenario Questions**

**Scenario 1**

Your team starts a sprint. The Architect has not updated CLAUDE.md since the previous sprint. This sprint introduces a new payment processing integration that must use a specific SDK wrapper. Three stories are assigned and Claude Code sessions start.

**Q-S1.** What is the most likely outcome? Describe what the agent will do and why.

**Q-S2.** What should the Architect have done before sprint planning, and specifically what would they have added to CLAUDE.md?

---

**Scenario 2**

A Tech Lead gives a developer this prompt: *“Implement the user authentication feature.”*

**Q-S3.** Name three specific things this prompt is missing that will cause incorrect or incomplete output.

**Q-S4.** Rewrite the prompt using the five-component structure from Module D2.

---

**Scenario 3**

Two developers work in parallel. Developer A builds the backend API. Developer B builds the frontend. On Day 3, Developer B notices the API response is missing a field they need. Developer A agrees and updates the response. Both update their code independently.

**Q-S5.** What protocol was violated? What should have happened instead?

---

**Scenario 4**

A developer is on their fourth correction loop. Claude keeps misunderstanding a validation rule. The session is now 30 messages long.

**Q-S6.** What should the developer do now? Write the first message they should send to Claude.

**Q-S7.** After resolving the story, what should they do to prevent this happening on the next story?

---

## **Part 2 — Answer Key**

### **Module A Answers**

**Q1.** The agent treats the ADR as background reading, not instruction. It will still evaluate or re-debate the decision at runtime because there is no explicit rule telling it what to do.

**Q2.** **(b)** To eliminate ambiguities the AI would otherwise have to guess at.

**Q3.** **False.** Copilot cannot infer constraints not explicitly written down anywhere.

**Q4.** To warn the agent of likely error points, specify the correct pattern to follow, and set the order of file creation — so the most common mistakes are avoided before execution begins.

**Q5.** Not sufficient. Missing: the exact field to validate, the format expected (e.g., email format check), the error response format and status code on failure, and the uniqueness constraint behaviour on conflict.

**Q6.** **(b)** The “Must NOT change” section. Without it, the agent will freely modify any file it considers relevant.

**Q7.** Correct the file path in the story file before triggering the agent. Never proceed with an invalid path — the agent will read the wrong file and build on it.

**Q8.** **(b)** Ask the Tech Lead for the API contract and implement against a mock.

**Q9.** Add that validation convention to the story’s Agent Execution Notes, then trigger the agent.

### **Module B Answers**

**Q10.** Layer 1 — the agent’s core Identity (the “Always Do / Never Do” behaviours in CLAUDE.md Section 5).

**Q11.** The **“Never Do”** sub-section.

**Q12.** Every future Claude session reads anti-patterns.md and will not repeat that mistake — even in a brand new session with no conversation history from Sprint 3\.

**Q13.** It should be converted into a slash command in .claude/commands/ and added to the prompt library as a validated entry.

**Q14.** NOT VERIFIABLE means the AC cannot be confirmed from the code alone — it may require manual testing or an external dependency. This is important because it flags ACs that the developer must test manually rather than assuming the automated check covers them.

**Q15.** **False.** The review agent must be a new, context-isolated session. A session that made the implementation decisions cannot objectively evaluate the outcome against the story requirements.

**Q16.** Stop the agent. Ask it to show the exact failing test, the exact error, and its current diagnosis. Diagnose yourself. Escalate to Tech Lead if you cannot resolve it within 10 minutes.

**Q17.** **(b)** Stop Claude immediately, check with Tech Lead, then redirect.

**Q18.** Resolve both ambiguities before approving execution. If either one affects implementation, resolve it first. Add the resolution to the story file.

### **Module C Answers**

**Q19.** They must stop and bring the change to the Tech Lead immediately. Under Protocol 2 (API Contract Freeze), the contract cannot be changed unilaterally during parallel execution. Tech Lead decides whether to change the contract; if approved, both developers re-sync.

**Q20.** A session that made the implementation decisions cannot impartially review those decisions. A fresh session evaluates only what the story requires — not what was convenient to implement.

**Q21.** The backend developer must stop. Under Protocol 2, the contract is frozen. They must raise it with the Tech Lead, who decides. If the contract changes, both developers must re-sync before continuing.

**Q22.** Tech Lead applies judgment to the recommendations and decides which to implement. Any changes to CLAUDE.md must then be reviewed and approved by the Architect before being committed to the repository.

**Q23.** Stop Claude immediately. Ask it to explain why it created that file and what it contains. If it’s outside the approved plan, revert it and continue within scope.

**Q24.** **False.** Minor style differences (spacing, variable naming conventions) are not worth a correction loop. Let Claude continue — style is handled by linting tools, not agent interruption.

### **Module D Answers**

**Q25.** Move it to an ADR file. The history and reasoning belong in an ADR — CLAUDE.md should contain only what the agent needs to act on, not the story behind the decision.

**Q26.** Example rewrite: *“Validate all API inputs using express-validator. All endpoint handlers must call validationResult() before processing. Return 400 with { code, field, message } on validation failure.”*

**Q27.** Tell Claude to read the file: "Read src/services/user.service.ts." Claude reads files natively. Pasting 400 lines costs \~400 extra tokens and makes the prompt harder to parse.

**Q28.** **(c) Role priming.** It anchors the agent’s operating mode at the start of every interaction without repeating all rules.

**Q29.** Check: (1) Are stories truly AI-ready before execution starts? (2) Are developers using slash commands or typing ad-hoc prompts? (3) Does CLAUDE.md cover the most common causes of corrections logged in feedback files?

**Q30.** Perform a session reset. Ask Claude to summarise the current state. If the code is worse than the starting point, revert all changes, open a new session, and restart with a tighter context load that addresses the specific confusion.

**Q31.** **(c)** — Specific file, specific line, specific error message, specific scope of fix.

**Q32.** **True.** “Plan approved. Proceed.” is efficient (\~5 tokens) and clear. You do not need to repeat back the entire plan.

---

## **Completion Checklist**

| Item | Status |
| :---- | :---- |
| All four modules read for your role | ☐ |
| All exercises completed and documented | ☐ |
| All knowledge checks answered and scored | ☐ |
| Final assessment scenarios answered | ☐ |
| Score: \_\_\_ / 32 correct |  |
| Score ≥ 80% → Ready for independent operation | ☐ |
| Score \< 80% → Revisit flagged modules, re-attempt | ☐ |

Share your completed checklist with your Tech Lead or direct manager.

---

# **Glossary**

| Term | Definition |
| :---- | :---- |
| **AC (Acceptance Criterion)** | A specific, testable condition that must be true for a story to be complete. Must be machine-verifiable in AI-driven development. |
| **ADR (Architecture Decision Record)** | A document recording an architectural decision, reasoning, and explicit constraints for AI agents to follow. |
| **Agent** | An AI system (Claude Code) that executes multi-step tasks by reading files, writing code, running commands, and using tools autonomously. |
| **Agent Execution Notes** | A section in the story file giving the AI hints about patterns to follow, likely errors, and file creation order. |
| **Agent Maturation** | The sprint-over-sprint improvement of agent quality through updating CLAUDE.md, refining prompts, and enriching memory files. |
| **Anti-pattern** | A recurring mistake made by the AI agent, documented in .claude/memory/anti-patterns.md to prevent repetition in future sessions. |
| **Approved Libraries** | The explicit list of packages the agent is permitted to use, maintained in CLAUDE.md. Anything not on this list requires Tech Lead approval. |
| **CLAUDE.md** | The primary configuration file for Claude Code agents. Contains project overview, architecture rules, code style, testing standards, and AI behavior instructions. |
| **Context Load** | The first prompt in any Claude Code session, instructing the agent to read all relevant files before starting any task. |
| **Copilot** | GitHub Copilot — an AI assistant for inline completion, test generation, boilerplate, and documentation. |
| **Correction Loop** | A back-and-forth exchange where the developer redirects the agent after incorrect output. Each loop costs tokens and time. |
| **Definition of Done** | The complete list of criteria that must all be true before a story is considered complete (see SOP Section 16). |
| **Feedback Log** | A per-story document recording what the AI got right, what needed correction, and what context was missing. Used for sprint retrospectives. |
| **Gate Instruction** | The part of a prompt that tells the agent to stop and wait for human approval before proceeding to the next phase. |
| **Generic Agent** | An agent with no task-specific context — only core identity and project persona. Specialised by injecting story context per execution. |
| **Memory Files** | Markdown files in .claude/memory/ that persist learned patterns, anti-patterns, domain terms, and API contracts across sessions. |
| **Orchestration** | The coordination of multiple AI agents or Claude sessions working in sequence or parallel on related tasks. |
| **Parallel Agents** | Two or more Claude Code sessions running simultaneously on independent tasks, sharing a frozen API contract. |
| **Plan Gate** | The human review step between Claude generating an implementation plan and beginning to write code. |
| **Prompt Library** | A maintained collection of validated, reusable prompts organised by category, stored in docs/prompt-library.md. |
| **Quality Gates** | The six automated and manual checks (G1–G6) all AI-generated code must pass before a PR can be merged. |
| **Role Priming** | The first component of an efficient prompt, setting the agent’s operating mode (e.g., “Act as a backend engineer”). |
| **Scope Drift** | When the agent modifies files or creates artifacts outside the boundaries defined in the story. Requires immediate intervention. |
| **Slash Command** | A reusable, pre-loaded prompt triggered by /command-name in Claude Code. Stored in .claude/commands/. |
| **Sprint Context** | The docs/sprint-context.md file updated before each sprint with sprint goals, decisions, and lessons from the previous sprint. |
| **Token** | The unit of text processed by AI models. Roughly: 1 token ≈ 0.75 words. Both prompts and responses consume tokens. |
| **Token Budget** | The target size for a context file (e.g., CLAUDE.md target: 1,000–1,500 tokens) to keep agent context efficient. |
| **Token Efficiency** | The ratio of useful output to total tokens spent. Measured as stories completed in one pass and correction loops per story. |

---

# **Quick Reference Cards**

## **QRC-1 — Architect Daily Reference**

| Category | Checklist |
| :---- | :---- |
| **Planning** | CLAUDE.md reviewed and updated for sprint scope |
|  | New ADRs drafted with “Constraints for AI” section |
|  | copilot-instructions.md updated for any new stack components |
|  | NFRs explicit in story template for this epic |
| **Agents** | CLAUDE.md Section 5: Always / Never / Uncertain — all filled |
|  | Memory files seeded or updated |
|  | Approved and denied library lists are current |
| **Orchestration** | Orchestration flow designed for this sprint |
|  | Human gates identified at each phase boundary |
|  | Parallel tracks have defined and frozen contract |
| **Token Governance** | CLAUDE.md ≤ 1,500 tokens |
|  | Memory files pruned this month |
|  | ADRs contain decision \+ AI constraints only (no history) |

---

## **QRC-2 — Technical Lead Daily Reference**

| Category | Action |
| :---- | :---- |
| **Story Prep** | Run 3-Prompt Story Refinement for every story |
|  | → Prompt 1: Technical context extraction |
|  | → Prompt 2: AC sharpening for machine execution |
|  | → Prompt 3: Agent execution notes |
| **Prompt Library** | Five required categories: Feature, Bug, Refactor, Review, Sprint Ops |
|  | Rule: used 3+ times → convert to slash command |
| **Protocols** | 1\. Shared Context Rule — one committed CLAUDE.md for all sessions |
|  | 2\. API Contract Freeze — freeze before parallel tracks start |
|  | 3\. Integration Gate — G1–G4 per track before convergence |
|  | 4\. Feedback Consolidation — all logs → /sprint-retro |
| **Token Tracking** | % stories completed in 1 pass (target \> 70%) |
|  | Avg correction loops (target \< 2\) |
|  | % using slash commands (target \> 90%) |

---

## **QRC-3 — Developer Daily Reference**

| Category | Action |
| :---- | :---- |
| **Before Start** | All story file paths verified as valid |
|  | All ACs understood well enough to test manually |
|  | sprint-context.md read today |
| **Execution Phases** | 1\. Context Load → confirm understanding |
|  | 2\. Plan Review → approve or ONE targeted redirect |
|  | 3\. Execution → monitor scope, libraries, patterns |
|  | 4\. /review-output \[ID\] → verify each AC |
|  | 5\. PR → Claude generates description |
|  | 6\. Feedback log → submit every story, no exceptions |
| **Escalate When** | 3+ failed self-corrections → Tech Lead |
|  | Scope drift detected → Stop, redirect |
|  | Unapproved library → Stop, check Tech Lead |
|  | \> 30 min manual coding → Escalate |
| **Token Rules** | Reference files — never paste code inline |
|  | Use slash commands, not typed prompts |
|  | Approve plan: “Plan approved. Proceed.” (5 tokens) |
|  | Corrections: surgical and specific |
|  | Session reset if \> 3 failed corrections |

---

## **QRC-4 — Prompt Anti-Patterns (All Roles)**

| Anti-Pattern | Why It Fails | What to Do Instead |
| :---- | :---- | :---- |
| “Fix this” (no specifics) | AI doesn’t know what file, line, or error | Name the file, line number, error, and what correct looks like |
| “Make it better” | AI doesn’t know what “better” means | Specify what to improve, in which file, using which reference |
| “Here is the code: \[paste\]” | Wastes tokens; Claude reads files natively | “Read \[file path\]” |
| Skipping plan review | Wrong direction \= 5,000+ token re-run | Always gate at plan. A bad plan caught early costs \~200 tokens |
| “Continue” after wrong output | Compounds the wrong foundation | “Stop. Revert \[file\]. Correct approach is \[specific\]. Revise.” |
| No context load at session start | Agent guesses everything | Always run context load first — no exceptions |
| Skipping the feedback log | Agent cannot improve without feedback | Submit after every story. No log \= no sprint improvement. |

---

**Document Control**

| Version | Date | Changes |
| :---- | :---- | :---- |
| 1.0 | 2026-05-27 | Initial release — sourced from Training-QuickLearning-Guide.md v1.0 |

**Next review:** 2026-06-27 (align with SOP and Guide monthly review)

*This training manual is a living document. Update exercises and knowledge checks each sprint to reflect current CLAUDE.md rules, prompt library entries, and observed agent behaviours.*

*Supporting documents: SOP-AI-Driven-Development.md · Training-QuickLearning-Guide.md · docs/prompt-library.md*