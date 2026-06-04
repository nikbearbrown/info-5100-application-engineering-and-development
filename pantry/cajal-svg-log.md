# CAJAL SVG Generation Log

## Run: 2026-05-25T16:24Z — pilot

### 01-fundamentals-of-programming-in-java-cajal.md

- figures found: 3
- SVGs generated: 3
- skipped (existing): 0

| File | Figure title | Type | Status |
|---|---|---|---|
| 01-fundamentals-of-programming-in-java-fig-01.svg | Procedural vs Object Model: Where Behavior Lives | Comparison panels | generated |
| 01-fundamentals-of-programming-in-java-fig-02.svg | Three Kinds of Wrong | Comparison panels (horizontal spectrum) | generated |
| 01-fundamentals-of-programming-in-java-fig-03.svg | The Verification Loop | Cycle diagram | generated |

### Notes — pilot run

Translated CAJAL's Okabe-Ito palette to Brutalist:

- Sky Blue / Bluish Green / Vermillion data-encoding → neutral ink (#2a1a0e) + light gray fills (#F5F5F5, #EAEAEA, #C8C8C8) where progressive encoding required.
- Red (#C8102E) reserved for the figure's single primary highlight: Fig 1.1 → Patron object boundary; Fig 1.3 → VERIFY label at the loop's center.
- Fig 1.2 deliberately uses no red — would have collided with the "do not encode danger with red" rule.

User flagged that a visible "SOURCE — CAJAL FIG 1.1" footer line was rendered in Fig 1.1. Removed and regenerated. The `<metadata>` XML block and HTML comment header are non-rendering (correct per SVG spec). No CAJAL identifier appears as visible text in any generated SVG.

---

## Run: 2026-05-25T16:50Z — full run

After pilot sign-off, processed remaining 19 cajal files (skipping density-0 files: 00-frontmatter, 97-fundamental-themes, 99-back-matter).

### 00-introduction-cajal.md
- figures found: 1, SVGs generated: 1, skipped: 0

| File | Figure title | Type | Status |
|---|---|---|---|
| 00-introduction-fig-01.svg | Book Map: Themes Across Modules | Systems diagram (grid) | generated |

### 00-welcome-cajal.md
- figures found: 5, SVGs generated: 5, skipped: 0

| File | Figure title | Type | Status |
|---|---|---|---|
| 00-welcome-fig-01.svg | JDK vs JRE Containment | Structural schematic | generated |
| 00-welcome-fig-02.svg | Java Toolchain Pipeline | Process flowchart | generated |
| 00-welcome-fig-03.svg | Belief-Based vs Evidence-Based Verification | Comparison panels | generated |
| 00-welcome-fig-04.svg | NetBeans Project Folder Tree | Hierarchy | generated |
| 00-welcome-fig-05.svg | Three-Layer Diagnostic Model | Structural schematic | generated |

### 02-methods-arrays-and-file-objects-cajal.md
- figures found: 5, SVGs generated: 5, skipped: 0

| File | Figure title | Type | Status |
|---|---|---|---|
| 02-methods-arrays-and-file-objects-fig-01.svg | Reference Variable Points to Heap Object | Structural schematic | generated |
| 02-methods-arrays-and-file-objects-fig-02.svg | Two Independent Objects | Structural schematic | generated |
| 02-methods-arrays-and-file-objects-fig-03.svg | Shared-Reference Trap | Structural schematic | generated |
| 02-methods-arrays-and-file-objects-fig-04.svg | Trace Before You Run | Comparison panels | generated |
| 02-methods-arrays-and-file-objects-fig-05.svg | AI Boundary Flowchart | Process flowchart | generated |

### 03-objects-and-classes-cajal.md
- figures found: 3, SVGs generated: 3, skipped: 0

| File | Figure title | Type | Status |
|---|---|---|---|
| 03-objects-and-classes-fig-01.svg | Screen-Centric vs State-Centric Mental Model | Comparison panels | generated |
| 03-objects-and-classes-fig-02.svg | CardLayout Container Structure | Structural schematic | generated |
| 03-objects-and-classes-fig-03.svg | Three-Layer Responsibility Model | Hierarchy | generated |

### 04-basics-of-object-oriented-programming-part-2-cajal.md
- figures found: 2 (cajal dropped duplicate Fig 4.3), SVGs generated: 2, skipped: 0

| File | Figure title | Type | Status |
|---|---|---|---|
| 04-basics-of-object-oriented-programming-part-2-fig-01.svg | Symptom / Proximate / Root Diagnostic Hierarchy | Hierarchy | generated |
| 04-basics-of-object-oriented-programming-part-2-fig-02.svg | Hypothesize, Isolate, Test — the Debugging Loop | Cycle diagram | generated |

### 05-inheritance-and-polymorphism-cajal.md
- figures found: 5 (cajal dropped draft Fig 5.1 as a table), SVGs generated: 5, skipped: 0

| File | Figure title | Type | Status |
|---|---|---|---|
| 05-inheritance-and-polymorphism-fig-01.svg | Supply-Coupled vs Preloaded Construction | Comparison panels | generated |
| 05-inheritance-and-polymorphism-fig-02.svg | Catalog Class Boundary | Structural schematic | generated |
| 05-inheritance-and-polymorphism-fig-03.svg | Author Shared Across Books | Structural schematic | generated |
| 05-inheritance-and-polymorphism-fig-04.svg | Annotated main() with Supply / Demand Divider | Annotated example | generated |
| 05-inheritance-and-polymorphism-fig-05.svg | AI Three-Stage Workflow | Process flowchart | generated |

### 06-basics-of-gui-programming-in-java-cajal.md
- figures found: 4, SVGs generated: 4, skipped: 0

| File | Figure title | Type | Status |
|---|---|---|---|
| 06-basics-of-gui-programming-in-java-fig-01.svg | Conflated vs Separated Credential Design | Comparison panels | generated |
| 06-basics-of-gui-programming-in-java-fig-02.svg | Hash Function Mechanism | Process flowchart | generated |
| 06-basics-of-gui-programming-in-java-fig-03.svg | Login Flow Sequence | Systems diagram (sequence) | generated |
| 06-basics-of-gui-programming-in-java-fig-04.svg | Attacker Reads: Plaintext vs Hashed Storage | Comparison panels | generated |

### 07-midterm-exam-cajal.md
- figures found: 3, SVGs generated: 3, skipped: 0

| File | Figure title | Type | Status |
|---|---|---|---|
| 07-midterm-exam-fig-01.svg | Dynamic Dispatch | Systems diagram | generated |
| 07-midterm-exam-fig-02.svg | Change-Cost Trajectory: Polymorphic vs If-Else | Statistical / quantitative (line chart) | generated |
| 07-midterm-exam-fig-03.svg | If-Else vs Polymorphic — Before and After | Comparison panels | generated |

### 08-abstract-classes-and-interfaces-cajal.md
- figures found: 4 (cajal dropped Fig 8.1 as a table), SVGs generated: 4, skipped: 0

| File | Figure title | Type | Status |
|---|---|---|---|
| 08-abstract-classes-and-interfaces-fig-01.svg | Write Path vs Read Path with Failure Points | Process flowchart (paired) | generated |
| 08-abstract-classes-and-interfaces-fig-02.svg | Object → File → Object Lifecycle | Process flowchart | generated |
| 08-abstract-classes-and-interfaces-fig-03.svg | Memory vs File Timeline — the Data-Loss Window | Timeline | generated |
| 08-abstract-classes-and-interfaces-fig-04.svg | Three-Question Persistence Design Form | Annotated example | generated |

### 09-event-driven-programming-cajal.md
- figures found: 2, SVGs generated: 2, skipped: 0

| File | Figure title | Type | Status |
|---|---|---|---|
| 09-event-driven-programming-fig-01.svg | Comparator: Inline Tangle vs Named Object | Comparison panels | generated |
| 09-event-driven-programming-fig-02.svg | Stream Pipeline with Persistent Source | Process flowchart | generated |

### 10-event-driven-programming-with-scene-builder-cajal.md
- figures found: 3, SVGs generated: 3, skipped: 0

| File | Figure title | Type | Status |
|---|---|---|---|
| 10-event-driven-programming-with-scene-builder-fig-01.svg | MVC Responsibility Map | Systems diagram | generated |
| 10-event-driven-programming-with-scene-builder-fig-02.svg | Scene Graph Tree | Hierarchy | generated |
| 10-event-driven-programming-with-scene-builder-fig-03.svg | Three-Layer Stack with Controller Seam | Hierarchy | generated |

### 11-generics-cajal.md
- figures found: 6, SVGs generated: 6, skipped: 0

| File | Figure title | Type | Status |
|---|---|---|---|
| 11-generics-fig-01.svg | Event Structure with Three Registration Forms | Annotated example | generated |
| 11-generics-fig-02.svg | Handler Responsibility Decomposition | Systems diagram | generated |
| 11-generics-fig-03.svg | Closet Handler vs Clean Handler | Annotated example (paired) | generated |
| 11-generics-fig-04.svg | Click-to-View Chain with Bug Locations | Process flowchart | generated |
| 11-generics-fig-05.svg | Before and After a Deadline Refactor | Comparison panels | generated |
| 11-generics-fig-06.svg | AI Scaffolds. You Fill Bodies. | Comparison panels | generated |

### 12-recursion-cajal.md
- figures found: 4, SVGs generated: 4, skipped: 0

| File | Figure title | Type | Status |
|---|---|---|---|
| 12-recursion-fig-01.svg | Java Code vs FXML — Two Representations of the Same View | Comparison panels | generated |
| 12-recursion-fig-02.svg | FXMLLoader Injection — Match vs Mismatch | Process flowchart (paired) | generated |
| 12-recursion-fig-03.svg | Controller Lifecycle — Four Phases | Timeline | generated |
| 12-recursion-fig-04.svg | Traceability Chain — Intact vs Broken | Comparison panels | generated |

### 13-collections-and-iterators-cajal.md
- figures found: 2 (cajal dropped Fig 13.1 as a table), SVGs generated: 2, skipped: 0

| File | Figure title | Type | Status |
|---|---|---|---|
| 13-collections-and-iterators-fig-01.svg | Regression Timeline — Tests Catch What People Miss | Timeline | generated |
| 13-collections-and-iterators-fig-02.svg | Test Anatomy — Setup, Execution, Assertion | Annotated example | generated |

### 14-lists-stacks-queues-and-the-final-project-cajal.md
- figures found: 4 (cajal dropped Fig 14.2 as a table), SVGs generated: 4, skipped: 0

| File | Figure title | Type | Status |
|---|---|---|---|
| 14-lists-stacks-queues-and-the-final-project-fig-01.svg | Five-Layer Project Architecture | Hierarchy | generated |
| 14-lists-stacks-queues-and-the-final-project-fig-02.svg | AI Audit Form | Annotated example | generated |
| 14-lists-stacks-queues-and-the-final-project-fig-03.svg | Impression vs Evidence | Comparison panels | generated |
| 14-lists-stacks-queues-and-the-final-project-fig-04.svg | Course-Capability Arc — Before and After | Comparison panels | generated |

### 95-claude-code-cajal.md
- figures found: 1, SVGs generated: 1 (replaced older off-style file), skipped: 0

| File | Figure title | Type | Status |
|---|---|---|---|
| 95-claude-code-fig-01.svg | Phase-Gate Ladder — AI Permission Across the Semester | Hierarchy / progression | generated |

### Skipped — density 0

- `00-frontmatter-cajal.md` — declined
- `97-fundamental-themes-cajal.md` — declined
- `99-back-matter-cajal.md` — declined

---

## Summary

Total cajal.md files processed: 20 / 20 (17 yielded figures, 3 declined at density 0)
Total figures parsed: 57
Total SVGs generated: 57
Total skipped (already exist): 0
PNG conversion: run completed — 57 PNGs at 300 DPI in `images/`

### Translation pattern (book-to-book reusable)

- CAJAL files use the Okabe-Ito semantic palette. Brutalist style uses a single red accent + ink + neutrals. Translation rule:
  - The CAJAL figure's *single most pedagogically important element* gets red (#C8102E). Everything else is ink (#2a1a0e), light gray fill (#F5F5F5), or border gray (#D4D4D4).
  - Where CAJAL uses red-for-disruptive or red-for-danger semantics, replace with neutral encoding (progressive grays, dashed strokes, structural breaks). The "no red for danger" rule overrides cajal semantics.
  - Where CAJAL specifies multiple distinct data colors, fold to ≤2 data-encoding hues, using direct labels for the rest.
- Three font roles are honored uniformly: EB Garamond for figure title and body callouts; Inter for axis/captions/labels; JetBrains Mono for code identifiers, file paths, and axis numerics.
- Variable-thickness arrows implemented as tapered polygons. Cycle arrows as quadratic Bézier curves.
- Every SVG: HTML comment header + `<metadata><cajal:figure …/></metadata>` block + `role="img"` + `<title>` + `<desc>` + `<defs><marker id="arrow"/></defs>` (where arrows used). **No CAJAL identifiers ever render as visible text.**
- Where the cajal file points to inline `[SCOPE | ...]` markers in the chapter source rather than carrying full SCOPE blocks itself, I inferred figure structure from the cajal validation tables + zone maps + figure titles. Component counts were respected within the 6–8 limit; where a figure's CAJAL component count exceeded 8, it was collapsed (Fig 14.5 → 3+3 buckets) rather than split, per the cajal author's editorial intent.
