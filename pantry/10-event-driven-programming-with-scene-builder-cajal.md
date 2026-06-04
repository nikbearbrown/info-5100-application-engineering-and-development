# CAJAL Figure Intelligence — Module 10: Event-Driven Programming with Scene Builder

**Source:** `chapters/10-event-driven-programming-with-scene-builder.md`
**Mode:** `/scan silent`
**Domain note:** CS textbook. Author has pre-specified three figures via inline `[SCOPE | ...]` markers. The chapter introduces MVC through the Scene Builder workflow.

---

## Density Recommendation

**3 figures, Mechanistic density.** MVC responsibility map (10.1), scene graph tree (10.2), three-layer stack as built in the project (10.3). Each figure carries a distinct architectural claim about the View/Controller/Model separation that anchors the rest of the JavaFX work.

---

## Zone Map

- **MC:** MVC bidirectional flow — state and method calls in both directions between Model, Controller, View.
- **VG:** Scene graph tree (10.2) — the parent/child JavaFX hierarchy. Three-layer stack with controller as the "seam" (10.3) — the architectural claim that view reaches into model in exactly one place.
- **PQ:** None.

---

## Figure Validation (Author-Specified, CAJAL-Validated)

| # | Figure | Type | Priority | Components | Exclusion list present | Validates |
|---|---|---|---|---|---|---|
| 10.1 | MVC responsibility map | Systems diagram | Critical | 7 | ✓ | ✓ |
| 10.2 | Scene graph tree | Hierarchy / taxonomy | Important | 8 | ✓ | ✓ |
| 10.3 | Three-layer stack with controller seam | Hierarchy / layered stack | Critical | 6 | ✓ | ✓ |

Fig 10.2 at 8 components (Stage, Scene, BorderPane + 3 BorderPane children + 2 TableColumn children + 2 Label children) is at the absolute upper limit — but the hierarchy is deliberately the minimal real-application example the chapter uses. CAJAL accepts.

---

## Video Candidate Pass

**FIGURE 10.1 (MVC responsibility map):** STATIC SUFFICIENT — borderline. The bidirectional state/method-call flow could be animated, but MVC is a discipline students must internalize as a static structural commitment, not a dynamic dance.

**Others:** STATIC SUFFICIENT.

**Video candidates identified: 0.**

---

## Split-point note

The chapter's FXML code listings are typography. The Scene Builder UI screenshots (if any) are picture research / screen captures, not CAJAL figures.

---

## CAJAL discipline checks

- Component counts: within 6–8 limit (Fig 10.2 at upper limit, justified by the minimum-viable scene-graph example) ✓
- Exclusion lists: present and specific ✓
- Figure types match: systems diagram (correct for MVC with bidirectional flows), hierarchy (correct for scene-graph tree), layered stack (correct for view/controller/model separation) ✓
