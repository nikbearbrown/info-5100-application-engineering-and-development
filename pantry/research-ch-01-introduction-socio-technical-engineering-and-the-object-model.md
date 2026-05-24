# Research: Chapter 01 — Introduction: Socio-Technical Engineering and the Object Model
## Programming with Java: An Object-Oriented Practicum

**Chapter one-line:** Students learn why objects — not procedures — are the right mental model for business software, by running and breaking a working application before they write one.
**Research date:** 2026-05-23

---

## 1. Primary Sources

### Foundational papers and texts
- Booch, Grady, Object-Oriented Analysis and Design with Applications, 2nd ed., 1994. Booch provides a durable foundation for treating objects as modeling units with identity, state, and behavior. Use it to frame why business software maps well to objects.
- Rumbaugh, James et al., Object-Oriented Modeling and Design, 1991. This source supports the idea that OO modeling is analysis and design, not merely Java syntax. It helps connect library books, patrons, and checkouts to conceptual models.
- Gosling, James, Joy, Bill, Steele, Guy, Bracha, Gilad, Buckley, Alex, and Smith, Daniel, The Java Language Specification, Java SE 21 Edition, Oracle, 2023. This is the authoritative language source for Java classes, objects, fields, methods, inheritance, lambdas, and exceptions. Use it to anchor factual claims about Java behavior rather than relying on tutorial simplifications.
- Oracle, Java SE 21 API Specification, 2023. The API docs are the correct source for standard library contracts such as `List`, `Map`, `Set`, `Comparator`, I/O classes, and exception behavior. The chapter drafter should cite API contracts when explaining what a library type promises.
- Peng, Siddharth et al., "The Impact of AI on Developer Productivity: Evidence from GitHub Copilot," arXiv, 2023. The study supports the claim that AI assistance can accelerate programming tasks, while leaving open whether learners can verify outputs safely. Use it to motivate disciplined AI use rather than AI replacement.
- Vaithilingam, Priyan et al., "Expectation vs. Experience: Evaluating the Usability of Code Generation Tools Powered by Large Language Models," CHI Extended Abstracts, 2022. This paper is useful for the gap between plausible generated code and user understanding. It supports the course's requirement that students explain and verify AI-assisted work.

### Key empirical cases
- Illustrative course lab: a library checkout program runs but prints the wrong patron for a book. The case is suitable because it distinguishes running code from correct behavior before vocabulary is introduced.
- Real pedagogical pattern: prediction-before-run activities in programming education reveal misconceptions about state and control flow. Use this to support asking students to predict output before execution.
- AI explanation comparison: students ask AI to explain provided code and compare it to their own reading. This case exposes plausible but incomplete explanations rather than treating AI as an answer key.

---

## 2. The Core Concept — State of the Field

### What is settled
The settled instructional core is that introductory application engineering students need executable mental models, not just syntax exposure. Java's type system, class model, object references, collections, exceptions, GUI APIs, and testing tools are documented in official specifications and API references, while programming-education research shows that students learn these concepts more reliably when they predict, trace, test, and explain code. For this chapter, the author can confidently treat object model, business entities, compilation versus runtime behavior, socio-technical requirements, and first AI verification boundary as a design-and-verification problem, not only an implementation topic.

### What is disputed
The disputed issues are how early to introduce AI assistance, how much code generation to allow, whether object-oriented design remains the right first paradigm for applied graduate students, and how formal the verification layer should be. The book's position is that AI can be introduced, but only behind explicit phase gates: students must understand enough to inspect, explain, and reject output. Drafters should avoid claiming that AI is either harmless or categorically inappropriate; the point is disciplined delegation.

### What has changed recently (last 5 years)
AI coding assistants have changed the meaning of beginner programming assignments: students can obtain plausible code before they understand it. Java platform content is comparatively stable, but JavaFX setup, IDE workflows, JUnit integration, and AI-tool interfaces are high-aging-risk. Current-source claims about Claude, Copilot, NetBeans, Scene Builder, JavaFX packaging, or academic integrity policy should be rechecked before each offering.

---

## 3. Application Domain Examples

- Library domain: `Book`, `Patron`, and `CheckoutTransaction` as objects rather than rows or procedures.
- Inventory domain: `Product`, `Supplier`, and `StockMovement` as parallel entities.
- Scheduling domain: `Patient`, `Provider`, and `Appointment` as parallel entities.

---

## 4. The Book's Thesis Connection

This chapter serves the book's central thesis by making object model, business entities, compilation versus runtime behavior, socio-technical requirements, and first AI verification boundary part of the student's own verification capacity. The book argues that productive AI-assisted development requires genuine object-oriented understanding because the student cannot safely delegate what they cannot identify, design, or verify.

In the threaded project, this chapter contributes one concrete layer to that capacity. The learner must supply the business meaning, object boundary, failure expectation, user workflow, or verification criterion. AI can help explain, scaffold, or implement only after that human layer exists.

The research literature supports the thesis in a calibrated way. AI coding-assistant studies support the usefulness of generated code and productivity assistance, but usability and security studies show that generated code still requires human review. Programming-education research supports worked examples, tracing, prediction, testing, and reflection as the route from copied code to understanding.

---

## 5. The AI Wayback Machine — Candidate Figures

- **Ole-Johan Dahl** — Connection: use this figure to connect object model, business entities, compilation versus runtime behavior, socio-technical requirements, and first AI verification boundary to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Ole-Johan Dahl reviewing a student's INFO 5100 project for object model, business entities, compilation versus runtime behavior, socio-technical requirements, and first AI verification boundary. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Kristen Nygaard** — Connection: use this figure to connect object model, business entities, compilation versus runtime behavior, socio-technical requirements, and first AI verification boundary to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Kristen Nygaard reviewing a student's INFO 5100 project for object model, business entities, compilation versus runtime behavior, socio-technical requirements, and first AI verification boundary. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Grady Booch** — Connection: use this figure to connect object model, business entities, compilation versus runtime behavior, socio-technical requirements, and first AI verification boundary to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Grady Booch reviewing a student's INFO 5100 project for object model, business entities, compilation versus runtime behavior, socio-technical requirements, and first AI verification boundary. Ask what evidence proves the student understood the design rather than merely accepted generated code."

Diversity note: computing history candidates skew U.S./Western European and male if the drafter uses only canonical language-design figures. Across the full book, preserve substantive candidates such as Grace Hopper, Adele Goldberg, Jean E. Sammet, Frances E. Allen, Margaret Hamilton, and Barbara Liskov where appropriate, and balance them against domain-specific figures for security, testing, UI, and software process.

---

## 6. Pedagogical Delivery Research

The target reader knows basic programming ideas from Python, R, or a prior scripting context, but does not yet have Java, OO design, debugging discipline, or a reliable way to supervise AI-generated code. Prior knowledge required for this chapter should be stated as capabilities from earlier modules, not as generic "knows programming."

Common misconceptions include "if it compiles, it works," "AI writes better code than I can," "debugging means reading error messages," and "OO is just Java syntax." The strongest delivery sequence is: run or inspect a concrete artifact, predict behavior, introduce vocabulary, work a library example, transfer to inventory/scheduling variants, then ask for an AI Use Disclosure that names what the student verified.

Known teaching failure modes are syntax-first lectures without running examples, letting AI produce complete answers before students can inspect them, and treating the threaded project as a set of disconnected labs. Students who understand the concept can explain the behavior of their own program and identify what evidence would falsify their design. Students who merely memorize can reproduce definitions but cannot debug, adapt, or reject plausible generated code.

---

## 7. Representation and Display Research

A comparison table should map procedural representation versus object representation for the same library checkout task: data location, behavior location, failure mode, and AI-safe delegation.

---

## 8. Open Questions and Research Gaps

- Aging risk: Low for OO principles; medium for AI tool examples.
- Verify current JDK, NetBeans, JavaFX, Scene Builder, JUnit, and AI-tool instructions before each offering.
- Replace illustrative course-lab cases with documented student artifacts after the course has run, with permission and anonymization.
- Confirm whether the EDGE/Coursera gradebook, AI Use Disclosure form, and CLAUDE.md format match the final course deployment.
- Avoid overclaiming: compilation, passing tests, and AI fluency are evidence, but none alone proves the application satisfies requirements.

---

## 9. Sourcing Notes

Use official Java, OpenJFX, NetBeans, Scene Builder, and JUnit documentation for tool and API claims. Use Java books and OO design texts for durable conceptual explanation. Use AI coding-assistant research only for claims about observed assistance, usability, or risk; do not cite vendor marketing as evidence. Many sources are books or standards and may require library access for page-level citations.