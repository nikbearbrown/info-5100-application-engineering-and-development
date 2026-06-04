# CAJAL Figure Intelligence — Module 9: Event-Driven Programming

**Source:** `chapters/09-event-driven-programming.md`
**Mode:** `/scan silent`
**Domain note:** CS textbook. Author has pre-specified two figures via inline `[SCOPE | ...]` markers.

---

## Density Recommendation

**2 figures, Foundational density.** Comparator-as-named-object vs. inline-tangle (9.1) and the stream pipeline with persistent source (9.2). Two well-architected figures carry the chapter's central claims about behavior-as-object and immutable-pipeline semantics.

---

## Zone Map

- **MC:** Stream pipeline — source flows through transformation stages, source unchanged. The functional-style mechanism this chapter introduces.
- **VG:** Comparator-as-named-object — the architectural shift from inline comparisons (no name, no reuse) to named rule-objects that can be swapped.
- **PQ:** None.

---

## Figure Validation (Author-Specified, CAJAL-Validated)

| # | Figure | Type | Priority | Components | Exclusion list present | Validates |
|---|---|---|---|---|---|---|
| 9.1 | Comparator: tangled inline vs. named object | Comparison panels | Critical | 6 | ✓ | ✓ |
| 9.2 | Stream pipeline with persistent source | Process flowchart | Critical | 7 | ✓ | ✓ |

Fig 9.2 at 7 components (source, 3 stages, result, persistent-source, untouched indicator) is within the upper safe boundary.

---

## Video Candidate Pass

**FIGURE 9.2 (Stream pipeline):** **VIDEO CANDIDATE.** Criterion 1 (transition mechanism is the learning target) — students consistently misunderstand that the source collection is unmodified; an animated pipeline showing elements flowing through stages while the source-below-the-pipeline stays still would communicate immutability viscerally. Suggested format: looping animation with element shapes propagating left-to-right through filter/sorted/collect while the source-below tracks pulse to confirm it is not consumed.

**FIGURE 9.1 (Comparator):** STATIC SUFFICIENT.

**Video candidates identified: 1.** Recommended: **Fig 9.2** — the immutability claim is exactly the kind of mechanism static representation has to encode through indicator shapes; motion communicates it directly.

---

## Split-point note

The chapter's lambda / anonymous class / named class comparison is typography. Code listings are typography.

---

## CAJAL discipline checks

- Component counts: within 6–8 limit ✓
- Exclusion lists: present and specific (especially 9.2's exclusion of "modifies source" iconography) ✓
- Figure types match: comparison panels (correct for inline-vs-named contrast), process flowchart (correct for stream pipeline with side-source) ✓
- One video candidate flagged
