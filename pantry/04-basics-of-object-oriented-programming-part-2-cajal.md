# CAJAL Figure Intelligence — Module 4: Basics of Object-Oriented Programming Part 2

**Source:** `chapters/04-basics-of-object-oriented-programming-part-2.md`
**Mode:** `/scan silent`
**Domain note:** CS textbook. Author has pre-specified figures via inline `[SCOPE | ...]` markers. Layout-purpose palette; Okabe-Ito governs.

---

## Density Recommendation

**2 figures, Foundational density.** Fig 4.1 (three-level diagnostic hierarchy: symptom → proximate → root) and Fig 4.2 (three-phase debugging workflow loop). Fig 4.3 in the draft is a near-duplicate of Fig 4.2 reformatted horizontally — drop the duplicate; keep Fig 4.2 as the canonical version. The chapter is a debugging chapter and two well-architected figures carry the work.

**Cut from current draft:** Fig 4.3 — duplicates Fig 4.2 with the same three-phase loop concept in a different orientation. CAJAL rejects: same concept, same components, same exclusion list. Pick one.

---

## Zone Map

- **MC:** The Hypothesize / Isolate / Test loop — debugging as causal reasoning with explicit return on refuted hypotheses.
- **VG:** Three-level diagnostic hierarchy (symptom / proximate / root) — students default to fixing the symptom; the figure shows the upstream relationship.
- **PQ:** None.

---

## Figure Validation (Author-Specified, CAJAL-Validated)

| # | Figure | Type | Priority | Components | Exclusion list present | Validates |
|---|---|---|---|---|---|---|
| 4.1 | Symptom / proximate / root hierarchy | Hierarchy | Critical | 5 | ✓ | ✓ |
| 4.2 | Hypothesize → Isolate → Test loop | Cycle / process flowchart | Critical | 5 | ✓ | ✓ |
| 4.3 | (Duplicate of 4.2 in horizontal orientation) | — | — | — | — | Drop |

---

## Video Candidate Pass

**FIGURE 4.2 (Debugging loop):** STATIC SUFFICIENT — borderline. A short animation showing a hypothesis getting refuted and the dashed return arrow firing would communicate the iteration viscerally. But the cycle is a discipline the student practices, not a process they watch — static lets them rehearse the loop themselves.

**FIGURE 4.1 (Diagnostic hierarchy):** STATIC SUFFICIENT.

**Video candidates identified: 0.**

---

## Split-point note

The chapter's debugging case tables and AI-boundary prompts are typography. Code listings handled by the layout system, not CAJAL.

---

## CAJAL discipline checks

- Component counts: within 6–8 limit ✓
- Exclusion lists: present and specific ✓
- Figure types match: hierarchy (correct for upstream-causation diagnostic), cycle (correct for iterative debugging) ✓
- Author's inline SCOPE markers are source of truth for Illustrae paste blocks ✓
- Recommendation: collapse Fig 4.3 into Fig 4.2; ship two figures rather than three
