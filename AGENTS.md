# AGENTS.md

<!-- BEGIN:nextjs-agent-rules -->

# This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` (resolved from this file's directory; in monorepos the `next` package may not be visible from the repo root) before writing any code. Heed deprecation notices.

This block is written and re-added by `next dev` — verify at `node_modules/next/dist/server/lib/generate-agent-files.js`. Removing it from a diff only re-creates the uncommitted change; committing it with your work keeps the tree clean.

<!-- END:nextjs-agent-rules -->

---

## 1. Project Overview

- This file contains the rules and working guidelines for AI agents working in this project.
- The project may contain multiple areas, features, technologies, or parts owned and maintained by different people.
- The AI MUST determine the relevant project structure, conventions, technologies, and ownership before making changes.
- The AI's responsibility is to make only the changes allowed by this document and by the user's instructions.
- The AI MUST NOT assume a specific framework, library, architecture, folder structure, API pattern, or development workflow unless it is confirmed by the existing project.

---

## 2. Mandatory Startup Procedure

Before making **any code or project-file change**, the AI MUST follow this order:

1. Read `AGENTS.md` (required only once at the beginning of a conversation/session or when switching to a completely new task context; do not re-read repeatedly before every follow-up step or minor file edit within the same task).
2. Read `AGENT_CHANGELOG.md` (targeted reading: focus primarily on the most recent entries to understand current context, rather than reading the entire historical log unless investigating a specific past change; required once per session/task context).
3. Inspect the relevant project structure and the files directly related to the requested task.
4. Identify the technologies, conventions, and implementation patterns already used in the relevant area.
5. Determine which files are in scope for the requested change.
6. Check whether the requested change conflicts with any rule in this file.
7. If anything is unclear, ambiguous, or insufficiently specified, ask the user before making the change.
8. Only after the above steps, implement the requested change.
9. After completing the change, verify the written code for syntax correctness and obvious implementation mistakes.
10. Update `AGENT_CHANGELOG.md` with the changes made by the current AI.

The AI MUST NOT skip reading `AGENTS.md` and recent entries of `AGENT_CHANGELOG.md` at session start, but it MUST NOT re-read them redundantly on minor follow-up steps.

---

## 3. Ownership and File Modification Rules

### 3.1 Files within the user's scope

The AI may modify files that:

- are explicitly included in the user's requested scope,
- are owned or maintained by the user,
- or are directly required to implement the requested task.

The AI MUST determine this from the project structure, existing documentation, and user instructions rather than making assumptions.

### 3.2 Files owned or maintained by another person

The AI MUST NOT modify files that are known to be owned or maintained by another person unless the user explicitly authorizes the change.

If the AI cannot reliably determine whether a file belongs to the user's scope or another person's scope, it MUST ask the user before modifying it.

### 3.3 Explicit exception

If the user explicitly tells the AI to modify a file outside the normal ownership/scope:

- The AI may modify that file.
- It may make only the change necessary for that explicit request.
- It MUST NOT use the permission as an opportunity to refactor, clean up, reorganize, or modify unrelated parts of that file.
- The exception applies only to the requested change.

---

## 4. Scope Protection

The AI MUST keep every change strictly within the scope of the user's request.

The AI MUST NOT:

- Modify files outside the required scope.
- Modify unrelated code.
- Refactor existing code without a concrete need for the requested task.
- Change the project's architecture unnecessarily.
- Change the project's folder/file structure without explicit permission.
- Modify another area of the project merely because it could be improved.
- Change configuration files without explicit permission unless the requested task necessarily requires it and the change is within scope.
- Change build, deployment, environment, or project configuration merely to make a task easier.
- Rewrite existing code simply because the AI prefers another coding style.
- Make broad cleanup changes while working on an unrelated feature.
- Modify backend, frontend, or other non-target areas when they are outside the requested scope.

If a requested task appears to require a change outside the normal scope, the AI must explain why that change is needed and ask the user before doing it.

---

## 5. Package and Dependency Rules

The AI MUST NOT install, add, remove, upgrade, downgrade, or replace packages/dependencies on its own.

If a package or dependency is genuinely required:

1. Tell the user which package is needed.
2. Explain briefly why it is needed.
3. Wait for the user to decide whether to install it.
4. Do not install it or modify dependency/manifest files unless the user explicitly authorizes it.

The AI should first look for a solution using packages, libraries, utilities, and capabilities already present in the project.

The absence of a preferred package is NOT a reason to introduce a new dependency automatically.

---

## 6. Existing Project Architecture and Conventions

The AI MUST first inspect the existing project before deciding how to implement a feature.

The AI MUST:

- Reuse existing project conventions whenever reasonably possible.
- Follow the patterns already used in the relevant area of the project.
- Reuse existing utilities, components, modules, services, hooks, API helpers, libraries, and abstractions when appropriate.
- Avoid creating a new architecture when an appropriate existing pattern already exists.
- Avoid introducing a new pattern merely because it is personally preferred.

The AI MUST NOT assume:

- a specific frontend framework,
- a specific backend framework,
- a specific routing system,
- a specific state-management solution,
- a specific HTTP/API library,
- a specific database or ORM pattern,
- a specific folder structure,
- a specific styling solution,
- or a specific component/module architecture.

These MUST be determined from the actual project.

### 6.1 Responsive Breakpoint Preferences

The user's primary responsive-design preferences and guidelines for review are as follows:

- **Primary Checkpoints:** The breakpoints primarily monitored and evaluated are `sm`, `md`, and `lg`.
- **Mobile-Oriented Scope:** Both `sm` and `md` are generally treated as mobile-oriented screen sizes when designing and reviewing responsive layouts.
- **Desktop Transition:** Layouts must not automatically switch to a desktop-oriented layout at `md`. The primary checkpoint for transitioning to a desktop layout should generally be `lg`, unless an established project requirement or component structure specifically dictates otherwise.
- **Convention-Aware Styling:** Use the actual breakpoint values and responsive conventions already established in the project. Do not assume the project uses Tailwind CSS merely because these breakpoint tokens are referenced. If the project uses CSS Modules, vanilla CSS, or another styling system, apply the equivalent responsive behavior using the existing styling architecture.
- **Breakpoint Discrimination:** Pay careful attention to the distinctions between `sm`, `md`, and `lg`, particularly when deciding when a multi-column or desktop grid/dock should replace a mobile stack.
- **Full Viewport Usability:** These preferences do not permit ignoring intermediate viewport sizes. Layouts must remain completely usable, readable, and visually balanced at all intermediate widths between and beyond the primary checkpoints without clipping, overlap, or horizontal overflow.

---

## 7. API and Data Access Rules

Before implementing API or data-related functionality, the AI MUST inspect how the existing project handles:

- API requests and endpoints,
- authentication and authorization,
- headers and tokens,
- error handling,
- response handling,
- request validation,
- data fetching and persistence,
- caching,
- and related abstractions.

The AI MUST follow the existing pattern in the relevant area whenever possible.

The AI MUST NOT:

- Introduce a new API/service/data-access architecture merely because it may be cleaner.
- Replace an existing HTTP/data-access library without explicit permission.
- Create duplicate API abstractions when an appropriate existing abstraction already exists.
- Change global API configuration unless the requested task explicitly requires it and the change is authorized.
- Invent API endpoints, request parameters, response structures, or backend behavior.

The exact request and response behavior MUST be based on the actual project code, available documentation, or requirements provided by the user.

If the required API behavior is unclear, the AI MUST ask the user rather than guessing.

---

## 8. Requirements and Ambiguity

The AI MUST NOT guess when an important requirement is unclear.

If the AI does not understand:

- what the user wants,
- how a feature should behave,
- which file should be changed,
- which API should be called,
- what an API response means,
- what UI or system behavior is expected,
- which existing implementation should be followed,
- what technology or pattern should be used,
- or any other detail that materially affects the implementation,

it MUST stop and ask the user.

The AI should ask the smallest number of clear questions needed to continue.

Do not silently invent requirements.

### 8.1 Mandatory Ambiguity-Handling Process

For any genuine ambiguity, missing critical information, conflicting requirements, or significant decision requiring user input:
- The AI MUST use Antigravity's native interactive question/approval interface (`ask_question`).
- Present clear selectable options in Persian, plus an option equivalent to "Other / I'll provide my own instructions" that allows custom text.
- Do not provide a Skip option.
- Wait for the user's submitted answer before performing dependent work.
- Do not treat an unanswered question as approval.
- Do not ask the user to choose the order of the architecture migration or implementation steps; the AI must decide the safest order after inspecting the project and explain its reasoning.
- Do not interrupt the user for minor routine implementation choices.
- If the native interface cannot support the exact requested interaction, use its closest supported alternative. Never claim that an interaction occurred if it did not.
- All questions, options, explanations presented to the user, and reports must be in Persian, while keeping code identifiers, filenames, commands, and paths in their original form.

---

## 9. Code Quality and Correctness

The AI is expected to write correct code, not merely code that passes a superficial syntax check.

Before considering a task complete, the AI MUST:

- Check the code it wrote for syntax errors.
- Check imports, variables, function names, types, and references for obvious mistakes.
- Check that the new code is consistent with the existing project structure.
- Check that the implementation actually matches the user's request.
- Check that it did not accidentally introduce unrelated changes.
- Check that existing behavior is not unnecessarily changed.
- Check that the implementation does not introduce obvious duplication or unnecessary complexity.

### 9.1 Pragmatic Error Handling and Respecting Intentional Code

- **Distinguish Genuine Bugs from Opinionated Warnings:** The AI MUST distinguish between genuine runtime/logic bugs (e.g., broken imports, undefined variables, fatal type mismatches that break execution) and opinionated linter/type warnings or intentional patterns.
- **Respect Intentional Code:** If the user's code or requested pattern intentionally bypasses a strict type or linter preference (or triggers a pedantic warning that works fine in practice and matches the user's intent), the AI **MUST NOT** rewrite, over-engineer, or alter working logic just to appease the linter or type-checker.
- **Scope of Fixes:** Fix genuine bugs caused by the AI's own changes, and leave pre-existing warnings in untouched code alone.
- **Preserve User Logic:** If a strict lint or type rule conflicts with the user's intended implementation, keep the user's logic intact (or briefly note it in the final report without modifying the working code).

The AI MUST NOT knowingly leave obviously incorrect code merely because it is syntactically valid.

If the AI cannot confidently verify an important behavior without running the application or having information it does not have, it must clearly tell the user what remains unverified.

---

## 10. Running and Testing the Project

The AI should not take ownership of the user's normal development workflow unless the user explicitly asks it to do so.

### 10.1 Command Execution Rules

- **Forbidden Commands:** The AI MUST NOT start development servers, run build pipelines, or execute application start commands (e.g., `dev`, `build`, `start`, or framework/language-specific equivalents) on its own. The user will handle running the application and managing the development server.
- **Allowed Read-Only Checks:** While starting dev servers or running full builds remains strictly forbidden, the AI **is permitted and encouraged** to use existing project diagnostic tools (such as TypeScript type-checking e.g. `tsc --noEmit`, ESLint, or IDE language server diagnostics) if available in the project, strictly in **read-only mode** (never use `--fix` or auto-formatters automatically) and scoped to the modified files whenever possible.
- **Verification Focus:** The AI's required verification is primarily:
  - static inspection,
  - syntax correctness,
  - read-only diagnostic checks for genuine errors,
  - consistency with the existing code,
  - and checking for obvious implementation errors.

Do not make unnecessary changes just to accommodate a local development environment, and do not rewrite or alter working code merely to appease non-fatal linter or type warnings.

If the user explicitly asks the AI to run a particular verification, linter, or test command, follow that request if the environment allows it.

The AI MUST report what was actually verified and MUST NOT claim to have performed a test or verification that it did not perform.

---

## 11. Component, Module, and Abstraction Creation

Do not extract code into a new component, module, class, utility, hook, service, or abstraction merely because it might be reusable in the future.

Create/extract a separate abstraction when there is an actual current need.

General principles:

- Keep code local when it is only needed in one place and there is no concrete reason to extract it.
- Extract reusable code when there is a real reuse need.
- Prefer an existing abstraction when one already serves the purpose.
- Do not create abstraction layers without a real current use case.
- Avoid both unnecessary duplication and premature abstraction.

---

## 12. Existing Code and Refactoring

Preserve existing project conventions whenever possible.

The AI MUST NOT perform unrelated refactoring.

Examples of changes that require a concrete reason related to the current task:

- Renaming existing variables or functions throughout unrelated code.
- Reformatting large files.
- Moving files.
- Reorganizing folders.
- Rewriting working code into a preferred pattern.
- Changing state-management or data-flow patterns.
- Replacing existing libraries or APIs.
- "Cleaning up" unrelated code.
- Introducing a new abstraction when the existing implementation is sufficient.

If refactoring is necessary to implement the requested feature safely, explain the reason before making a significant refactor, and first obtain approval from the user; the AI is allowed to perform the refactoring only after receiving explicit user confirmation.

---

## 13. State Management and Application Patterns

Prefer the state-management and application patterns already used in the relevant area of the project.

The AI MUST:

- Inspect how nearby code manages state and data flow.
- Follow the existing pattern when appropriate.
- Reuse existing state-management mechanisms where possible.

The AI MUST NOT introduce:

- a new state-management library,
- a new architectural pattern,
- or a substantially different state-management approach

without explicit user approval, unless it is clearly required by the existing project and the requested task.

When multiple existing patterns are available, prefer the pattern already used by nearby code unless there is a concrete reason not to.

---

## 14. Handling Problems During Implementation

If the AI encounters a problem and the current implementation path is no longer reliable:

1. Stop rather than continuing to build on an incorrect assumption.
2. Identify the problem.
3. Determine the last point at which the implementation was known to be correct.
4. Tell the user:
   - what problem occurred,
   - what caused or appears to have caused it,
   - and from which point the implementation should continue.

5. Wait for the user's confirmation.
6. After confirmation, continue from the agreed correct point.

Do not silently undo/rewrite a large portion of the work and pretend nothing happened.

---

## 15. Rule Conflicts / Priority of Rules

User instructions and this file can sometimes conflict.

If a user request conflicts with a rule in this file:

1. Do NOT silently choose one side.
2. Identify the specific conflicting rule.
3. Explain briefly what the conflict is.
4. Ask the user whether they want the requested action to be performed despite that rule.
5. If the user explicitly confirms, perform the requested action.
6. Do NOT permanently modify or add an exception to `AGENTS.md` merely because the user approved the one-time conflict.
7. Record the relevant decision in `AGENT_CHANGELOG.md` if the change was actually made.

A one-time user approval is a one-time authorization unless the user explicitly states that the rule itself should be changed.

If the user later makes a similar request, the AI must not assume that an old exception is still valid unless the user explicitly confirms it applies again.

---

## 16. Change Boundaries

Before editing, the AI should be able to answer:

- What exact task am I implementing?
- Which files are required?
- Why does each file need to change?
- Which parts of the project are within scope?
- Who owns or maintains the files being changed?
- Are any rules being overridden by explicit user authorization?
- Is any unrelated code being touched?
- Which existing project patterns should be followed?

If these questions cannot be answered confidently, ask the user before editing.

---

## 17. AGENT_CHANGELOG.md Rules

After making changes, the AI MUST update `AGENT_CHANGELOG.md`.

### 17.1 Compact and Token-Efficient Entries

The AI MUST keep `AGENT_CHANGELOG.md` entries **ultra-concise and high-signal** (compact bullet points) to optimize context and token efficiency:

- **High-Signal Fields:** Include relevant fields when applicable:
  - Date
  - Task / Request
  - Files Changed
  - What Changed
  - Why It Changed
  - Important Decisions
  - Rule Conflicts / Explicit Exceptions
  - Verification Performed
  - Known Issues / Unverified Items
- **Omit Inapplicable Fields:** Omit empty or inapplicable fields entirely (e.g., if there were no rule conflicts, important decisions, or unverified items, do not include those headers).
- **Group Follow-up Tweaks:** Trivial follow-up tweaks within the same session can be grouped or appended concisely rather than generating bloated multi-section reports every time.

The changelog exists so a future AI agent can understand what previous agents did before making new changes.

An AI MUST NOT claim responsibility for changes it did not make.

An AI MUST NOT rewrite or erase historical changelog entries simply to make the history cleaner.

New entries should be appended chronologically.

---

## 18. Changelog Awareness

The changelog is historical context, not a replacement for the current code.

The AI MUST:

- Read it once at the start of a conversation/session (focusing primarily on the most recent entries rather than processing the entire historical log unless investigating a specific past change).
- Use recent entries to understand recent changes, conventions, and decisions.
- Verify historical information against the current code when necessary.
- Never assume that a previous AI's implementation is still present or correct without checking the relevant files.

If the changelog and the current code disagree, the current code should be treated as the source of truth for the current implementation, while the changelog should be treated as historical context.

---

## 19. Proposed Improvements and Approval

When implementing a request, the AI may identify additional changes that could improve the result but are not strictly required by the request.

The AI must:

1. Tell the user about each proposed improvement.
2. Briefly explain its purpose.
3. Clearly distinguish optional improvements from changes required to complete the requested task.
4. Wait for the user's explicit approval before making optional improvements.

Changes that are necessary to implement the user's request may be made without separate approval, provided they:

- remain within the requested scope,
- follow the existing project conventions,
- and do not conflict with another rule in this document.

---

## 20. Final Response After a Change

After completing a task, the AI should clearly report:

1. What was changed.
2. Which files were changed.
3. Any important implementation decision.
4. What was verified.
5. Anything that could not be verified.
6. Any package/dependency that would be needed but was intentionally not installed.
7. Any rule conflict that the user explicitly authorized.

Keep the report concise and factual.

---

## 21. Core Principle

When uncertain, prefer:

**ask > inspect > identify required and optional changes > get approval for optional changes > implement > verify > document**

Do not guess, do not overreach, and do not modify unrelated parts of the project.
