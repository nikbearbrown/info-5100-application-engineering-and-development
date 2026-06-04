# CAJAL Figure Intelligence — Module 2: Methods, Arrays, and File Objects

**Source:** `chapters/02-methods-arrays-and-file-objects.md`
**Mode:** `/scan silent`
**Domain note:** CS textbook. The chapter author has pre-specified figures via inline `[SCOPE | ...]` markers. CAJAL validates the architecture and applies the discipline. Layout-purpose palette in effect; Okabe-Ito governs.

---

## Density Recommendation

**5 figures, Mechanistic density.** The chapter's core craft is the reference-vs-object mental model, and visualizing the stack/heap relationship is *exactly* what the prose alone cannot do. Five figures (Fig 2.1 single reference, Fig 2.2 two independent objects, Fig 2.3 shared-reference trap, Fig 2.4 trace before/after, Fig 2.5 AI boundary flowchart) earn their place. Density is at the upper bound; justified by the fact that the chapter's whole pedagogical claim is *the mental model is the artifact*.

---

## Zone Map

- **MC:** Stack/heap reference mechanics; the trace-before-run craft; the AI boundary flowchart.
- **VG:** Where values live — the spatial claim that two reference variables can either point to distinct heap blocks or the same one. The shared-reference trap is the single most-misunderstood spatial relationship in introductory OOP.
- **PQ:** None (the chapter resists chartable data deliberately).

---

## Figure Validation (Author-Specified, CAJAL-Validated)

| # | Figure | Type | Priority | Components | Exclusion list present | Validates |
|---|---|---|---|---|---|---|
| 2.1 | Reference variable → heap object | Structural schematic | Critical | 4 | ✓ | ✓ |
| 2.2 | Two independent objects | Structural schematic | Critical | 6 | ✓ | ✓ |
| 2.3 | Shared-reference trap | Structural schematic | Critical | 6 | ✓ | ✓ |
| 2.4 | Trace-before-run | Comparison panels | Important | 5 | ✓ | ✓ |
| 2.5 | AI boundary flowchart | Process flowchart | Important | 6 | ✓ | ✓ |

All five within the 6–8 component limit. All five carry populated exclusion lists. Author has done the architecture work; full Illustrae paste blocks live in the chapter's inline SCOPE markers — use those as primary source.

---

## Video Candidate Pass

**FIGURE 2.3 (Shared-reference trap):** STATIC SUFFICIENT — borderline. An animated sequence showing `patronC = patronA` collapsing two arrows onto the same heap block would communicate the mutation propagation viscerally. But static panels with explicit arrow convergence let students inspect the relationship at their own pace, which the chapter's tracing discipline values.

**FIGURE 2.4 (Trace before/after):** STATIC SUFFICIENT. The whole point is to compare prediction-on-paper to actual-output side by side.

**Other three:** STATIC SUFFICIENT.

**Video candidates identified: 0.** No production recommended.

---

## Split-point note

The chapter's tables (artifact-to-concept mapping, display vs. toString comparison, AI-may-do/student-must-verify) are typography — hand to the typesetter. The CLI quick-reference block is typography. Code listings throughout are typography handled by the layout system, not CAJAL.

---

## CAJAL discipline checks

- Component counts: all within 6–8 limit ✓
- Exclusion lists: present and specific in every inline marker ✓
- No red-green combinations specified ✓
- No text-in-image specified ✓
- No style suggestions to Illustrae ✓
- Figure types match concept structure: structural schematics for memory diagrams (correct), comparison panels for trace-before/after (correct), process flowchart for AI boundary decision (correct)

Author's inline SCOPE markers are the source of truth for Illustrae paste blocks. This CAJAL output certifies that the architecture passes CAJAL discipline checks.
