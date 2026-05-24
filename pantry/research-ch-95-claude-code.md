# Research: Chapter 95 — Claude Code for Java
## Programming with Java: An Object-Oriented Practicum

**Chapter one-line:** Appendix that helps students use Claude Code for Java throughout the course without bypassing the understanding, debugging, and verification work each module requires.
**Research date:** 2026-05-23

---

## 1. Primary Sources

### Foundational papers and texts
- Anthropic, "Claude Code settings," current documentation. Relevant because it explains project and user settings, permissions, memory files, hooks, and sensitive-file denial rules. The appendix should teach students that Claude Code is not just a chat box; it has file access, edit ability, shell access, and configurable boundaries.
- Anthropic, "Manage Claude's memory," current documentation. Relevant because it identifies project `CLAUDE.md` as shared project memory and user `CLAUDE.md` as personal memory. The course can use this distinction to tell students where course constraints belong.
- Anthropic, "Slash commands," current documentation. Relevant because custom commands can turn repeated course routines into project commands: `/explain-error`, `/review-handler`, `/test-cases`, and `/ai-disclosure`.
- Anthropic, "CLI reference," current documentation. Relevant because students need minimal command fluency: `claude`, `claude -p`, continuation, and status/config commands. The appendix should keep CLI use practical and avoid overwhelming beginners.
- Robins, Rountree, and Rountree, "Learning and Teaching Programming," 2003; Sweller, "Cognitive Load During Problem Solving," 1988; Collins, Brown, and Newman, "Cognitive Apprenticeship," 1989. These support the appendix's teaching position: AI assistance must reduce incidental friction without removing prediction, tracing, debugging, testing, and explanation.

### Key empirical cases
- Course case: a student lets Claude Code "fix" a JavaFX handler, accepts a working patch, then cannot explain why model state changed twice. This is illustrative but central: code changed faster than understanding.
- Course case: a student uses Claude Code to ask for five hypotheses about a bug before showing code. The student then tests the hypotheses in NetBeans. This preserves the Module 4 phase gate.
- Tooling case: Claude Code can read and edit project files and run shell commands when permitted. This makes settings and permissions a learning issue, not merely a security issue.

---

## 2. The Core Concept — State of the Field

### What is settled
Claude Code is designed for codebase-aware work: reading files, editing files, running commands, using project memory, and following project settings. That makes it more powerful than a plain chat assistant and more dangerous if students use it without boundaries. Programming education research supports worked examples, prediction, explanation, and debugging practice; those learning activities should not be erased by an assistant that can make direct edits.

### What is disputed
The contested question is how much AI assistance is appropriate in a first Java application-engineering course. The book's position is that AI use should escalate by module: diagnostic only, then scaffold, then implementation assist, then full collaboration. The appendix should not argue that Claude Code is bad; it should teach when Claude Code is allowed to act and what students must verify.

### What has changed recently
Claude Code product behavior, command names, permission modes, settings schemas, and memory locations may change. Anything about installation, subscriptions, model names, or exact command behavior should be verified before each offering. The stable content is the course logic: students must specify, trace, test, and explain what they accept.

---

## 3. Application Domain Examples

- Library: use Claude Code to inspect `Book`, `Patron`, and `CheckoutTransaction`, then ask for questions that test whether the student understands object state.
- Inventory: use Claude Code to generate class stubs from a written `Product` and `StockMovement` specification, then manually implement method bodies.
- Scheduling: use Claude Code to map FXML `fx:id` values to controller fields, then require the student to verify each connection by running the GUI.
- Debugging: use Claude Code to critique a stated bug hypothesis before it reads the code.
- Final project: use Claude Code to produce a consistency report across classes, tests, AI disclosures, and the final defense matrix.

---

## 4. The Book's Thesis Connection

This appendix directly supports the book's thesis: AI-assisted development is productive only when the student understands enough to verify the output. Claude Code can accelerate many parts of the course, but it can also erase the learning evidence if used too early. The appendix therefore turns tool use into a structured engineering practice.

The student supplies problem formulation, project requirements, object boundaries, debugging hypotheses, collection-choice rationale, security assumptions, testing meaning, and final defense. Claude Code can help inspect, explain, scaffold, and sometimes implement, but it cannot own the requirement or the verification.

---

## 5. The AI Wayback Machine — Candidate Figures

- **Grace Hopper** — Debugging, compiler history, and operational accountability. Prompt: "Imagine Grace Hopper reviewing my Claude Code workflow. What evidence would convince her I understood the bug rather than accepted a patch?"
- **Margaret Hamilton** — Software reliability and responsibility for system behavior. Prompt: "Imagine Margaret Hamilton reviewing my final project CLAUDE.md. What failure modes would she say I failed to protect?"
- **Watts Humphrey** — Software process discipline and personal software process. Prompt: "Imagine Watts Humphrey reviewing my AI Use Disclosure. What process evidence is missing?"

---

## 6. Pedagogical Delivery Research

The appendix should be procedural and concrete. The target reader is not ready for a long discussion of AI philosophy. They need a repeatable routine: state the requirement, choose the allowed assistance level, ask Claude Code, inspect the output, test or trace it, then write the disclosure.

Common misconceptions:
- "Claude Code is in the terminal, so it is automatically more technical and trustworthy."
- "If Claude Code edits the file directly, I can skip reading the diff."
- "A project CLAUDE.md is a magic rule that prevents misuse."
- "Tests generated by Claude Code prove the code is correct."

The appendix should include templates students can copy, but every template should force project-specific details. A generic CLAUDE.md is too weak for Module 14.

---

## 7. Representation and Display Research

Required displays:
- A phase-gate table from Module 0 through Module 14.
- A "before you ask / while Claude works / before you accept" workflow card.
- A project directory sketch showing `CLAUDE.md`, `.claude/settings.json`, `.claude/commands/`, `src/`, and `test/`.
- An AI Use Disclosure template.

---

## 8. Open Questions and Research Gaps

- Verify exact Claude Code installation and login steps before course release.
- Decide whether student projects should include `.claude/settings.json` or only `CLAUDE.md`.
- Decide whether custom slash commands should be provided as course files or written by students.
- Decide what permissions are safe in a classroom environment, especially shell commands and file writes.
- Confirm whether "Claude Code" should remain the named tool or whether the appendix should become tool-agnostic.

---

## 9. Sourcing Notes

Use Anthropic documentation for Claude Code product claims. Do not rely on blog posts for settings, permissions, memory locations, or command behavior. For pedagogy claims, cite programming-education research and the course's TIKTOC. Mark installation details and command behavior as high-aging-risk.
