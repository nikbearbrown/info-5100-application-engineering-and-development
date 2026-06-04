# CAJAL Figure Intelligence — Module 12: Recursion

**Source:** `chapters/12-recursion.md`
**Mode:** `/scan silent`
**Domain note:** CS textbook. Author has pre-specified four figures via inline `[SCOPE | ...]` markers. Despite the chapter's title pointing at recursion, the actual figure set is about *FXML, controller injection, and end-to-end traceability* — the chapter teaches the FXMLLoader lifecycle and the controller-injection contract.

---

## Density Recommendation

**4 figures, Mechanistic density.** Java-code-vs-FXML equivalence within the view layer (12.1), FXMLLoader injection with match/mismatch paths (12.2), JavaFX controller lifecycle as four sequential phases (12.3), end-to-end traceability chain with broken-version (12.4). Each figure carries a distinct claim about the FXML-controller seam.

---

## Zone Map

- **MC:** Controller lifecycle — four phases with @FXML field state changing across them. The phase-1 "null fields" trap is the chapter's single most important warning, and the figure has to make the field-state transition visible.
- **VG:** Java-vs-FXML equivalence (same structure, two representations); FXMLLoader as bridge between fx:id and @FXML field (with the broken-link failure mode); end-to-end traceability chain (with the looks-right-but-makes-no-model-call failure).
- **PQ:** None.

---

## Figure Validation (Author-Specified, CAJAL-Validated)

| # | Figure | Type | Priority | Components | Exclusion list present | Validates |
|---|---|---|---|---|---|---|
| 12.1 | Java code vs. FXML equivalence within view layer | Comparison panels | Important | 7 | ✓ | ✓ |
| 12.2 | FXMLLoader injection: match vs. mismatch | Process flowchart (paired) | Critical | 6 | ✓ | ✓ |
| 12.3 | Controller lifecycle: four phases | Timeline / progression | Critical | 8 | ✓ | ✓ |
| 12.4 | Traceability chain with broken-version | Comparison panels | Critical | 8 | ✓ | ✓ |

Figs 12.3 and 12.4 at 8 components each are at the absolute upper limit. CAJAL accepts both: the lifecycle requires four phase bands plus three field-state indicators plus the FXMLLoader actor; the traceability chain requires five-node connected chain plus five-node broken chain. Both are minimal architecturally.

---

## Video Candidate Pass

**FIGURE 12.3 (Controller lifecycle):** **VIDEO CANDIDATE.** Criterion 2 (three or more sequential causal stages) and criterion 1 (transition mechanism is the learning target). Watching @FXML fields transition from null in phase 1 to populated in phase 2, to setup-ready in phase 3, to event-responsive in phase 4 would communicate the lifecycle viscerally — and the phase-1 null trap (the chapter's single most-warned-against bug) becomes immediately obvious when motion shows fields filling between phases. Suggested format: looping animation with phase bands progressing top-to-bottom, field shapes transitioning empty→filled at the injection moment, warning indicator pulsing at phase 1.

**FIGURE 12.4 (Traceability chain):** STATIC SUFFICIENT — borderline. Both connected and broken versions side-by-side make the comparison cleanly.

**Others:** STATIC SUFFICIENT.

**Video candidates identified: 1.** Recommended: **Fig 12.3** — the controller lifecycle is the chapter's hardest concept and the phase-transition mechanism is exactly what motion communicates that static cannot.

---

## Split-point note

The chapter's actual *recursion* content (factorials, Fibonacci, base/recursive cases) appears in the prose but is not figure-architected by the author — likely because recursion's canonical figure (the call stack / recursion tree) is a textbook standard that the chapter handles by reference rather than building from scratch. CAJAL flags: if the chapter wants a call-stack-unrolling figure for the factorial example, it would be a video candidate (criterion 4: transformation below direct observation), but the author has deliberately left it out. Editorial decision.

---

## CAJAL discipline checks

- Component counts: within 6–8 limit (two figures at upper limit, both justified) ✓
- Exclusion lists: present and specific ✓
- Figure types match: comparison panels (correct for equivalence and broken-vs-intact), process flowchart (correct for injection paths), timeline (correct for lifecycle phases) ✓
- One video candidate flagged: Fig 12.3 (controller lifecycle phases)
- Note: the recursion-tree figure that the chapter title would suggest is *absent* from the author's figure architecture — flag for editorial decision
