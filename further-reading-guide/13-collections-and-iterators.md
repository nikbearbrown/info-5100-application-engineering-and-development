# Module 13 — Collections and Iterators: Further Reading

> **Content note:** Despite its title, this module's primary content covers JUnit testing, assertion-based requirement specification, boundary-case taxonomy, regression testing, and lambda/stream operations. The Java Collections Framework appears in the learning objectives and key terms but the chapter's teaching focus is on making behavioral claims executable through tests. This guide reflects the actual content.

This chapter teaches you to state requirements as executable assertions — but it stops at the unit-test boundary and does not show you how to apply that discipline at scale, how to design test suites systematically, or how the test-first (TDD) mindset changes the way you write production code. These resources close those gaps: the Key resource gives you the JUnit 5 mechanics the chapter uses but does not fully document; the Recommended resources extend the boundary-case taxonomy into professional test design and connect testing discipline to the TDD workflow the bridge question is pointing toward; the Further resource shows where the theoretical foundation for the "tests as executable specifications" argument comes from.

Read the Key resource before attempting Exercise 4 (the five-case test suite for your project's search method) — it documents the specific JUnit 5 annotations and assertion methods the exercise requires. Choose one Recommended resource based on what felt least resolved: pick the first if you want structured guidance on designing test cases beyond the five-case taxonomy, pick the second if you want to see how writing tests before code changes the way requirements are made explicit. The Further item is for students who want the theoretical underpinning of specification-based testing; it is not required, and most students should save it until after they have written at least one failing test from the exercises.

---

### Key

**JUnit 5 User Guide** — The JUnit Team, 2024 (junit.org/junit5)

I included this because the chapter uses `@Test`, `assertEquals`, `assertThrows`, and the setup/execution/assertion structure throughout — but it does not document the full annotation set or explain how to configure JUnit 5 in a project. The JUnit 5 User Guide covers exactly what the exercises require: Section 2.3 ("Annotations") documents `@Test`, `@BeforeEach`, and `@DisplayName` with working examples; Section 2.4 ("Assertions") documents `assertEquals`, `assertTrue`, `assertNull`, `assertThrows`, and the overloads that include failure messages. Read Sections 2.3 and 2.4 (approximately 20–30 minutes) before attempting Exercise 4 — specifically the `assertThrows` documentation, which the null-input test case in Exercise 4 may require. Use it as a reference while writing your test suite rather than reading it linearly; when an assertion method behaves differently than expected, the User Guide is the authoritative source. Available free at [https://junit.org/junit5/docs/current/user-guide/](https://junit.org/junit5/docs/current/user-guide/).

---

### Recommended

**Pragmatic Unit Testing in Java 8 with JUnit** — Andy Hunt and Dave Thomas (series editors), Jeff Langr, 2015 (Pragmatic Bookshelf)

I included this because the chapter gives you a five-case taxonomy (normal, empty, no-match, boundary, invalid input) but does not give you a systematic method for generating all the cases a method needs. Langr's "CORRECT" boundary mnemonic (Chapter 7, "Boundary Conditions," pages 91–112) extends the chapter's boundary concept into a checklist — Conformance, Ordering, Range, Reference, Existence, Cardinality, Time — that applies to any method and maps directly onto the five-case taxonomy you have already learned. Read Chapter 7 before Exercise 8 (the feature-extension exercise for search-on-author), where generating the boundary cases for a new requirement is exactly the task. The chapter's "boundary" key term and the CORRECT mnemonic cover the same concept at different levels of resolution; reading both will let you apply the concept to methods you have not seen before. Available through Pragmatic Bookshelf, O'Reilly Learning, and most university libraries.

**Test-Driven Development: By Example** — Kent Beck, 2002 (Addison-Wesley)

This book is the source of the test-first discipline the chapter's AI boundary section is implicitly defending — the principle that you write the assertion before you write the implementation, so that the requirement is explicit before any inference about it is made. Part I ("The Money Example," Chapters 1–17, pages 1–95) demonstrates the complete TDD cycle — red, green, refactor — on a worked domain example, showing how writing the test first forces requirement precision that writing the test after implementation systematically avoids. Read Chapters 1–3 (approximately 40 pages) after completing Exercises 4 and 5 in this module; the TDD cycle will map onto what you experienced when a test initially failed and revealed an implementation assumption. Beck's book is the reason Exercise 4 requires at least one initially failing test, and reading it makes that requirement's pedagogy visible. Available widely in print and through O'Reilly Learning; the 2002 edition remains the standard reference.

---

### Further

**"A Theory of Testing"** — Glenford Myers, Corey Sandler, and Tom Badgett, in *The Art of Software Testing, Third Edition*, Chapter 2, pages 13–38 (Wiley, 2011)

This is a specialist resource that assumes familiarity with software testing as a practice and comfort with slightly formal definitions; plan for 45–60 minutes and note which definitions revise assumptions you already had. The prerequisite is that you have written at least a five-case test suite (Exercise 4) and experienced the difference between a passing test and proof of correctness — the payoff is a principled account of why that gap is irreducible, not a practical limitation. Myers et al. define "testing" as the process of executing a program with the intent of finding errors (not confirming correctness), formalize the concept of a test case as a claim about a specific input-output relationship, and derive the limits of testing from the combinatorial impossibility of exhaustive coverage. What the Recommended tier gives you is technique; what this chapter gives you is the theoretical argument for why the chapter's central claim — "a test is a claim, not a proof" — is not a caveat but the fundamental nature of the activity. This resource is particularly valuable before attempting Exercise 9 (the bridge question about unit testing versus system correctness), where you are asked to reason about the limits of the test suite you have built. Available through Wiley Online Library with institutional access; also held by most university libraries in print.

---

> **Assessment connection:** The Key resource (JUnit 5 User Guide, Sections 2.3 and 2.4) directly supports Exercise 4 — the Optional Exercise: Collections and Iterators assessment that requires writing a five-case test suite for your project's search method, including at least one use of `assertThrows` for the null-input case and `assertEquals` with specific size assertions for the multi-result case.
