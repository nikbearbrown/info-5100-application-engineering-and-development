# CAJAL Figure Intelligence — Module 13: Collections and Iterators

**Source:** `chapters/13-collections-and-iterators.md`
**Mode:** `/scan silent`
**Domain note:** CS textbook. Author has pre-specified three figures via inline `[SCOPE | ...]` markers. Despite the chapter's title pointing at Collections/Iterators, the actual figure set is about *testing discipline* — the chapter teaches collections through the lens of test-design.

---

## Density Recommendation

**2 figures, Foundational density.** Five-case test coverage matrix (13.1) is a typography table — author marks it `TABLE`, CAJAL agrees. Drop from figure budget. Regression timeline (13.2) and test anatomy (13.3) earn their place.

**Cut from current draft:** Fig 13.1 (five-case test coverage matrix) — typography. Author's own `[SCOPE | ... TABLE: ...]` tag is the correct designation.

---

## Zone Map

- **MC:** Test anatomy — Setup/Execution/Assertion as three labeled sections with right-side callouts naming what each section does and what a failure there means.
- **VG:** Regression timeline — what tests catch *at the moment regression is introduced* vs. *at the demo*. The visibility-without-tests claim made temporal.
- **PQ:** None.

---

## Figure Validation (Author-Specified, CAJAL-Validated)

| # | Figure | Type | Priority | Components | Exclusion list present | Validates |
|---|---|---|---|---|---|---|
| 13.1 | Five-case test coverage matrix | — (table, not figure) | — | — | — | Drop (typography) |
| 13.2 | Regression timeline (M1–M13) | Timeline / progression | Critical | 6 | ✓ | ✓ |
| 13.3 | Test anatomy (Setup/Execution/Assertion) | Annotated example | Critical | 6 | ✓ | ✓ |

---

## Video Candidate Pass

**FIGURE 13.2 (Regression timeline):** STATIC SUFFICIENT — borderline. The "regression breaks the test the moment it is introduced" claim could be animated with the test line breaking as the M7 marker is reached, but static lets the student inspect the temporal-vs-undetected gap simultaneously.

**FIGURE 13.3 (Test anatomy):** STATIC SUFFICIENT.

**Video candidates identified: 0.**

---

## Split-point note

The five-case test matrix (Fig 13.1) is typography. Code listings are typography. The chapter's actual Collections/Iterator content is taught via prose and code examples — the author has chosen to anchor the figure work in the testing discipline that motivates well-tested collection code.

---

## CAJAL discipline checks

- Component counts: within 6–8 limit ✓
- Exclusion lists: present and specific ✓
- Figure types match: timeline (correct for regression-introduction temporal claim), annotated example (correct for three-section test anatomy) ✓
- One drop recommended: Fig 13.1 is structurally a table
