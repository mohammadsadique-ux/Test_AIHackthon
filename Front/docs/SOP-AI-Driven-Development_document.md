

**STANDARD OPERATING PROCEDURE**

**AI-Driven Software Development**

Using Claude Code & GitHub Copilot  
for \>70% AI-Executed Delivery

| Document Version | 1.0 |
| :---- | :---- |
| **Effective Date** | 2026-05-18 |
| **Audience** | Architects, Technical Leads, Developers |
| **Classification** | Internal — Engineering Practice |
| **Owner** | Engineering Excellence / AI Adoption Team |

**1\. Executive Summary**

This SOP defines the operating model for engineering teams to deliver software where AI agents (Claude Code and GitHub Copilot) execute 90% or more of development tasks. Human roles shift from writing code to directing, reviewing, and continuously improving AI agent behavior.

### **Core Mandate**

| Metric | Target |
| :---: | :---: |
| AI-executed code (lines, features, tests) | ≥ 70% |
| Human review & steering time per story | ≤ 30% of total effort |
| Defect escape rate post AI delivery | \< 5% |
| Agent maturation velocity | Measurable improvement every sprint |

### 

### **What Changes**

* Architects define intent, constraints, and agent scaffolding — not implementation detail.

* Technical Leads act as AI orchestrators: they prompt, validate, and improve agent instructions.

* Developers become AI operators and quality gatekeepers — not primary code authors.

**2\. Guiding Principles**

**1\. Intent Over Implementation**

Humans specify WHAT and WHY. AI determines HOW.

**2\. Generic Agents, Specific Context**

Agents are reusable across projects. Context (CLAUDE.md, memory, user stories) specializes in their behavior.

**3\. Continuous Feedback Loop**

Every sprint improves agent instructions, memory, and prompt libraries. Agents get smarter with each cycle.

**4\. Trust But Verify**

AI output is presumed correct until a quality gate fails. Humans inspect outcomes, not every line of code.

**5\. Auditability First**

Every AI action is logged. Every override is documented. AI decisions are traceable and explainable.

**3\. Roles & Responsibilities**

## **3.1 RACI Matrix**

| Activity | Architect | Tech Lead | Developer |
| :---: | :---: | :---: | :---: |
| Define system architecture | R/A | C | I |
| Author CLAUDE.md & agent config | A | R | C |
| Write & refine master prompts | C | R/A | C |
| Break epics into AI-ready stories | C | R/A | I |
| Configure agent memory/context | A | R | C |
| Trigger AI agent execution | I | C | R/A |
| Review AI-generated code | I | A | R |
| Run quality gates & approve PRs | I | R/A | R |
| Log agent feedback & corrections | I | A | R |
| Sprint retrospective / agent tuning | C | R/A | C |
| Escalate AI failures | A | R | R |
| Define non-functional requirements | R/A | C | I |

## 

*R \= Responsible   A \= Accountable   C \= Consulted   I \= Informed*

## **3.2 Role Profiles**

### **Architect**

**Primary concern:** System integrity, scalability, security, AI agent architecture

**Key AI interactions:** Defines CLAUDE.md project context, sets non-negotiable constraints, reviews agent-generated architecture artefact's			

**Time allocation:** 10% active coding · 40% architecture intent authoring · 50% review & governance

**Output:** Architecture Decision Records (ADRs), CLAUDE.md, agent scaffolding templates

### **Technical Lead**

**Primary concern:** Sprint execution quality, agent orchestration, prompt effectiveness

**Key AI interactions:** Authors and owns master prompt library, manages agent memory, orchestrates multi-agent workflows, validates AI output before developer review

**Time allocation:** 15% coding · 40% AI orchestration & prompt engineering · 30% code review · 5% retrospective & tuning

**Output:** Prompt library, sprint delivery, agent improvement log

### **Developer**

**Primary concern:** AI execution trigger, first-line review, testing, feedback capture

**Key AI interactions:** Runs Claude Code agents against user stories, uses Copilot for gap-filling, captures and escalates agent failures, writes correction prompts

**Time allocation:** 10% coding (corrections only) · 40% AI execution & monitoring · 35% review & testing · 15% feedback logging

**Output:** Reviewed PRs, test results, agent feedback logs

**4\. System Architecture Overview**

## **4.1 High-Level Architecture Layers**

┌─────────────────────────────────────────────────────────────────────────┐  
│                    INTENT LAYER  (Human)                                 │  
│                                                                          │  
│   \[ ARCHITECT \]          \[ TECHNICAL LEAD \]         \[ DEVELOPER \]        │  
│   • ADRs & CLAUDE.md     • Prompt Library           • Story Execution    │  
│   • NFRs                 • Agent Memory             • Feedback Logs      │  
│   • Architecture rules   • Sprint Goals             • Correction Prompts │  
└───────────────────────────────┬─────────────────────────────────────────┘  
                                │  
                                ▼  
┌─────────────────────────────────────────────────────────────────────────┐  
│                    ORCHESTRATION LAYER                                   │  
│                                                                          │  
│   ┌────────────────────────────────────────────────────────────────┐    │  
│   │                  AGENT CONTEXT STORE                            │    │  
│   │  CLAUDE.md ──► Project Rules    Memory Files ──► User Prefs    │    │  
│   │  Prompt Library ──► Reusable    ADR Store ──► Constraints       │    │  
│   │  Story Context ──► Sprint       Past PRs ──► Pattern Learning   │    │  
│   └────────────────────────────────────────────────────────────────┘    │  
│                                                                          │  
│   ┌──────────────────────────┐   ┌──────────────────────────────────┐   │  
│   │   CLAUDE CODE AGENT      │   │     GITHUB COPILOT AGENT         │   │  
│   │ • Multi-file reasoning   │   │ • IDE inline completion          │   │  
│   │ • Agentic task loops     │   │ • Test generation                │   │  
│   │ • Code \+ architecture    │   │ • Docstring authoring            │   │  
│   │ • Sub-agent spawning     │   │ • Quick boilerplate              │   │  
│   │ • Memory & context       │   │ • PR description generation      │   │  
│   └────────────┬─────────────┘   └──────────────────┬───────────────┘   │  
└────────────────┼──────────────────────────────────────┼──────────────────┘  
                 │                                        │  
                 ▼                                        ▼  
┌─────────────────────────────────────────────────────────────────────────┐  
│                    EXECUTION LAYER                                       │  
│                                                                          │  
│  \[ CODE REPO \]    \[ TEST SUITE \]    \[ CI/CD PIPELINE \]   \[ ARTIFACTS \]  │  
└──────────────────────────────────────┬──────────────────────────────────┘  
                                       │  
                                       ▼  
┌─────────────────────────────────────────────────────────────────────────┐  
│                    FEEDBACK LAYER                                        │  
│  Quality Gate Results ──► Agent Memory Update ──► Prompt Refinement     │  
│  PR Review Comments ──► Correction Prompts ──► Sprint Retrospective      │  
│  Failure Logs ──► Escalation ──► Architect Review ──► CLAUDE.md Update  │  
└─────────────────────────────────────────────────────────────────────────┘

## **4.2 Agent Context Hierarchy**

LEVEL 1 — GLOBAL CONTEXT  (Persistent across all projects)  
  \~/.claude/CLAUDE.md          — Global behaviour rules

  \~/.claude/agents/architct.agent.md         

  \~/.claude/agents/backend.agent.md    

  \~/.claude/prompts/\*          \-Add common prompts for consistency

  \~/.claude/memory/            — Cross-project user preferences  
  \~/.claude/commands/          — Reusable slash commands  
         │  
         ▼  
LEVEL 2 — PROJECT CONTEXT  (Per repository)  
  .claude/CLAUDE.md            — Project rules & tech stack  
  .claude/memory/              — Project-specific memory  
  .claude/commands/            — Project slash commands  
  .claude/settings.json        — Permissions & hooks  
         │  
         ▼  
LEVEL 3 — SPRINT CONTEXT  (Per sprint / iteration)  
  docs/sprint-context.md       — Active sprint goals  
  docs/prompt-library.md       — Approved prompt patterns  
  docs/architecture-decisions/ — ADRs for agent context  
  docs/user-stories/           — Story files for AI execution  
         │  
         ▼  
LEVEL 4 — STORY CONTEXT  (Per user story)  
  story-XXX.md                 — Single story with ACs  
  story-XXX-context.md         — Related code, deps, APIs  
  story-XXX-output/            — AI-generated artifacts

**5\. AI Agent Design — Generic & Adaptive**

## **5.1 Generic Agent Design Principles**

Agents must be tool-agnostic, project-agnostic, and stack-agnostic at their core. They specialise only through injected context at three levels:

┌──────────────────────────────────────────────────────────────────┐  
│  CORE AGENT IDENTITY  (Never changes)                            │  
│  • Role: "Senior software engineer with expertise in..."         │  
│  • Ethics: Security-first, clean code, no over-engineering       │  
│  • Output: Structured, testable, documented                      │  
└────────────────────────────────┬─────────────────────────────────┘  
                                 │  INJECT AT RUNTIME  
                                 ▼  
┌──────────────────────────────────────────────────────────────────┐  
│  SPECIALISATION CONTEXT  (Changes per project / sprint / story)  │  
│  • Tech stack: "React 18, Node.js 20, PostgreSQL"                │  
│  • Conventions: "Follow patterns in CLAUDE.md"                   │  
│  • Constraints: "Do not modify files in /legacy"                 │  
│  • Domain: "Fintech app. PCI-DSS compliance required."           │  
└────────────────────────────────┬─────────────────────────────────┘  
                                 │  INJECT PER EXECUTION  
                                 ▼  
┌──────────────────────────────────────────────────────────────────┐  
│  TASK CONTEXT  (Changes per user story)                          │  
│  • User story \+ acceptance criteria                              │  
│  • Relevant existing code (file paths, function names)           │  
│  • API contracts, DB schema snippets                             │  
│  • Related past stories (for pattern consistency)                │  
└──────────────────────────────────────────────────────────────────┘

## **5.2 Adaptive Learning Loop (Per Sprint)**

 ┌─────────────────────────────────────────────────────┐  
 │           AGENT MATURATION CYCLE (Every Sprint)      │  
 └─────────────────────────┬───────────────────────────┘  
                           │  
       ┌───────────────────▼───────────────┐  
       │           SPRINT N                 │  
       │    Agent executes stories          │  
       └───────────────────┬───────────────┘  
                           │  
       ┌───────────────────▼───────────────┐  
       │      QUALITY GATE REVIEW           │  
       │  • What did AI get right?          │  
       │  • Where did AI deviate?           │  
       │  • What corrections were needed?   │  
       └───────────────────┬───────────────┘  
                           │  
       ┌───────────────────▼───────────────┐  
       │     RETROSPECTIVE CAPTURE          │  
       │  • Log correction patterns         │  
       │  • Identify prompt gaps            │  
       │  • Note context improvements       │  
       └───────────────────┬───────────────┘  
                           │  
       ┌───────────────────▼───────────────┐  
       │      AGENT IMPROVEMENT             │  
       │  • Update CLAUDE.md rules          │  
       │  • Refine prompt templates         │  
       │  • Enrich memory files             │  
       │  • Add new slash commands          │  
       └───────────────────┬───────────────┘  
                           │  
       ┌───────────────────▼───────────────┐  
       │          SPRINT N+1                │  
       │  Agent executes with improved      │  
       │  instructions & context            │  
       └───────────────────────────────────┘

## **5.3 Agent Capability Matrix**

| Task Type | Primary Agent | Secondary Agent |
| :---: | :---: | :---: |
| Architecture design | Claude Code | Human (Architect) |
| Feature implementation | Claude Code | Copilot (gap fill) |
| Unit test generation | Claude Code | Copilot |
| Integration test authoring | Claude Code | Human validation |
| API contract authoring | Claude Code | Human review |
| Database schema design | Claude Code | Architect approval |
| Code refactoring | Claude Code | Copilot suggestions |
| Inline code completion | Copilot | Claude Code |
| PR descriptions | Copilot / Claude | Tech Lead review |
| Documentation | Claude Code | Copilot |
| Security scanning guidance | Claude Code | Human (security gate) |
| Bug diagnosis & fix | Claude Code | Developer confirmation |
| Code review comments | Claude Code | Tech Lead final |
| Sprint planning breakdown | Claude Code | Tech Lead approval |

## 

**6\. End-to-End Development Workflow**

## **6.1 Master Process Flow**

SPRINT PLANNING  
───────────────  
\[Product Owner\] ──► Epic / Feature Brief  
      │  
      ▼  
\[Tech Lead \+ Claude\] ──► Story Decomposition ──► AI-Ready User Stories  
      │  
      ▼  
\[Architect\] ──► Validate Architecture Impact ──► Update CLAUDE.md if needed  
      │  
      ▼  
\[Tech Lead\] ──► Assign stories to Developers (AI Operators)

────────────────────────────────────────────────────────────────────────

STORY EXECUTION  (Developer as AI Operator)

  STEP 1: CONTEXT PREPARATION  
  Developer loads story file \+ injects relevant codebase context.  
  Claude reads CLAUDE.md, memory, story, and related files.  
         │  
         ▼  
  STEP 2: PLAN GENERATION  
  Claude generates implementation plan (files to create/modify, approach).  
  Developer reviews plan ──► Approve / Redirect / Clarify.  
         │  
         ▼  
  STEP 3: AI CODE GENERATION  
  Claude executes: writes code, creates files, runs tests.  
  Copilot fills inline gaps while developer monitors execution.  
         │  
         ▼  
  STEP 4: AUTO-VALIDATION  
  Claude runs: unit tests, linting, type checking, build verification.  
  Failures ──► Claude self-corrects up to 3 iterations.  
         │  
     Pass │  Fail (\>3 iterations) ──► Escalate to Tech Lead  
         │  
         ▼  
  STEP 5: HUMAN QUALITY GATE  
  Developer reviews AI output against acceptance criteria.  
  Tech Lead reviews for architecture alignment.  
         │  
         ▼  
  STEP 6: PR CREATION & CI  
  Claude generates PR description, summary, and test plan.  
  CI pipeline: security scan, integration tests, coverage check.  
         │  
         ▼  
  STEP 7: FEEDBACK CAPTURE  
  Developer logs what AI got right, corrections needed, prompt gaps.  
  Feeds the next sprint's agent improvement cycle.

## **6.2 Decision Flow — When to Override AI**

          ┌─────────────────────────────┐  
          │   AI generates output        │  
          └─────────────┬───────────────┘  
                        │  
          ┌─────────────▼───────────────┐  
          │  Does output pass            │  
          │  acceptance criteria?        │  
          └─────────────┬───────────────┘  
                 Yes    │    No  
       ┌────────────────┘    └─────────────────────┐  
       │                                            │  
       ▼                                            ▼  
┌──────────────────┐                  ┌─────────────────────────────┐  
│ Aligns with      │                  │ Failure due to:             │  
│ architecture?    │                  │  a) Missing context?        │  
└──────────┬───────┘                  │  b) Wrong prompt?           │  
     Yes   │  No                      │  c) Agent limitation?       │  
      │    │                          └──────────────┬──────────────┘  
      │    ▼                               (a/b)     │    (c)  
      │  ┌─────────────────────┐             │       │  
      │  │ Flag to Tech Lead   │             ▼       ▼  
      │  │ Redirect with       │       ┌─────────┐ ┌─────────────────┐  
      │  │ correction prompt   │       │ Refine  │ │ Developer manual│  
      │  └─────────────────────┘       │ prompt  │ │ fix \+ log gap   │  
      │                                │ & re-run│ └─────────────────┘  
      ▼                                └─────────┘  
┌─────────────────┐  
│  APPROVE & MERGE│  
└─────────────────┘

**7\. User Story Lifecycle (AI-Driven)**

## **7.1 AI-Ready Story Template**

Every user story must be machine-readable. Tech Leads are responsible for ensuring this format before developer assignment. The template below is mandatory:

\# Story: \[ID\] — \[Title\]

\#\# Intent  
\[1-2 sentences: What business outcome does this deliver?\]

\#\# User Story  
As a \[role\], I want to \[action\] so that \[outcome\].

\#\# Acceptance Criteria  
\- \[ \] AC1: \[Specific, testable criterion\]  
\- \[ \] AC2: \[Specific, testable criterion\]  
\- \[ \] AC3: \[Specific, testable criterion\]

\#\# Technical Context  
\- Relevant files:  \[list file paths\]  
\- APIs involved:   \[list endpoints or contracts\]  
\- DB tables:       \[list tables affected\]  
\- Dependencies:    \[list story IDs this depends on\]  
\- Must NOT change: \[list files/modules off-limits\]

\#\# Non-Functional Requirements  
\- Performance: \[e.g., API response \< 200ms\]  
\- Security:    \[e.g., validate and sanitise all inputs\]  
\- Coverage:    \[e.g., ≥ 85% unit test coverage\]

\#\# Agent Execution Notes  
\[Hints for AI: known patterns, past similar stories, specific library to use\]

## **7.2 Story Lifecycle Flow**

┌──────────┐   ┌─────────────┐   ┌──────────────┐   ┌────────────┐  
│  BACKLOG │──►│ AI-READY    │──►│ IN PROGRESS  │──►│  REVIEW    │  
│          │   │ REFINEMENT  │   │ (AI Agent)   │   │  (Human)   │  
│ Raw PO   │   │             │   │              │   │            │  
│ stories  │   │ Tech Lead   │   │ Developer    │   │ Tech Lead  │  
│          │   │ formats for │   │ triggers     │   │ validates  │  
│          │   │ AI execution│   │ Claude agent │   │ output     │  
└──────────┘   └─────────────┘   └──────────────┘   └─────┬──────┘  
                                                           │  
                                        ┌──────────────────┤  
                                   Pass │           Fail   │  
                                        │                  │  
                                        ▼                  ▼  
                                  ┌──────────┐    ┌──────────────────┐  
                                  │   DONE   │    │    REWORK        │  
                                  │ Merged \+ │    │ Agent re-runs    │  
                                  │ feedback │    │ with corrected   │  
                                  │ logged   │    │ prompt           │  
                                  └──────────┘    └──────────────────┘

**8\. Role-Specific SOPs**

## **8.1 Architect SOP**

### **Pre-Sprint: Author / Update CLAUDE.md**

The CLAUDE.md file is the single most important artifact for AI agent behaviour. The Architect owns its content. It must include:

**Section 1 — Project Overview:** What the system does, primary tech stack with versions, deployment environment

**Section 2 — Architecture Rules (NON-NEGOTIABLE):** Folder structure conventions, module boundaries, forbidden patterns, security constraints

**Section 3 — Code Style & Conventions:** Naming conventions, error handling patterns, logging standards, comment policy

**Section 4 — Testing Standards:** Required test types per feature, coverage thresholds, testing libraries to use

**Section 5 — AI Behaviour Instructions:** What Claude should always do, what Claude must never do, how to handle ambiguity

### **Pre-Sprint: Epic Architecture Review Checklist**

☐  Does this epic introduce new external dependencies? If YES → Add to CLAUDE.md approved libraries

☐  Does this epic touch security boundaries? If YES → Add explicit security notes to CLAUDE.md

☐  Does this epic require new infrastructure? If YES → Create ADR and add architectural context

☐  Does this epic change data models? If YES → Update schema docs and story technical context

☐  Are there NFRs that AI must know about? If YES → Add NFR notes to CLAUDE.md or story template

### **Pre-Sprint: Architecture Decision Records (ADRs)**

ADRs are automatically included in Claude's context. Required format:

\# ADR-\[NNN\]: \[Decision Title\]  
Date: YYYY-MM-DD   Status: Accepted

\#\# Decision  
\[One paragraph: what was decided\]

\#\# Reasoning  
\[Why this decision was made\]

\#\# Constraints for AI  
\[Explicit rules: "Always use X", "Never bypass Y"\]

### **During Sprint**

* Review AI-generated architecture-level code (infrastructure, schemas, core modules)

* Flag architectural drift in PR reviews (block on structure, not style)

* Update CLAUDE.md immediately when new patterns are approved

### **Post-Sprint**

* Conduct Architecture Health Check: does the codebase still match intended design?

* Update ADRs based on AI-driven patterns that emerged

* Add new constraints discovered to CLAUDE.md for the next sprint

## **8.2 Technical Lead SOP**

### **Pre-Sprint: Story Refinement for AI Execution**

**Step 1:** Read raw story from backlog

**Step 2:** Ask Claude: "Given our CLAUDE.md and this raw story, generate an AI-ready story file with technical context, file paths, and agent execution notes"

**Step 3:** Review Claude's generated story — verify testable ACs, technical context, off-limits files, NFR section

**Step 4:** Save as docs/user-stories/story-\[ID\].md

**Step 5:** Assign story file to Developer

### **Pre-Sprint: Sprint Context File (sprint-context.md)**

\# Sprint \[N\] Context — \[Sprint Name\]

\#\# Sprint Goal  
\[One sentence\]

\#\# Key Decisions for This Sprint  
\- \[Decision 1 and why it matters for AI execution\]

\#\# Patterns Established Last Sprint (AI Must Follow)  
\- \[Pattern 1 with example\]

\#\# Things AI Got Wrong Last Sprint (Watch For)  
\- \[Issue 1 and correct behaviour\]

\#\# New Libraries / APIs Introduced This Sprint  
\- \[Library\]: \[How to use it\]

### **During Sprint: Daily AI Output Review**

☐  Is the AI implementation plan logical and aligned with architecture?

☐  Does generated code follow CLAUDE.md patterns?

☐  Are tests meaningful — not just coverage-filling?

☐  Did AI produce any anti-patterns or security issues?

☐  Are there any deviations that need prompt correction?

### **Handling AI Failures**

When AI output fails a quality gate:

1\. Identify failure category:  
   a) Missing context   → Enrich story file, re-trigger agent  
   b) Wrong approach    → Write correction prompt, re-trigger  
   c) Architecture viol → Update CLAUDE.md, re-trigger  
   d) Agent limitation  → Developer completes manually \+ logs gap

2\. Never allow a Developer to spend \> 30 min on a single AI failure  
   before escalating to the Tech Lead.

3\. Log all failures in sprint-retrospective.md

### **Post-Sprint: Retrospective with Claude**

Prompt template for end-of-sprint retrospective:

"Review the following sprint feedback log: \[PASTE LOG\]  
 Identify:  
 1\. Top 3 prompt improvements needed  
 2\. Top 2 CLAUDE.md rules to add or update  
 3\. Any new slash commands that would save time  
 4\. Patterns the AI consistently got right (to reinforce)  
 Generate specific, actionable updates for each." 

## **8.3 Developer SOP**

### **Morning Setup (15 minutes)**

☐  Pull latest main branch

☐  Read sprint-context.md for today's focus

☐  Review assigned story file (story-\[ID\].md)

☐  Verify technical context files exist and are current

☐  Open Claude Code session in correct working directory

### **Story Execution — 6 Phases**

**Phase 1: Context Load (5–10 min)**

Prompt Claude to read CLAUDE.md, sprint-context.md, and the story file. Ask Claude to summarise its understanding and list any questions before proceeding. Do NOT proceed if Claude misunderstood the story.

**Phase 2: Plan Review (5–10 min)**

Ask Claude to generate a detailed implementation plan (files to create/modify, function signatures, test strategy, order of operations) WITHOUT writing any code. Approve or redirect the plan before execution.

**Phase 3: Execution (30–60 min)**

Approve execution. Monitor for: files modified outside agreed scope, unapproved library usage, CLAUDE.md violations. Pause and redirect immediately if deviation is spotted.

**Phase 4: Validation (20–30 min)**

Run full test suite manually. Verify each AC by reading code and tests. Check for hardcoded values, exposed secrets, console.logs. Escalate major issues to Tech Lead.

**Phase 5: PR Creation (10 min)**

Ask Claude to generate a PR title, description, and test plan. Verify accuracy, then submit and tag Tech Lead.

**Phase 6: Feedback Log (10 min)**

Log: AI completion %, corrections needed and why, prompt patterns that worked, context gaps. Save to docs/agent-feedback/sprint-\[N\]/story-\[ID\]-feedback.md

### **Copilot Usage Guidelines**

| USE Copilot FOR | DO NOT USE Copilot FOR |
| :---- | :---- |
| ✓  Inline boilerplate within a function already scaffolded by Claude | ✗  Architectural decisions or module design |
| ✓  Quick test case variations (5 similar tests) | ✗  Complex business logic (use Claude with full context) |
| ✓  Utility function bodies when signature is clear | ✗  Security-sensitive code |
| ✓  Documentation and docstrings | ✗  Cross-cutting concerns (auth, logging, DB models) |
| ✓  Regex patterns, SQL queries, config snippets | ✗  Anything requiring multi-file reasoning |

### 

**9\. Tool Configuration & Setup**

## **9.1 Claude Code Setup**

INITIAL SETUP (One-time per developer):

1\. Install Claude Code CLI:  
   npm install \-g @anthropic-ai/claude-code

2\. Configure global settings:  
   \~/.claude/CLAUDE.md        ← global developer preferences

   \~/.claude/agents/architect.agent.md 

        
   \~/.claude/settings.json    ← permissions & allowed tools

3\. Verify project CLAUDE.md is in the repo root

4\. Install project slash commands in .claude/commands/:  
   implement-story.md  
   review-output.md  
   sprint-retro.md

### **Recommended settings.json**

{  
  "permissions": {  
    "allow": \[  
      "Bash(npm run test\*)",  
      "Bash(npm run lint\*)",  
      "Bash(npm run build\*)",  
      "Bash(git status)",  
      "Bash(git diff\*)",  
      "Read(\*\*)"  
    \],  
    "deny": \[  
      "Bash(git push\*)",  
      "Bash(rm \-rf\*)",  
      "Bash(git reset \--hard\*)"  
    \]  
  },  
  "hooks": {  
    "PostToolUse": \[{  
      "matcher": "Edit|Write",  
      "hooks": \[{ "type": "command",  
                  "command": "npm run lint \--fix 2\>/dev/null || true" }\]  
    }\]  
  }  
}

### **Recommended Slash Commands**

**/implement-story \[ID\]:** Read CLAUDE.md, sprint-context.md, and the story file. Summarise understanding. Generate implementation plan. Wait for approval. Then implement tests.

**/review-output \[ID\]:** Review the current git diff against the acceptance criteria in the story file. Report which ACs are met, which are not, and any architectural or quality issues.

**/sprint-retro \[N\]:** Read all files in docs/agent-feedback/sprint-N/. Analyse patterns. Produce: top 5 prompt improvements, CLAUDE.md updates, new slash commands, success patterns to reinforce.

## **9.2 GitHub Copilot Setup**

1\. Install GitHub Copilot extension in VS Code / JetBrains  
2\. Enable Copilot Chat panel  
3\. Create .github/copilot-instructions.md:

   \# Copilot Instructions  
   Follow conventions in CLAUDE.md.  
   Always generate tests alongside implementation code.  
   Never use deprecated APIs. Prefer \[approved libraries\].  
   Security: validate all inputs. Never log sensitive data.

4\. Set inline suggestion delay: 500ms (avoid accepting too fast)

**10\. Quality Gates & Acceptance Criteria**

## **10.1 Gate Framework**

| Gate | Criteria | Who Validates |
| :---: | :---: | :---: |
| G1: Auto Tests | All unit tests passTest coverage ≥ threshold | Claude (auto) \+ CI pipeline |
| G2: Lint / Type | Zero lint errorsZero type errors | CI pipeline \+ Claude pre-commit |
| G3: AC Check | All acceptance criteria metManual verification done | Developer \+ Tech Lead (spot check) |
| G4: Security | No OWASP Top 10 violationsNo secrets in code | SAST tool \+ Claude \+ Developer |
| G5: Architecture | No boundary violationsFollows CLAUDE.md patterns | Tech Lead \+ Architect (core changes) |
| G6: Integration | Integration tests passAPI contracts valid | CI pipeline \+ Tech Lead |

## 

### **10.2 Developer Checklist — Before Submitting PR**

☐  G1: npm run test — all pass, coverage met

☐  G2: npm run lint && npm run type-check — zero errors

☐  G3: Manually verified each acceptance criterion

☐  G4: Searched for hardcoded secrets, console.log, TODO, any, eval

☐  G5: Confirmed no files outside story scope were modified

☐  G6: Ran integration tests if story touches APIs

### **10.3 Tech Lead Checklist — Before Merging PR**

☐  AI attribution: implementation is consistent with AI-first approach

☐  Pattern compliance: code follows established patterns

☐  Test quality: tests are meaningful, not just coverage-filling

☐  Security: spot-check for injection points, auth gaps, data exposure

☐  Architecture: no unexpected dependencies or structural changes

☐  Feedback log submitted by Developer

**11\. Continuous Learning & Agent Maturation**

## **11.1 Sprint-Over-Sprint Maturity Scorecard**

| Sprint | AI % Complete | Corrections Needed | CLAUDE.md Updates | Prompt Updates |
| :---: | :---: | :---: | :---: | :---: |
| N-2 | 72% | 28 | 2 | 5 |
| N-1 | 81% | 19 | 1 | 3 |
| N (current) | 89% | 11 | 1 | 2 |
| N+1 (target) | ≥ 90% | \< 10 | — | — |

## 

## **11.2 Knowledge Capture Protocol**

WEEK 1-2: EXECUTION  
  Developers log feedback after every story  
  → docs/agent-feedback/sprint-\[N\]/

END OF SPRINT: SYNTHESIS  
  Tech Lead runs: /sprint-retro \[N\]  
  Claude analyses all feedback files and produces:  
    1\. Updated CLAUDE.md sections (diff format)  
    2\. New / updated prompt templates  
    3\. New slash commands  
    4\. Sprint N+1 context file draft

BEFORE SPRINT N+1 PLANNING:  
  Architect reviews CLAUDE.md changes (approve / reject each)  
  Tech Lead publishes updated prompt library  
  Tech Lead briefs developers on new patterns

## **11.3 Agent Memory File Structure**

.claude/memory/  
├── project-patterns.md     ← Established code patterns (auto-updated)  
├── anti-patterns.md        ← Things AI got wrong (never repeat)  
├── domain-glossary.md      ← Domain terms and their meaning  
├── api-contracts.md        ← Key API shapes and contracts  
├── team-preferences.md     ← Style and approach preferences  
└── sprint-history.md       ← Summary of past sprint learnings

MEMORY UPDATE RULE:  
  Every correction made to AI output → entry in anti-patterns.md  
  Every approved pattern            → entry in project-patterns.md  
  Memory files are reviewed and pruned monthly

**12\. Metrics & Success Criteria**

## **12.1 Key Performance Indicators**

| Metric | Baseline | Target | How Measured |
| :---: | :---: | :---: | :---: |
| AI code contribution (%) | \< 40% | ≥ 70% | Per story feedback log |
| Developer coding time (hrs/story) | 8–12 h | 1–2 h | Time logs |
| Stories delivered per sprint | Baseline | \+40% | Jira / ADO |
| Defect escape rate | Baseline | \< 5% | QA logs |
| Agent self-correction rate | N/A | \> 80% | Feedback log |
| Prompt correction frequency | N/A | \< 10/spr | Retro log |
| Test coverage | Baseline | ≥ 80% | CI report |
| Time to onboard new developer | 1–2 weeks | 2–3 days | Onboarding log |

## 

### **12.2 Monthly Health Check Agenda**

* 1\. AI Contribution Trend — is the ≥70% target maintained?

* 2\. Defect Analysis — are AI-generated defects increasing or decreasing?

* 3\. Agent Maturation — is CLAUDE.md and prompt library growing meaningfully?

* 4\. Bottleneck Identification — where is human time still being spent?

* 5\. Tooling — any new Claude or Copilot capabilities to adopt?

* 6\. Team Feedback — developer satisfaction with the AI workflow?

* 7\. Action Items — specific improvements for next month

**13\. Escalation & Override Protocol**

## **13.1 Escalation Matrix**

| Scenario | Contact | Resolution Time |
| :---: | :---: | :---: |
| AI output fails 3+ self-correct attempts | Tech Lead | Same day |
| AI violates architecture pattern in generated code | Tech Lead → Architect | Same day |
| Claude API unavailable | Use Copilot \+ manual(fallback mode) | Immediate |
| Security vulnerability in AI-generated code | Tech Lead → Architect→ Security team | Block PR, same day |
| Agent misunderstands same pattern 3+ stories | Tech Lead updatesCLAUDE.md | Before next sprint |
| Developer spends \> 2 h on single AI failure | Tech Lead takes over story | Immediate |

## 

## **13.2 Manual Override Protocol**

When a Developer must write code manually (AI failure):

1\. Document the failure:  
   \- What was the prompt?  
   \- What did AI produce?  
   \- Why was it wrong?

2\. Write the code manually.

3\. Show correct code to Claude afterwards:  
   "This is the correct implementation I wrote manually.  
    Analyse why you produced a different result.  
    What context was missing? What rule would prevent this?"

4\. Log Claude's analysis in: docs/agent-feedback/overrides.md

5\. Tech Lead reviews override log weekly and updates CLAUDE.md  
   or prompt library based on patterns found.

IMPORTANT: Manual code must still pass all quality gates.  
           Manual overrides are NOT exempt from review standards.

**14\. Appendix**

## **A. Developer Daily Cheat Sheet**

MORNING  
  ☐ git pull && read sprint-context.md  
  ☐ Review assigned story file

STORY EXECUTION  
  1\. /implement-story story-\[ID\]    ← Load context & get plan  
  2\. Review plan → approve or redirect  
  3\. Claude executes → monitor for scope drift  
  4\. /review-output story-\[ID\]      ← Validate ACs  
  5\. Create PR with Claude description  
  6\. Submit feedback log

ESCALATION TRIGGERS  
  \! AI fails 3+ times               → call Tech Lead  
  \! AI modifies out-of-scope files  → stop and redirect  
  \! Security issue found            → block PR, call Tech Lead  
  \! \> 30 min manual coding          → escalate

END OF DAY  
  ☐ Feedback log submitted  
  ☐ PRs reviewed (as reviewer)

## **B. Prompt Anti-Patterns**

| Ineffective (Vague) | Effective (Specific \+ Context-Rich) |
| :---: | :---: |
| "Write a login feature" | "Read story-042.md and CLAUDE.md. Implement JWT-based login per the ACs. Use auth patterns in src/auth/. Tests must cover all ACs." |
| "Fix the bug" | "The test in auth.test.ts line 47 is failing with \[error\]. Read auth.ts and diagnose the root cause. Propose fix before changing anything." |
| "Refactor this code" | "Refactor getUserById in user.service.ts to follow the async/await pattern in order.service.ts. Do not change the function signature." |
| "Make it better" | "The function at user.service.ts:82 has a N+1 query issue. Fix it with a single JOIN query. Do not modify the function signature or tests." |

## 

## **C. Story Readiness Checklist (Tech Lead Pre-Sprint)**

☐  Story has a clear, single-sentence intent statement

☐  User story follows "As a / I want / So that" format

☐  Acceptance criteria are numbered, specific, and testable

☐  All relevant file paths are listed in Technical Context

☐  APIs and DB tables are explicitly named

☐  "Must NOT change" section is populated

☐  NFR section has at least performance and security entries

☐  Agent Execution Notes includes at least one similar past story

☐  Story has been cross-referenced against current CLAUDE.md rules

☐  No ambiguities remain that an AI would need to guess about

## **D. New Developer Onboarding (AI Workflow)**

**Day 1 — Conceptual**

☐  Read this SOP

☐  Read project CLAUDE.md

☐  Read docs/prompt-library.md

☐  Shadow an existing Developer on one story (observe only)

**Day 2 — Tool Setup**

☐  Claude Code installed and configured

☐  Copilot installed and configured

☐  Access to docs/ folder confirmed

☐  Shadow another story (help with monitoring phase)

**Days 3–4 — Supervised Execution**

☐  Execute one low-complexity story with Tech Lead reviewing each phase

☐  Submit first feedback log with Tech Lead review

**Day 5+ — Independent**

☐  Execute stories independently

☐  Escalate per escalation matrix

☐  Contribute to retrospective

## **Document Control**

| Version | Date | Author | Changes |
| :---: | :---: | :---: | :---: |
| 1.0 | 2026-05-18 | AI Adoption Team | Initial release |

## 

