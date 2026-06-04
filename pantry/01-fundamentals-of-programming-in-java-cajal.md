# CAJAL Figure Intelligence — Module 1: Fundamentals of Programming in Java

**Source:** `chapters/01-fundamentals-of-programming-in-java.md`
**Mode:** `/scan silent`
**Domain note:** CS textbook. CAJAL's natural domain. Author has pre-specified figures via inline `[SCOPE | ...]` markers AND an end-of-chapter CAJAL SCOPE OUTPUTS section. CAJAL validates and applies the discipline.

The chapter pre-specifies three figures (Fig 1.1 procedural vs. object model, Fig 1.2 three kinds of wrong, Fig 1.3 verification loop). All three are well-architected with proper exclusion lists. Density check passes.

---

## Density Recommendation

**3 figures, Mechanistic density.** Each does distinct argumentative work — the object-model spatial contrast, the wrong-detectability spectrum, the recurring verification cycle. Author's component counts are within the 6–8 limit. Exclusion lists are populated.

---

## Zone Map

- **MC:** Procedural-to-object model transition. Three-kinds-of-wrong taxonomy with decreasing detectability. Verification loop as recurring craft.
- **VG:** Where behavior lives — the spatial claim about encapsulation that prose alone cannot make visible.
- **PQ:** None.

---

## Figure 1.1 — Procedural vs. Object Model (Where Behavior Lives)

**Priority: Critical.** VG. Author-specified; CAJAL validates.

### Block 1 — Illustrae paste block

Single-column figure, 89mm width, flat vector, white background. Two side-by-side panels separated by a 0.5pt vertical Black `#000000` dividing line. Left panel (procedural model): three rectangular procedure boxes (checkOut, returnBook, getBorrowedCount) Vermillion `#D55E00` filled, arranged vertically, each with a Bluish Green `#009E73` 1pt single-headed arrow pointing rightward to a single shared light gray rectangle representing the patron data store. Right panel (object model): one large Sky Blue `#56B4E9` filled rounded rectangle representing a Patron object boundary, enclosing three internal regions in light gray — a name field, a borrowedBooks list region, and a row of three method indicator regions. No arrows cross the object boundary. White background, flat vector.

### Block 2 — Full SCOPE prompt

[S] Single-column 89mm, vector output, white background.
[C] Left panel: 3 procedure boxes + shared data store with 3 arrows. Right panel: 1 Patron object enclosing name field, borrowedBooks list, and 3 method indicators.
[O] Two equal-width horizontal panels separated by a 0.5pt vertical rule. Left flows top-to-bottom (procedures → data). Right shows spatial containment. No arrows cross the panel boundary.
[P] Procedure boxes Vermillion `#D55E00` filled. Shared data store light gray. Patron object boundary Sky Blue `#56B4E9` filled. Internal regions light gray. Arrows Bluish Green `#009E73` 1pt single-headed. Divider Black `#000000` 0.5pt.
[E] Compiler internals, memory allocation diagrams, UML class diagram notation, inheritance arrows, interface declarations, access modifiers (public/private), garbage collector, JVM internals, constructor syntax, any downstream classes (Book, Library), multiple patron instances, array notation, text labels.

### Block 3 — Negative prompt

text labels, words, gibberish letters, titles, captions, decorative borders, realistic 3D textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion, UML notation, inheritance arrows, dashed access modifier lines, constructor brackets, array syntax, multiple instances, memory address labels

---

## Figure 1.2 — Three Kinds of Wrong

**Priority: Critical.** MC + VG. Author-specified; CAJAL validates.

### Block 1 — Illustrae paste block

Single-column figure, 89mm width, flat vector, white background. Horizontal three-zone spectrum, left to right: zone 1 (compilation error), zone 2 (runtime error), zone 3 (silent wrong behavior). Zones equal width, separated by Black `#000000` 1pt vertical dividers. Bottom: a horizontal Black 1pt arrow spanning all three zones, increasing in stroke weight left to right (thin at left, thick at right) — danger gradient. Top: a horizontal Blue `#0072B2` 1pt arrow spanning all three zones, decreasing in stroke weight left to right — detectability gradient. Zone 1 icon region: Sky Blue `#56B4E9` filled shape. Zone 2 icon region: Orange `#E69F00` filled shape. Zone 3 icon region: Vermillion `#D55E00` filled shape. Zone backgrounds: progressively darker light gray left to right. White outer background, 1pt strokes, no gradients.

### Block 2 — Full SCOPE prompt

[S] Single-column 89mm, vector output, white background.
[C] 3 equal-width horizontal zones. Bottom danger arrow spanning all zones with increasing thickness. Top detectability arrow spanning all zones with decreasing thickness. One icon shape per zone in progressively warmer hues.
[O] Strict left-to-right horizontal layout. Vertical dividers between zones. Two horizontal arrows (top + bottom) spanning the full width.
[P] Zone 1 icon Sky Blue `#56B4E9` filled. Zone 2 icon Orange `#E69F00` filled. Zone 3 icon Vermillion `#D55E00` filled. Zone backgrounds progressive light gray. Danger arrow Black `#000000` 1pt with variable weight. Detectability arrow Blue `#0072B2` 1pt with variable weight.
[E] Specific exception class names (NullPointerException etc.), stack trace formatting, IDE error panels, debugger UI, test framework syntax, assert statements, logging frameworks, code snippets, Java syntax of any kind, specific library checkout example code, patron/book variable names.

### Block 3 — Negative prompt

text labels, words, code text, IDE interface elements, terminal windows, stack traces, gibberish letters, titles, captions, decorative borders, realistic 3D textures, drop shadows, gradient backgrounds, photographic elements, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Figure 1.3 — The Verification Loop

**Priority: Important.** MC. Author-specified; CAJAL validates.

### Block 1 — Illustrae paste block

Single-column figure, 89mm width, flat vector, white background. Three rounded rectangular nodes arranged in an equilateral triangle: top-center (business behavior question), bottom-left (Java artifact question), bottom-right (evidence question). Top node Orange `#E69F00` 1pt outline with 15% opacity fill. Bottom-left node Sky Blue `#56B4E9` 1pt outline with 15% opacity fill. Bottom-right node Bluish Green `#009E73` 1pt outline with 15% opacity fill. Three Bluish Green `#009E73` 1pt single-headed arrows connecting the nodes in a closed clockwise cycle (top → bottom-right → bottom-left → top). Each node has a small icon region inside for post-applied typography (document/code-bracket/checkmark). White background, no gradients, no drop shadows.

### Block 2 — Full SCOPE prompt

[S] Single-column 89mm, vector output, white background.
[C] 3 triangular-arranged rounded-rectangle nodes. 3 clockwise-cycle arrows. Icon regions inside each node.
[O] Equilateral triangle, top node centered. Clockwise arrow routing along the triangle's outside. Equal node spacing.
[P] Top node Orange `#E69F00` outline + 15% fill. Bottom-left Sky Blue `#56B4E9` outline + 15% fill. Bottom-right Bluish Green `#009E73` outline + 15% fill. Arrows Bluish Green 1pt single-headed.
[E] Specific test framework syntax, JUnit annotations, assertion library names, CI/CD pipeline elements, code coverage percentages, UML notation, formal verification symbols, specific library checkout variable names, any Java syntax, multiple verification loops.

### Block 3 — Negative prompt

text labels, words, code syntax, terminal output, test runner UI, UML class notation, gibberish letters, titles, captions, decorative borders, realistic 3D textures, drop shadows, gradient backgrounds, photographic elements, dual-headed arrows, hand-drawn styles, sketch lines, human figures, visual clutter, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video Candidate Pass

All three static sufficient. Structural, categorical, and cyclic — none requires animation to communicate.

**Video candidates identified: 0.**

---

## Split-point note

The chapter's end-of-chapter CAJAL SCOPE OUTPUTS section is the author's pre-build of the same three figures CAJAL has just validated. Use as primary source; this CAJAL output adds the density recommendation, video pass, and priority ranking. The "concept / Java artifact / AI may do / student verifies / evidence" comparison table is typography.
