# Worked Exercises Generation Report

**Book:** INFO 5100 Application Engineering and Development
**Date:** 2026-06-04
**Chapters processed:** 16
**Files written:** 16
**Output directory:** `worked-problems/`

| Chapter | File | Parts generated | Notes |
|---|---|---|---|
| Module 0: Welcome | 00-welcome-worked-exercises.md | A B C D E F | Skill = environment verification / setup-vs-code diagnosis |
| Ch 01: Fundamentals of Programming in Java | 01-…-worked-exercises.md | A B C D E F | |
| Ch 02: Methods, Arrays, and File Objects | 02-…-worked-exercises.md | A B C D E F | reference-vs-object model |
| Ch 03: Objects and Classes | 03-…-worked-exercises.md | A B C D E F | |
| Ch 04: Basics of OOP, Part 2 | 04-…-worked-exercises.md | A B C D E F | body teaches debugging (see mismatch note) |
| Ch 05: Inheritance and Polymorphism | 05-…-worked-exercises.md | A B C D E F | body teaches supply-side modeling (see note) |
| Ch 06: Basics of GUI Programming in Java | 06-…-worked-exercises.md | A B C D E F | body teaches authentication (see note) |
| Ch 08: Abstract Classes and Interfaces | 08-…-worked-exercises.md | A B C D E F | body teaches CSV persistence/CRUD (see note) |
| Ch 09: Event-Driven Programming | 09-…-worked-exercises.md | A B C D E F | body teaches Collections (see note) |
| Ch 10: Event-Driven Programming with Scene Builder | 10-…-worked-exercises.md | A B C D E F | |
| Ch 11: Generics | 11-…-worked-exercises.md | A B C D E F | body teaches event-driven (see note) |
| Ch 12: Recursion | 12-…-worked-exercises.md | A B C D E F | body teaches FXML/Scene Builder (see note) |
| Ch 13: Collections and Iterators | 13-…-worked-exercises.md | A B C D E F | |
| Ch 14: Lists, Stacks, Queues & Final Project | 14-…-worked-exercises.md | A B C D E F | |
| Appendix: Claude Code for Java | 95-claude-code-worked-exercises.md | A B C D E F | skill = verifying AI-generated code |
| Appendix: Fundamental Themes | 97-fundamental-themes-worked-exercises.md | A B C | Bridge chapter (synthesis, no anchor) |

**Excluded (per rule):** `00-frontmatter.md`, `99-back-matter.md`, `07-midterm-exam.md` (contains "exam").
**Skipped (judgment):** `00-introduction.md` — generic orientation with no teachable problem-solving concept; worked exercises would have been generic, which the rules forbid.

---

## ⚠ Finding requiring author decision — title/body mismatch in the source chapters

Two independent generators flagged, and I confirmed, that several source chapters have a **title that does not match the topic their prose actually teaches** — and the bodies appear to be shifted relative to their titles:

| Source file / declared title | What the prose (first content section) actually teaches |
|---|---|
| Module 05 — *Inheritance and Polymorphism* | "Two Kinds of Objects" — supply-side entity/relationship modeling |
| Module 06 — *Basics of GUI Programming* | "The Person Is Not the Account" — authentication & hashing |
| Module 08 — *Abstract Classes and Interfaces* | "What CRUD Actually Means" — CSV persistence / CRUD |
| Module 09 — *Event-Driven Programming* | "What Collections Are Actually Doing" — Collections |
| Module 11 — *Generics* | "How Event-Driven Programs Actually Work" — event-driven |
| Module 12 — *Recursion* | "What FXML Is" — Scene Builder / FXML |

This is a content-management defect in the source book (the chapter bodies look misfiled relative to their titles/EDGE outlines), independent of this exercise pass.

**Consequence for these files (an inconsistency to resolve):** because the prompt said to ground exercises in "each chapter's actual concepts, vocabulary, named examples," the two generators handling the affected chapters made different defensible calls:

- **Chapters 04–08** were generated to match the **prose/body** content (debugging, supply-side modeling, authentication, persistence). The canonical OOP topics in the titles (real inheritance/polymorphism, JavaFX widgets, abstract classes) are **not present** in those bodies to draw from.
- **Chapters 09–12** were generated to match the **declared titles** (event-driven, generics, recursion), using the title-keyed misconceptions, with the body's actual topic exercised in the Part F interleave.

**Recommended next step:** decide whether the **titles** or the **bodies** are authoritative for this book, fix the source mismatch at the chapter level, then re-run this pass (it safely overwrites). Until then, the affected files are internally sound and well-grounded, but they target different topics than their filenames imply for the chapters listed above.

The remaining files (00, 01, 02, 03, 10, 13, 14, 95, 97) had no title/body mismatch and are grounded directly in their chapters as written.
