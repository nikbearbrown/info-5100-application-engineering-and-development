# CAJAL Figure Intelligence — Module 11: Generics

**Source:** `chapters/11-generics.md`
**Mode:** `/scan silent`
**Domain note:** CS textbook. Author has pre-specified six figures via inline `[SCOPE | ...]` markers. Despite the chapter's title pointing at generics, the actual figure set is about *event handlers and single-responsibility design* — the chapter teaches generics through the lens of clean handler design.

---

## Density Recommendation

**6 figures, Mechanistic density.** All six earn their place: three-part event structure with registration forms (11.1), handler responsibility decomposition (11.2), code comparison closet-vs-clean handler (11.3), click-to-view chain with bug-locations (11.4), before/after deadline refactor (11.5), AI-fills-stubs vs. you-fill-bodies split (11.6).

Six is the absolute upper boundary for a single chapter; CAJAL accepts because the chapter is the *teach single-responsibility through visible architectural contrast* module, and each figure carries a structurally distinct argumentative beat that the prose alone cannot make spatial.

---

## Zone Map

- **MC:** Click-to-view chain (11.4) — the seven-node trace from user event through framework, handler, model, view update.
- **VG:** Closet handler vs. clean 4-line handler (11.3) — the architectural antipattern made visible. Same handler before/after a deadline-driven refactor (11.5) — the durability claim.
- **PQ:** None.

---

## Figure Validation (Author-Specified, CAJAL-Validated)

| # | Figure | Type | Priority | Components | Exclusion list present | Validates |
|---|---|---|---|---|---|---|
| 11.1 | Event structure + three registration forms | Annotated example | Important | 6 | ✓ | ✓ |
| 11.2 | Handler responsibility decomposition | Systems diagram | Critical | 4 | ✓ | ✓ |
| 11.3 | Closet vs. clean handler code comparison | Annotated example (paired) | Critical | 8 | ✓ | ✓ |
| 11.4 | Click-to-view chain with bug-location callouts | Process flowchart | Critical | 7 | ✓ | ✓ |
| 11.5 | Before/after deadline refactor | Comparison panels | Important | 6 | ✓ | ✓ |
| 11.6 | AI scaffolds / you fill bodies | Comparison panels | Important | 6 | ✓ | ✓ |

Fig 11.3 at 8 components (7 annotated rows + 4-line clean side) is at the absolute upper limit; CAJAL accepts because the architectural contrast requires showing the actual annotation density of the antipattern.

---

## Video Candidate Pass

**FIGURE 11.4 (Click-to-view chain):** STATIC SUFFICIENT — borderline. The click-to-view trace is sequential, but it's also the diagnostic instrument the chapter teaches; students need to *read* the trace, not watch it.

**Others:** STATIC SUFFICIENT.

**Video candidates identified: 0.**

---

## Split-group note

This is one of the highest-density chapters in the book. CAJAL's normal recommendation would be to split into two chapters at the natural seam (handler design vs. AI workflow), but the author has deliberately kept it as one — the single-responsibility argument is the *whole point* and splitting would dilute it. The figure density is the consequence.

---

## CAJAL discipline checks

- Component counts: within 6–8 limit (Fig 11.3 at upper limit) ✓
- Exclusion lists: present and specific ✓
- Figure types match: annotated examples (correct for code-with-callouts), systems diagram (correct for handler with responsibility branches), process flowchart (correct for click-to-view chain), comparison panels (correct for before/after structural shifts) ✓
- Six figures is the upper density bound; justified by the chapter's load-bearing role in the architectural sequence
