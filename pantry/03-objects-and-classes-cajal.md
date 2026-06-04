# CAJAL Figure Intelligence — Module 3: Objects and Classes

**Source:** `chapters/03-objects-and-classes.md`
**Mode:** `/scan silent`
**Domain note:** CS textbook. Author has pre-specified three figures via inline `[SCOPE | ...]` markers AND a complete end-of-chapter CAJAL SCOPE OUTPUTS section. CAJAL validates and applies discipline.

---

## Density Recommendation

**3 figures, Mechanistic density.** The chapter pivots on three architectural claims: screen-centric vs. state-centric mental models, CardLayout container mechanics, and the three-layer responsibility separation. Each earns one figure. The chapter explicitly cuts other candidate figures (the staging object pattern, the lost-reference vs. premature-display failure modes) and handles them in prose + typography tables.

---

## Zone Map

- **MC:** CardLayout container behavior (one visible panel, three dormant) — mechanism shape the prose names but cannot show.
- **VG:** Screen-centric vs. state-centric mental model (the foundational reframe); three-layer responsibility separation (visibility / display / state).
- **PQ:** None.

---

## Figure Validation (Author-Specified, CAJAL-Validated)

| # | Figure | Type | Priority | Components | Exclusion list present | Validates |
|---|---|---|---|---|---|---|
| 3.1 | Screen-centric vs. state-centric mental model | Comparison panels | Critical | 6 | ✓ | ✓ |
| 3.2 | CardLayout container structure | Structural schematic | Important | 5 | ✓ | ✓ |
| 3.3 | Three-layer responsibility model | Hierarchy / layered stack | Critical | 5 | ✓ | ✓ |

All three within the 6–8 component limit. All exclusion lists populated and specific. The chapter's end-of-chapter CAJAL SCOPE OUTPUTS section contains complete Illustrae paste blocks for all three — use as source of truth.

---

## Video Candidate Pass

**FIGURE 3.1 (Screen-centric vs. state-centric):** STATIC SUFFICIENT — borderline. The "object travels through the flow" claim could be animated as the Book object sliding along the baseline through each screen position. But static comparison panels with the same object shape rendered at four positions communicate persistence cleanly without motion overhead.

**FIGURE 3.2 (CardLayout container):** STATIC SUFFICIENT. The "one visible, others dormant" relationship is spatial, not temporal. A switching animation would invent a sequence the chapter doesn't require.

**FIGURE 3.3 (Three-layer responsibility):** STATIC SUFFICIENT. Layered hierarchies are structural.

**Video candidates identified: 0.** No production recommended.

---

## Split-point note

The chapter's state-table for the four screens (search/result/checkout/confirmation × objects-read/objects-modified/entry-state/exit-state) is typography — hand to the typesetter as a styled comparison matrix. The failure-mode table (Lost Reference / Premature Display) is typography. The AI-boundary prompt is a code block, not a figure.

The staging-object pattern (Appointment partially constructed across screens) is named in prose; CAJAL declines to add a fourth figure because the pattern is a small extension of Fig 3.1's state-centric model, not a structurally distinct concept.

---

## CAJAL discipline checks

- Component counts: all within 6–8 limit ✓
- Exclusion lists: present, specific, and *excellent* (the chapter's end-of-chapter SCOPE outputs explicitly exclude UML notation, database icons, network diagrams, code text, dual-headed arrows — exactly the noise that defeats CS-textbook figures) ✓
- No red-green combinations ✓
- No text-in-image ✓
- Figure types match concept structure: comparison panels (correct for two-mental-model contrast), structural schematic (correct for container-with-children), layered hierarchy (correct for separation-of-concerns claim)

The author's end-of-chapter CAJAL SCOPE OUTPUTS section is the source of truth for Illustrae paste blocks. This CAJAL output certifies architectural compliance with CAJAL discipline and adds density recommendation + video pass.
