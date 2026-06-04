# CAJAL Figure Intelligence — Module 8: Abstract Classes and Interfaces

**Source:** `chapters/08-abstract-classes-and-interfaces.md`
**Mode:** `/scan silent`
**Domain note:** CS textbook. Author has pre-specified five figures via inline `[SCOPE | ...]` markers. Despite the chapter's title pointing at abstract classes and interfaces, the actual figure set is about *persistence* — the read/write/durability problem that motivates interfaces (as durability contracts) in later modules.

---

## Density Recommendation

**5 figures, Mechanistic density.** CRUD-with-persistence-failures table (8.1), write/read path with failure markers (8.2), object-to-file lifecycle with failure callouts (8.3), memory-vs-file timeline with data-loss window (8.4), three-question persistence design form (8.5). Five figures earn their place because the chapter is the OOP module where students first confront the difference between in-memory state (perfect, immediate) and persistent state (failure-prone, lagging).

**Note:** Fig 8.1 is the CRUD comparison table — author marks it as `TABLE`, not `IMAGE`. CAJAL agrees: this is typography, not a figure. Drop from CAJAL budget; hand to typesetter.

**Cut from current draft:** Fig 8.1 (CRUD operations table) — typography. The author's own `[SCOPE | ... TABLE: ...]` tag is the correct designation.

---

## Density (revised): **4 figures, Mechanistic density.**

---

## Zone Map

- **MC:** Write-path / read-path with failure points (8.2); object-to-file-to-object lifecycle (8.3); memory-vs-file timeline with data-loss window (8.4).
- **VG:** Three-question persistence design form (8.5) — the engineer's decision-surface made visual.
- **PQ:** None directly chartable. Fig 8.4's data-loss window is a temporal-span representation, not a quantitative chart.

---

## Figure Validation (Author-Specified, CAJAL-Validated)

| # | Figure | Type | Priority | Components | Exclusion list present | Validates |
|---|---|---|---|---|---|---|
| 8.1 | CRUD operations comparison | — (table, not figure) | — | — | — | Drop (typography) |
| 8.2 | Write path / read path with failures | Process flowchart (paired) | Critical | 8 | ✓ | ✓ |
| 8.3 | Object → file → object lifecycle | Process flowchart | Critical | 7 | ✓ | ✓ |
| 8.4 | Memory vs. file timeline with data-loss window | Timeline / progression | Critical | 6 | ✓ | ✓ |
| 8.5 | Three-question persistence design form | Annotated example / decision form | Important | 4 | ✓ | ✓ |

Fig 8.2 at 8 components is at the absolute upper limit — the chapter pairs write-path and read-path symmetrically. CAJAL accepts: the pair is one figure architecturally (symmetric failure surfaces), not two.

---

## Video Candidate Pass

**FIGURE 8.4 (Memory vs. file timeline):** **VIDEO CANDIDATE.** Criterion 1 (transition mechanism is the learning target) — the data-loss window is *the* concept, and watching the memory track jump while the file track lags would viscerally communicate the durability gap that the static figure has to encode through shading. Suggested format: looping animation showing the mutation event firing on the memory track, the file track lagging until the save event closes the gap, and a crash annotation falling inside the gap.

**FIGURE 8.3 (Lifecycle):** STATIC SUFFICIENT — borderline. Five sequential nodes with failure callouts, but the failures are simultaneous-possibility-states, not sequential events.

**Other two:** STATIC SUFFICIENT.

**Video candidates identified: 1.** Recommended: **Fig 8.4** — the data-loss window is the chapter's hardest concept to convey statically, and motion makes the temporal gap immediately legible. If the editorial budget allows one video for the persistence cluster, this is it.

---

## Split-point note

The CRUD-with-persistence-failures table (Fig 8.1) is typography. Code listings are typography. The three-question form (Fig 8.5) is structurally a styled callout box that could be either a CAJAL figure or rich typography — author has tagged it as IMAGE, CAJAL accepts.

---

## CAJAL discipline checks

- Component counts: within 6–8 limit (Fig 8.2 at the absolute upper boundary, with pairing structure justifying it) ✓
- Exclusion lists: present and specific ✓
- Figure types match: process flowchart (correct for write/read paths), timeline (correct for memory-vs-file lag), decision form (correct for engineer-facing question structure) ✓
- One drop recommended: Fig 8.1 is structurally a table
- One video candidate flagged: Fig 8.4 (data-loss window is a transition mechanism, not a state pair)
