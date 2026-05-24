# Research: Chapter 09 — Targeting and Sorting: Working with Collections
## Programming with Java: An Object-Oriented Practicum

**Chapter one-line:** Students learn to sort, filter, and search collections of objects — and to choose the right collection type for each task.
**Research date:** 2026-05-23

---

## 1. Primary Sources

### Foundational papers and texts
- Naftalin, Maurice and Wadler, Philip, Java Generics and Collections, 2006. This is a strong practical source for Java collections, generics, and collection contracts. Use it for collection choice and type-safe examples.
- Cormen, Leiserson, Rivest, and Stein, Introduction to Algorithms, 4th ed., 2022. CLRS supports search, sort, and complexity reasoning. Use only the portions needed for access pattern and performance intuition.
- Gosling, James, Joy, Bill, Steele, Guy, Bracha, Gilad, Buckley, Alex, and Smith, Daniel, The Java Language Specification, Java SE 21 Edition, Oracle, 2023. This is the authoritative language source for Java classes, objects, fields, methods, inheritance, lambdas, and exceptions. Use it to anchor factual claims about Java behavior rather than relying on tutorial simplifications.
- Oracle, Java SE 21 API Specification, 2023. The API docs are the correct source for standard library contracts such as `List`, `Map`, `Set`, `Comparator`, I/O classes, and exception behavior. The chapter drafter should cite API contracts when explaining what a library type promises.
- Horstmann, Cay S., Core Java, Volume I: Fundamentals, 12th ed., 2021. Horstmann provides professional-grade explanations of Java fundamentals that are still accessible to serious beginners. Use it to supplement primary specifications with pedagogically useful examples.
- Bloch, Joshua, Effective Java, 3rd ed., 2018. Bloch helps explain collection APIs, generics, and API design tradeoffs in Java practice.

### Key empirical cases
- Illustrative course lab: 500 books sorted by title, author, and year; students compare naive and comparator-based approaches.
- Collection mismatch case: using `List` for frequent ISBN lookup works at small scale but reveals the wrong access pattern.
- AI-generated search case: code uses linear search without asking expected size. The student must decide if O(n) is acceptable.

---

## 2. The Core Concept — State of the Field

### What is settled
The settled instructional core is that introductory application engineering students need executable mental models, not just syntax exposure. Java's type system, class model, object references, collections, exceptions, GUI APIs, and testing tools are documented in official specifications and API references, while programming-education research shows that students learn these concepts more reliably when they predict, trace, test, and explain code. For this chapter, the author can confidently treat List, Map, Set, Comparator, Comparable, filtering, search, streams intro, access patterns, and AI collection-choice audit as a design-and-verification problem, not only an implementation topic.

### What is disputed
The disputed issues are how early to introduce AI assistance, how much code generation to allow, whether object-oriented design remains the right first paradigm for applied graduate students, and how formal the verification layer should be. The book's position is that AI can be introduced, but only behind explicit phase gates: students must understand enough to inspect, explain, and reject output. Drafters should avoid claiming that AI is either harmless or categorically inappropriate; the point is disciplined delegation.

### What has changed recently (last 5 years)
AI coding assistants have changed the meaning of beginner programming assignments: students can obtain plausible code before they understand it. Java platform content is comparatively stable, but JavaFX setup, IDE workflows, JUnit integration, and AI-tool interfaces are high-aging-risk. Current-source claims about Claude, Copilot, NetBeans, Scene Builder, JavaFX packaging, or academic integrity policy should be rechecked before each offering.

---

## 3. Application Domain Examples

- Library: `List<Book>` for display order, `Map<String, Book>` for ISBN lookup.
- Inventory: `Set<String>` for unique SKUs and `Map<String, Product>` for lookup.
- Scheduling: sort appointment slots by time and filter by provider.

---

## 4. The Book's Thesis Connection

This chapter serves the book's central thesis by making List, Map, Set, Comparator, Comparable, filtering, search, streams intro, access patterns, and AI collection-choice audit part of the student's own verification capacity. The book argues that productive AI-assisted development requires genuine object-oriented understanding because the student cannot safely delegate what they cannot identify, design, or verify.

In the threaded project, this chapter contributes one concrete layer to that capacity. The learner must supply the business meaning, object boundary, failure expectation, user workflow, or verification criterion. AI can help explain, scaffold, or implement only after that human layer exists.

The research literature supports the thesis in a calibrated way. AI coding-assistant studies support the usefulness of generated code and productivity assistance, but usability and security studies show that generated code still requires human review. Programming-education research supports worked examples, tracing, prediction, testing, and reflection as the route from copied code to understanding.

---

## 5. The AI Wayback Machine — Candidate Figures

- **Donald Knuth** — Connection: use this figure to connect List, Map, Set, Comparator, Comparable, filtering, search, streams intro, access patterns, and AI collection-choice audit to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Donald Knuth reviewing a student's INFO 5100 project for List, Map, Set, Comparator, Comparable, filtering, search, streams intro, access patterns, and AI collection-choice audit. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Robert Tarjan** — Connection: use this figure to connect List, Map, Set, Comparator, Comparable, filtering, search, streams intro, access patterns, and AI collection-choice audit to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Robert Tarjan reviewing a student's INFO 5100 project for List, Map, Set, Comparator, Comparable, filtering, search, streams intro, access patterns, and AI collection-choice audit. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Philip Wadler** — Connection: use this figure to connect List, Map, Set, Comparator, Comparable, filtering, search, streams intro, access patterns, and AI collection-choice audit to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Philip Wadler reviewing a student's INFO 5100 project for List, Map, Set, Comparator, Comparable, filtering, search, streams intro, access patterns, and AI collection-choice audit. Ask what evidence proves the student understood the design rather than merely accepted generated code."

Diversity note: computing history candidates skew U.S./Western European and male if the drafter uses only canonical language-design figures. Across the full book, preserve substantive candidates such as Grace Hopper, Adele Goldberg, Jean E. Sammet, Frances E. Allen, Margaret Hamilton, and Barbara Liskov where appropriate, and balance them against domain-specific figures for security, testing, UI, and software process.

---

## 6. Pedagogical Delivery Research

The target reader knows basic programming ideas from Python, R, or a prior scripting context, but does not yet have Java, OO design, debugging discipline, or a reliable way to supervise AI-generated code. Prior knowledge required for this chapter should be stated as capabilities from earlier modules, not as generic "knows programming."

Common misconceptions include "if it compiles, it works," "AI writes better code than I can," "debugging means reading error messages," and "OO is just Java syntax." The strongest delivery sequence is: run or inspect a concrete artifact, predict behavior, introduce vocabulary, work a library example, transfer to inventory/scheduling variants, then ask for an AI Use Disclosure that names what the student verified.

Known teaching failure modes are syntax-first lectures without running examples, letting AI produce complete answers before students can inspect them, and treating the threaded project as a set of disconnected labs. Students who understand the concept can explain the behavior of their own program and identify what evidence would falsify their design. Students who merely memorize can reproduce definitions but cannot debug, adapt, or reject plausible generated code.

---

## 7. Representation and Display Research

A collection-choice matrix should show operation profile, expected size, required invariant, candidate collection, complexity implication, and AI prompt clause.

---

## 8. Open Questions and Research Gaps

- Aging risk: Low for core concepts; medium for stream syntax version and style guidance.
- Verify current JDK, NetBeans, JavaFX, Scene Builder, JUnit, and AI-tool instructions before each offering.
- Replace illustrative course-lab cases with documented student artifacts after the course has run, with permission and anonymization.
- Confirm whether the EDGE/Coursera gradebook, AI Use Disclosure form, and CLAUDE.md format match the final course deployment.
- Avoid overclaiming: compilation, passing tests, and AI fluency are evidence, but none alone proves the application satisfies requirements.

---

## 9. Sourcing Notes

Use official Java, OpenJFX, NetBeans, Scene Builder, and JUnit documentation for tool and API claims. Use Java books and OO design texts for durable conceptual explanation. Use AI coding-assistant research only for claims about observed assistance, usability, or risk; do not cite vendor marketing as evidence. Many sources are books or standards and may require library access for page-level citations.