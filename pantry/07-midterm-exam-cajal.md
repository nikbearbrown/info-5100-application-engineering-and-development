# CAJAL Figure Intelligence — Module 7: Midterm Exam

**Source:** `chapters/07-midterm-exam.md`
**Mode:** `/scan silent`
**Domain note:** CS textbook. Author has pre-specified three figures via inline `[SCOPE | ...]` markers. Module 7 is the midterm exam module — a consolidation/review chapter rather than a new-concept introduction, so the figures earn their place by clarifying the OOP-vs-procedural turn the midterm is testing.

---

## Density Recommendation

**3 figures, Mechanistic density.** Dynamic dispatch mechanism (7.1), polymorphic-vs-if-else change cost trajectory (7.2), polymorphic-vs-if-else before/after structural contrast (7.3). The three together are the midterm's central conceptual move — *polymorphism is not a Java feature, it is an architectural decision with measurable maintenance consequences*.

---

## Zone Map

- **MC:** Dynamic dispatch — the JVM's runtime selection mechanism that prose can name but only a figure can spatially show.
- **VG:** Polymorphic vs. if-else design — the architectural contrast that motivates the whole inheritance/polymorphism module's payoff.
- **PQ:** Change-cost trajectory — Fig 7.2 is a genuine quantitative chart (places-to-change vs. number-of-types), exactly the chart format CAJAL design rules specify (line chart with y-axis at zero, two clearly differentiated series).

---

## Figure Validation (Author-Specified, CAJAL-Validated)

| # | Figure | Type | Priority | Components | Exclusion list present | Validates |
|---|---|---|---|---|---|---|
| 7.1 | Dynamic dispatch | Systems diagram | Critical | 6 | ✓ | ✓ |
| 7.2 | Change-cost trajectory (line chart) | Statistical / quantitative | Critical | 4 | ✓ | ✓ |
| 7.3 | If-else vs. polymorphic before/after | Comparison panels | Critical | 7 | ✓ | ✓ |

Fig 7.2 is the chapter's PQ figure and respects CAJAL discipline: y-axis at zero, two series clearly distinguishable (solid vs. dashed), no 3D distortion, no chart junk.

---

## Video Candidate Pass

**FIGURE 7.1 (Dynamic dispatch):** STATIC SUFFICIENT — borderline. The runtime-decision claim could be animated with the JVM "selecting" an arrow path based on the actual-type object that arrives. But CS students need to *read* the dispatch table mentally, which static representation supports better than ephemeral animation.

**FIGURE 7.2 (Change-cost line chart):** STATIC SUFFICIENT. Line charts are inherently static.

**FIGURE 7.3 (Before/after):** STATIC SUFFICIENT.

**Video candidates identified: 0.**

---

## Split-point note

The chapter's review-question tables and code listings are typography. The midterm rubric is administrative content, not a CAJAL figure.

---

## CAJAL discipline checks

- Component counts: within 6–8 limit (Fig 7.3 at upper boundary with seven components: 3 if-else branches + 1 polymorphic call + 3 subclass boxes; tight) ✓
- Exclusion lists: present and specific ✓
- Figure types match: systems diagram (correct for dispatch mechanism with multiple call paths), line chart (correct for cost-vs-N quantitative claim), comparison panels (correct for before/after architectural shift) ✓
- Y-axis at zero in Fig 7.2 ✓
- No 3D / no shadows / no gradient backgrounds in the chart ✓
