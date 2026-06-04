# CAJAL Figure Intelligence — Module 5: Inheritance and Polymorphism

**Source:** `chapters/05-inheritance-and-polymorphism.md`
**Mode:** `/scan silent`
**Domain note:** CS textbook. Author has pre-specified six figures via inline `[SCOPE | ...]` markers. Layout-purpose palette; Okabe-Ito governs.

---

## Density Recommendation

**5 figures, Mechanistic density.** Entity/Relationship/Transaction taxonomy (Fig 5.1) is a typography table — drop from figure budget. Keep five: supply-side vs. transaction-coupled (5.2), Catalog class boundary (5.3), shared Author across multiple Books (5.4), annotated main() with supply/demand divider (5.5), AI three-stage workflow (5.6).

The chapter's central craft move is the supply/demand separation, and each figure carries a distinct argumentative beat. Five is at the upper boundary; justified because the chapter is the OOP architectural turn the rest of the book builds on.

**Cut from current draft:** Fig 5.1 (entity/relationship/transaction table) — typography, not a CAJAL figure. Hand to the typesetter as a styled three-column comparison table.

---

## Zone Map

- **MC:** Supply-side preloaded vs. transaction-coupled construction — the architectural antipattern the chapter is correcting.
- **VG:** Catalog class boundary (state inside / interface outside / *not knowing about* zone) — the encapsulation claim made spatial. Shared-reference object graph (two Books sharing one Author object) — extends Ch 2's reference model to multi-object graphs.
- **PQ:** None.

---

## Figure Validation (Author-Specified, CAJAL-Validated)

| # | Figure | Type | Priority | Components | Exclusion list present | Validates |
|---|---|---|---|---|---|---|
| 5.1 | Entity/Relationship/Transaction | — (table, not figure) | — | — | — | Drop |
| 5.2 | Supply-coupled vs. preloaded | Comparison panels | Critical | 6 | ✓ | ✓ |
| 5.3 | Catalog class boundary | Structural schematic | Critical | 6 | ✓ | ✓ |
| 5.4 | Author shared across Books | Structural schematic | Important | 5 | ✓ | ✓ |
| 5.5 | main() with supply/demand divider | Annotated example | Important | 6 | ✓ | ✓ |
| 5.6 | AI three-stage workflow | Process flowchart | Important | 4 | ✓ | ✓ |

All five within the 6–8 component limit. All carry populated exclusion lists. Author's inline SCOPE markers are source of truth.

---

## Video Candidate Pass

**FIGURE 5.4 (Shared Author graph):** STATIC SUFFICIENT. The "update once, propagates" claim could be animated, but the chapter handles it via Ch 2's reference-model groundwork — static lets the student inspect the multi-arrow convergence pattern.

**Other four:** STATIC SUFFICIENT.

**Video candidates identified: 0.**

---

## Split-point note

The chapter's CRUD-comparison tables and AI workflow tables are typography. The entity/relationship/transaction classification (draft Fig 5.1) is typography. Code listings handled by layout.

---

## CAJAL discipline checks

- Component counts: all within 6–8 limit ✓
- Exclusion lists: present and specific in all five retained figures ✓
- Figure types match: comparison panels (correct for design contrast), structural schematic (correct for class boundaries and object graphs), annotated example (correct for code with semantic regions), process flowchart (correct for AI workflow sequence) ✓
- One drop recommended: Fig 5.1 is structurally a table, not a figure
