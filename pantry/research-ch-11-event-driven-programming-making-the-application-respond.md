# Research: Chapter 11 — Event-Driven Programming: Making the Application Respond
## Programming with Java: An Object-Oriented Practicum

**Chapter one-line:** Students learn to connect user actions to application behavior using JavaFX event handling — and to maintain the model-view separation under the pressure of deadline.
**Research date:** 2026-05-23

---

## 1. Primary Sources

### Foundational papers and texts
- OpenJFX Documentation, JavaFX event handling and input events, current version. This is the primary source for event sources, handlers, filters, and JavaFX event classes.
- Gamma, Helm, Johnson, and Vlissides, Design Patterns, 1994. Use only for observer/event-dispatch lineage and responsibility separation; formal patterns are out of scope.
- Harel, David, "Statecharts: A Visual Formalism for Complex Systems," Science of Computer Programming, 1987. Statecharts support representing event-driven behavior as states and transitions when handler code becomes hard to reason about.
- Gosling, James, Joy, Bill, Steele, Guy, Bracha, Gilad, Buckley, Alex, and Smith, Daniel, The Java Language Specification, Java SE 21 Edition, Oracle, 2023. This is the authoritative language source for Java classes, objects, fields, methods, inheritance, lambdas, and exceptions. Use it to anchor factual claims about Java behavior rather than relying on tutorial simplifications.
- Oracle, Java SE 21 API Specification, 2023. The API docs are the correct source for standard library contracts such as `List`, `Map`, `Set`, `Comparator`, I/O classes, and exception behavior. The chapter drafter should cite API contracts when explaining what a library type promises.

### Key empirical cases
- Illustrative course lab: one button handler validates input, mutates model, formats output, updates view, and writes a file. Students count responsibilities and decompose.
- Duplicate event case: a button can be clicked twice before model state updates, producing duplicate transactions. Students add guard conditions.
- AI handler case: AI generates a complete handler body that mixes UI and business logic. Students convert it to separate method calls.

---

## 2. The Core Concept — State of the Field

### What is settled
The settled instructional core is that introductory application engineering students need executable mental models, not just syntax exposure. Java's type system, class model, object references, collections, exceptions, GUI APIs, and testing tools are documented in official specifications and API references, while programming-education research shows that students learn these concepts more reliably when they predict, trace, test, and explain code. For this chapter, the author can confidently treat event loop, event handlers, registration, lambdas, inner classes, responsibility decomposition, and click-to-model-to-view tracing as a design-and-verification problem, not only an implementation topic.

### What is disputed
The disputed issues are how early to introduce AI assistance, how much code generation to allow, whether object-oriented design remains the right first paradigm for applied graduate students, and how formal the verification layer should be. The book's position is that AI can be introduced, but only behind explicit phase gates: students must understand enough to inspect, explain, and reject output. Drafters should avoid claiming that AI is either harmless or categorically inappropriate; the point is disciplined delegation.

### What has changed recently (last 5 years)
AI coding assistants have changed the meaning of beginner programming assignments: students can obtain plausible code before they understand it. Java platform content is comparatively stable, but JavaFX setup, IDE workflows, JUnit integration, and AI-tool interfaces are high-aging-risk. Current-source claims about Claude, Copilot, NetBeans, Scene Builder, JavaFX packaging, or academic integrity policy should be rechecked before each offering.

---

## 3. Application Domain Examples

- Library: checkout button calls validate selection, perform checkout, refresh table, show confirmation.
- Inventory: restock button validates quantity, updates product, records movement, refreshes view.
- Scheduling: book appointment button validates slot, updates appointment, refreshes calendar.

---

## 4. The Book's Thesis Connection

This chapter serves the book's central thesis by making event loop, event handlers, registration, lambdas, inner classes, responsibility decomposition, and click-to-model-to-view tracing part of the student's own verification capacity. The book argues that productive AI-assisted development requires genuine object-oriented understanding because the student cannot safely delegate what they cannot identify, design, or verify.

In the threaded project, this chapter contributes one concrete layer to that capacity. The learner must supply the business meaning, object boundary, failure expectation, user workflow, or verification criterion. AI can help explain, scaffold, or implement only after that human layer exists.

The research literature supports the thesis in a calibrated way. AI coding-assistant studies support the usefulness of generated code and productivity assistance, but usability and security studies show that generated code still requires human review. Programming-education research supports worked examples, tracing, prediction, testing, and reflection as the route from copied code to understanding.

---

## 5. The AI Wayback Machine — Candidate Figures

- **David Harel** — Connection: use this figure to connect event loop, event handlers, registration, lambdas, inner classes, responsibility decomposition, and click-to-model-to-view tracing to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine David Harel reviewing a student's INFO 5100 project for event loop, event handlers, registration, lambdas, inner classes, responsibility decomposition, and click-to-model-to-view tracing. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Douglas Engelbart** — Connection: use this figure to connect event loop, event handlers, registration, lambdas, inner classes, responsibility decomposition, and click-to-model-to-view tracing to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Douglas Engelbart reviewing a student's INFO 5100 project for event loop, event handlers, registration, lambdas, inner classes, responsibility decomposition, and click-to-model-to-view tracing. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Adele Goldberg** — Connection: use this figure to connect event loop, event handlers, registration, lambdas, inner classes, responsibility decomposition, and click-to-model-to-view tracing to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Adele Goldberg reviewing a student's INFO 5100 project for event loop, event handlers, registration, lambdas, inner classes, responsibility decomposition, and click-to-model-to-view tracing. Ask what evidence proves the student understood the design rather than merely accepted generated code."

Diversity note: computing history candidates skew U.S./Western European and male if the drafter uses only canonical language-design figures. Across the full book, preserve substantive candidates such as Grace Hopper, Adele Goldberg, Jean E. Sammet, Frances E. Allen, Margaret Hamilton, and Barbara Liskov where appropriate, and balance them against domain-specific figures for security, testing, UI, and software process.

---

## 6. Pedagogical Delivery Research

The target reader knows basic programming ideas from Python, R, or a prior scripting context, but does not yet have Java, OO design, debugging discipline, or a reliable way to supervise AI-generated code. Prior knowledge required for this chapter should be stated as capabilities from earlier modules, not as generic "knows programming."

Common misconceptions include "if it compiles, it works," "AI writes better code than I can," "debugging means reading error messages," and "OO is just Java syntax." The strongest delivery sequence is: run or inspect a concrete artifact, predict behavior, introduce vocabulary, work a library example, transfer to inventory/scheduling variants, then ask for an AI Use Disclosure that names what the student verified.

Known teaching failure modes are syntax-first lectures without running examples, letting AI produce complete answers before students can inspect them, and treating the threaded project as a set of disconnected labs. Students who understand the concept can explain the behavior of their own program and identify what evidence would falsify their design. Students who merely memorize can reproduce definitions but cannot debug, adapt, or reject plausible generated code.

---

## 7. Representation and Display Research

An event trace should show user action → event object → handler → model update → view refresh, with responsibility count for each method.

---

## 8. Open Questions and Research Gaps

- Aging risk: Medium-high: JavaFX event APIs are stable but examples are setup-sensitive.
- Verify current JDK, NetBeans, JavaFX, Scene Builder, JUnit, and AI-tool instructions before each offering.
- Replace illustrative course-lab cases with documented student artifacts after the course has run, with permission and anonymization.
- Confirm whether the EDGE/Coursera gradebook, AI Use Disclosure form, and CLAUDE.md format match the final course deployment.
- Avoid overclaiming: compilation, passing tests, and AI fluency are evidence, but none alone proves the application satisfies requirements.

---

## 9. Sourcing Notes

Use official Java, OpenJFX, NetBeans, Scene Builder, and JUnit documentation for tool and API claims. Use Java books and OO design texts for durable conceptual explanation. Use AI coding-assistant research only for claims about observed assistance, usability, or risk; do not cite vendor marketing as evidence. Many sources are books or standards and may require library access for page-level citations.