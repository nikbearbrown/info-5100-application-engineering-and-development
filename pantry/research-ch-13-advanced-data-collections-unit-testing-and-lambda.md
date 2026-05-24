# Research: Chapter 13 — Advanced Data: Collections, Unit Testing, and Lambda
## Programming with Java: An Object-Oriented Practicum

**Chapter one-line:** Students learn to write tests for their own code and use Java's advanced collection operations — and discover that untested code is code whose correctness you are guessing at.
**Research date:** 2026-05-23

---

## 1. Primary Sources

### Foundational papers and texts
- JUnit 5 User Guide, current version. This is the primary source for annotations, assertions, lifecycle, and test structure. Verify examples against the course's build setup.
- Beck, Kent, Test-Driven Development: By Example, 2002. Beck provides the pedagogical framing for test-first thinking, even if the course uses a lighter version. Use to explain why tests clarify behavior before implementation.
- Freeman, Steve and Pryce, Nat, Growing Object-Oriented Software, Guided by Tests, 2009. This source connects testing to object design and feedback. Use sparingly for beginner-friendly design implications.
- Gosling, James, Joy, Bill, Steele, Guy, Bracha, Gilad, Buckley, Alex, and Smith, Daniel, The Java Language Specification, Java SE 21 Edition, Oracle, 2023. This is the authoritative language source for Java classes, objects, fields, methods, inheritance, lambdas, and exceptions. Use it to anchor factual claims about Java behavior rather than relying on tutorial simplifications.
- Oracle, Java SE 21 API Specification, 2023. The API docs are the correct source for standard library contracts such as `List`, `Map`, `Set`, `Comparator`, I/O classes, and exception behavior. The chapter drafter should cite API contracts when explaining what a library type promises.
- Horstmann, Cay S., Core Java, Volume I: Fundamentals, 12th ed., 2021. Horstmann provides professional-grade explanations of Java fundamentals that are still accessible to serious beginners. Use it to supplement primary specifications with pedagogically useful examples.
- Peng, Siddharth et al., "The Impact of AI on Developer Productivity: Evidence from GitHub Copilot," arXiv, 2023. The study supports the claim that AI assistance can accelerate programming tasks, while leaving open whether learners can verify outputs safely. Use it to motivate disciplined AI use rather than AI replacement.
- Vaithilingam, Priyan et al., "Expectation vs. Experience: Evaluating the Usability of Code Generation Tools Powered by Large Language Models," CHI Extended Abstracts, 2022. This paper is useful for the gap between plausible generated code and user understanding. It supports the course's requirement that students explain and verify AI-assisted work.
- Pearce, Hammond et al., "Asleep at the Keyboard? Assessing the Security of GitHub Copilot's Code Contributions," IEEE Symposium on Security and Privacy Workshops, 2022. This gives empirical caution that generated code can look plausible while embedding risks. Use it where the book argues that AI output requires human auditing.

### Key empirical cases
- Illustrative course lab: a search method works until a new feature changes matching rules; a regression test would have caught it.
- AI test case gap: AI generates normal-path tests but misses empty catalog, null input, duplicate records, or boundary cases. Students add the missing cases.
- Lambda refactor case: a loop-based filter is rewritten as a stream pipeline; students verify same behavior before accepting the refactor.

---

## 2. The Core Concept — State of the Field

### What is settled
The settled instructional core is that introductory application engineering students need executable mental models, not just syntax exposure. Java's type system, class model, object references, collections, exceptions, GUI APIs, and testing tools are documented in official specifications and API references, while programming-education research shows that students learn these concepts more reliably when they predict, trace, test, and explain code. For this chapter, the author can confidently treat JUnit, assertions, test cases, test limitations, lambdas, streams, method references, and AI-generated test coverage audit as a design-and-verification problem, not only an implementation topic.

### What is disputed
The disputed issues are how early to introduce AI assistance, how much code generation to allow, whether object-oriented design remains the right first paradigm for applied graduate students, and how formal the verification layer should be. The book's position is that AI can be introduced, but only behind explicit phase gates: students must understand enough to inspect, explain, and reject output. Drafters should avoid claiming that AI is either harmless or categorically inappropriate; the point is disciplined delegation.

### What has changed recently (last 5 years)
AI coding assistants have changed the meaning of beginner programming assignments: students can obtain plausible code before they understand it. Java platform content is comparatively stable, but JavaFX setup, IDE workflows, JUnit integration, and AI-tool interfaces are high-aging-risk. Current-source claims about Claude, Copilot, NetBeans, Scene Builder, JavaFX packaging, or academic integrity policy should be rechecked before each offering.

---

## 3. Application Domain Examples

- Library: test search with empty catalog, one result, multiple results, no result, and null input.
- Inventory: test restock and stock decrease boundaries.
- Scheduling: test duplicate appointment prevention and date filtering.

---

## 4. The Book's Thesis Connection

This chapter serves the book's central thesis by making JUnit, assertions, test cases, test limitations, lambdas, streams, method references, and AI-generated test coverage audit part of the student's own verification capacity. The book argues that productive AI-assisted development requires genuine object-oriented understanding because the student cannot safely delegate what they cannot identify, design, or verify.

In the threaded project, this chapter contributes one concrete layer to that capacity. The learner must supply the business meaning, object boundary, failure expectation, user workflow, or verification criterion. AI can help explain, scaffold, or implement only after that human layer exists.

The research literature supports the thesis in a calibrated way. AI coding-assistant studies support the usefulness of generated code and productivity assistance, but usability and security studies show that generated code still requires human review. Programming-education research supports worked examples, tracing, prediction, testing, and reflection as the route from copied code to understanding.

---

## 5. The AI Wayback Machine — Candidate Figures

- **Kent Beck** — Connection: use this figure to connect JUnit, assertions, test cases, test limitations, lambdas, streams, method references, and AI-generated test coverage audit to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Kent Beck reviewing a student's INFO 5100 project for JUnit, assertions, test cases, test limitations, lambdas, streams, method references, and AI-generated test coverage audit. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Michael Feathers** — Connection: use this figure to connect JUnit, assertions, test cases, test limitations, lambdas, streams, method references, and AI-generated test coverage audit to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Michael Feathers reviewing a student's INFO 5100 project for JUnit, assertions, test cases, test limitations, lambdas, streams, method references, and AI-generated test coverage audit. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Frances E. Allen** — Connection: use this figure to connect JUnit, assertions, test cases, test limitations, lambdas, streams, method references, and AI-generated test coverage audit to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Frances E. Allen reviewing a student's INFO 5100 project for JUnit, assertions, test cases, test limitations, lambdas, streams, method references, and AI-generated test coverage audit. Ask what evidence proves the student understood the design rather than merely accepted generated code."

Diversity note: computing history candidates skew U.S./Western European and male if the drafter uses only canonical language-design figures. Across the full book, preserve substantive candidates such as Grace Hopper, Adele Goldberg, Jean E. Sammet, Frances E. Allen, Margaret Hamilton, and Barbara Liskov where appropriate, and balance them against domain-specific figures for security, testing, UI, and software process.

---

## 6. Pedagogical Delivery Research

The target reader knows basic programming ideas from Python, R, or a prior scripting context, but does not yet have Java, OO design, debugging discipline, or a reliable way to supervise AI-generated code. Prior knowledge required for this chapter should be stated as capabilities from earlier modules, not as generic "knows programming."

Common misconceptions include "if it compiles, it works," "AI writes better code than I can," "debugging means reading error messages," and "OO is just Java syntax." The strongest delivery sequence is: run or inspect a concrete artifact, predict behavior, introduce vocabulary, work a library example, transfer to inventory/scheduling variants, then ask for an AI Use Disclosure that names what the student verified.

Known teaching failure modes are syntax-first lectures without running examples, letting AI produce complete answers before students can inspect them, and treating the threaded project as a set of disconnected labs. Students who understand the concept can explain the behavior of their own program and identify what evidence would falsify their design. Students who merely memorize can reproduce definitions but cannot debug, adapt, or reject plausible generated code.

---

## 7. Representation and Display Research

A test coverage matrix should map method behavior to normal, boundary, error, null, and regression cases, with columns for AI-suggested and student-added tests.

---

## 8. Open Questions and Research Gaps

- Aging risk: Medium-high: JUnit versions and IDE integration details must be checked before each offering.
- Verify current JDK, NetBeans, JavaFX, Scene Builder, JUnit, and AI-tool instructions before each offering.
- Replace illustrative course-lab cases with documented student artifacts after the course has run, with permission and anonymization.
- Confirm whether the EDGE/Coursera gradebook, AI Use Disclosure form, and CLAUDE.md format match the final course deployment.
- Avoid overclaiming: compilation, passing tests, and AI fluency are evidence, but none alone proves the application satisfies requirements.

---

## 9. Sourcing Notes

Use official Java, OpenJFX, NetBeans, Scene Builder, and JUnit documentation for tool and API claims. Use Java books and OO design texts for durable conceptual explanation. Use AI coding-assistant research only for claims about observed assistance, usability, or risk; do not cite vendor marketing as evidence. Many sources are books or standards and may require library access for page-level citations.