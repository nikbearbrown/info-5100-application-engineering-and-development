# Assertions Report: 95-claude-code.md
**Date:** 2026-05-25
**Source file:** chapters/95-claude-code.md
**Assertions flagged:** 4
**Breakdown:** STAT: 0 | GUIDELINE: 1 | APPROVAL: 0 | EVIDENCE: 0 | SPECIALIST: 0 | CURRENT: 3

---

## ⚠️ Critical — Requires Immediate Expert Review
None found.

---

## Full Findings

### CURRENT — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** Claude Code is powerful in this course because it can work inside your project. It can read your files, trace your object structure, find inconsistencies across modules, suggest test cases, and generate scaffolding.
**Claim checked:** Claude Code can operate in a project/codebase and help with code navigation, edits, commands, and coding tasks.
**Site visited:** https://docs.anthropic.com/en/docs/claude-code/overview
**Finding:** Anthropic describes Claude Code as an agentic coding tool that works in the terminal, can navigate a codebase, edit files, run commands, and create commits.
**Expert review needed:** No
**Suggested reference:** Anthropic. Claude Code overview. Anthropic Docs, accessed 2026-05-25. https://docs.anthropic.com/en/docs/claude-code/overview
**Notes:** None.

### CURRENT — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** Claude Code can be configured with project and user settings that control which files it can read, which commands it can run, and what tools it can invoke.
**Claim checked:** Claude Code settings and permissions configure access and tools.
**Site visited:** https://docs.anthropic.com/en/docs/claude-code/settings
**Finding:** Anthropic documents settings files, permission rules, tool behavior, memory files, and deny rules for excluding sensitive files.
**Expert review needed:** No
**Suggested reference:** Anthropic. Claude Code settings. Anthropic Docs, accessed 2026-05-25. https://docs.anthropic.com/en/docs/claude-code/settings
**Notes:** None.

### GUIDELINE — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** API keys, database credentials, private keys, and `.env` files should be excluded from AI tool access by default.
**Claim checked:** Claude Code settings support deny rules for excluding sensitive files.
**Site visited:** https://docs.anthropic.com/en/docs/claude-code/settings
**Finding:** Anthropic documents settings files, permission rules, tool behavior, memory files, and deny rules for excluding sensitive files.
**Expert review needed:** No
**Suggested reference:** Anthropic. Claude Code settings. Anthropic Docs, accessed 2026-05-25. https://docs.anthropic.com/en/docs/claude-code/settings
**Notes:** None.

### CURRENT — CONFIRMED
**Assertion type:** POSITIVE
**Sentence:** When additional actions are needed, editing files, running tests, and executing commands require explicit permission under Claude Code's default security model.
**Claim checked:** Claude Code uses a permission-based architecture for non-read actions.
**Site visited:** https://docs.anthropic.com/en/docs/claude-code/security
**Finding:** Anthropic describes Claude Code's permission-based architecture and states that editing files, running tests, and executing commands require explicit permission under default behavior.
**Expert review needed:** No
**Suggested reference:** Anthropic. Security. Anthropic Docs, accessed 2026-05-25. https://docs.anthropic.com/en/docs/claude-code/security
**Notes:** None.

---

## Unverified Assertions
None found.

---

## AI-Pass Flags
No internal contradictions or clearly incorrect definitions found during this pass.
