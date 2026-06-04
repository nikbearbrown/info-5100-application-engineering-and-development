# CAJAL Figure Intelligence — Module 6: Basics of GUI Programming in Java

**Source:** `chapters/06-basics-of-gui-programming-in-java.md`
**Mode:** `/scan silent`
**Domain note:** CS textbook. Author has pre-specified four figures via inline `[SCOPE | ...]` markers. Layout-purpose palette; Okabe-Ito governs.

---

## Density Recommendation

**4 figures, Mechanistic density.** The chapter centers on a real architectural decision (separating credentials from domain objects) and the cryptographic mechanism beneath it. Each of the four figures earns its place: design contrast (6.1), hash function pipeline (6.2), login flow sequence (6.3), attacker-reads comparison (6.4).

---

## Zone Map

- **MC:** Hash function as one-way pipeline; login flow as multi-actor sequence with Patron deliberately absent.
- **VG:** Conflated vs. separated design — the architectural claim the chapter is making.
- **PQ:** Damage-reduction visualization — the attacker-reads comparison uses zone-size contrast to encode bounded vs. unbounded damage. This is quasi-quantitative; the visual encoding is proportional but not strictly chartable.

---

## Figure Validation (Author-Specified, CAJAL-Validated)

| # | Figure | Type | Priority | Components | Exclusion list present | Validates |
|---|---|---|---|---|---|---|
| 6.1 | Conflated vs. separated credential design | Comparison panels | Critical | 7 | ✓ | ✓ |
| 6.2 | Hash function mechanism | Process flowchart | Critical | 6 | ✓ | ✓ |
| 6.3 | Login flow sequence (5 swimlanes) | Systems diagram (sequence) | Critical | 6 | ✓ | ✓ |
| 6.4 | Attacker reads: plaintext vs. hashed | Comparison panels | Important | 6 | ✓ | ✓ |

All four within the 6–8 component limit. Exclusion lists populated. Fig 6.1 at 7 components is at the upper safe boundary — the author has tightened the inclusion list well (Patron fields + UserAccount fields + LoginManager + ID-link arrow stay; Library, Loan, Book, navigation panels, database icons explicitly excluded).

---

## Video Candidate Pass

**FIGURE 6.3 (Login flow sequence):** STATIC SUFFICIENT — borderline. A sequence diagram animated with arrows firing left-to-right and the boolean returning right-to-left would communicate the call-and-return mechanism viscerally. But the static swimlane sequence with numbered arrows is the standard representation that CS students learn to read; the chapter explicitly wants the student to *read* the sequence, not watch it.

**FIGURE 6.2 (Hash function):** STATIC SUFFICIENT — borderline. The "cannot reverse" claim could be animated as an arrow trying to go backward and bouncing off a barrier. Static with a blocked arrow handles it.

**Other two:** STATIC SUFFICIENT.

**Video candidates identified: 0.**

---

## Split-point note

The credential-handling code examples and AI-boundary tables are typography. The attacker-consequences lists inside Fig 6.4 are typography (post-applied annotation), not part of the generated image.

---

## CAJAL discipline checks

- Component counts: within 6–8 limit (Fig 6.1 at the upper boundary, deliberately) ✓
- Exclusion lists: present and well-tuned (especially Fig 6.1's exclusion of unrelated domain classes) ✓
- Figure types match: comparison panels (correct for design contrast and attacker-read contrast), process flowchart (correct for hash pipeline), systems/sequence diagram (correct for multi-actor login flow) ✓
- The chapter handles the security-illustration challenge cleanly: no red-green encoding (uses Vermillion-vs-Blue), no human attacker iconography, no padlock clichés
