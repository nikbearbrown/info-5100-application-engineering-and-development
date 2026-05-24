# Research: Chapter 02 — Creating and Displaying Multiple Objects
## Programming with Java: An Object-Oriented Practicum

**Chapter one-line:** Students learn to instantiate multiple objects from one class and trace how Java manages them in memory.
**Research date:** 2026-05-23

---

## 1. Primary Sources

### Foundational papers and texts
- Gosling, James, Joy, Bill, Steele, Guy, Bracha, Gilad, Buckley, Alex, and Smith, Daniel, The Java Language Specification, Java SE 21 Edition, Oracle, 2023. This is the authoritative language source for Java classes, objects, fields, methods, inheritance, lambdas, and exceptions. Use it to anchor factual claims about Java behavior rather than relying on tutorial simplifications.
- Oracle, Java SE 21 API Specification, 2023. The API docs are the correct source for standard library contracts such as `List`, `Map`, `Set`, `Comparator`, I/O classes, and exception behavior. The chapter drafter should cite API contracts when explaining what a library type promises.
- Horstmann, Cay S., Core Java, Volume I: Fundamentals, 12th ed., 2021. Horstmann provides professional-grade explanations of Java fundamentals that are still accessible to serious beginners. Use it to supplement primary specifications with pedagogically useful examples.
- Sorva, Juha, "Visual Program Simulation in Introductory Programming Education," PhD dissertation, Aalto University, 2012. Sorva's work supports visualization and tracing of object state and references for novices. It is directly relevant to stack/heap mental models without going into JVM implementation internals.
- Robins, Anthony, Rountree, Janet, and Rountree, Nathan, "Learning and Teaching Programming: A Review and Discussion," Computer Science Education, 2003. This review documents recurring novice difficulties with tracing, abstraction, syntax, and mental models. It supports the course's emphasis on prediction, tracing, and explanation before delegation.
- Sweller, John, "Cognitive Load During Problem Solving: Effects on Learning," Cognitive Science, 1988. Cognitive load theory supports worked examples, staged scaffolding, and avoiding too many new representations at once. It is especially relevant for JavaFX and debugging modules.

### Key empirical cases
- Illustrative course lab: three `Person` objects print the same name but different ages; students must locate where the values live. This exposes the reference-versus-object distinction.
- Library example: two patrons check out different books using the same `Patron` class. The insight is that a class is a blueprint and each object has separate state.
- Common novice bug: modifying one variable and expecting another object to change, or copying references accidentally. This is well documented in programming education literature on mental models.

---

## 2. The Core Concept — State of the Field

### What is settled
The settled instructional core is that introductory application engineering students need executable mental models, not just syntax exposure. Java's type system, class model, object references, collections, exceptions, GUI APIs, and testing tools are documented in official specifications and API references, while programming-education research shows that students learn these concepts more reliably when they predict, trace, test, and explain code. For this chapter, the author can confidently treat class/object distinction, constructors, references, fields, stack/heap mental model, multiple instances, and object tracing as a design-and-verification problem, not only an implementation topic.

### What is disputed
The disputed issues are how early to introduce AI assistance, how much code generation to allow, whether object-oriented design remains the right first paradigm for applied graduate students, and how formal the verification layer should be. The book's position is that AI can be introduced, but only behind explicit phase gates: students must understand enough to inspect, explain, and reject output. Drafters should avoid claiming that AI is either harmless or categorically inappropriate; the point is disciplined delegation.

### What has changed recently (last 5 years)
AI coding assistants have changed the meaning of beginner programming assignments: students can obtain plausible code before they understand it. Java platform content is comparatively stable, but JavaFX setup, IDE workflows, JUnit integration, and AI-tool interfaces are high-aging-risk. Current-source claims about Claude, Copilot, NetBeans, Scene Builder, JavaFX packaging, or academic integrity policy should be rechecked before each offering.

---

## 3. Application Domain Examples

- Instantiate three `Book` objects with different ISBNs and trace fields after each constructor call.
- Modify `patronA.name` and explain why `patronB.name` does not change.
- Use AI only to quiz the student on their own class after they have written it.

---

## 4. The Book's Thesis Connection

This chapter serves the book's central thesis by making class/object distinction, constructors, references, fields, stack/heap mental model, multiple instances, and object tracing part of the student's own verification capacity. The book argues that productive AI-assisted development requires genuine object-oriented understanding because the student cannot safely delegate what they cannot identify, design, or verify.

In the threaded project, this chapter contributes one concrete layer to that capacity. The learner must supply the business meaning, object boundary, failure expectation, user workflow, or verification criterion. AI can help explain, scaffold, or implement only after that human layer exists.

The research literature supports the thesis in a calibrated way. AI coding-assistant studies support the usefulness of generated code and productivity assistance, but usability and security studies show that generated code still requires human review. Programming-education research supports worked examples, tracing, prediction, testing, and reflection as the route from copied code to understanding.

---

## 5. The AI Wayback Machine — Candidate Figures

- **Adele Goldberg** — Connection: use this figure to connect class/object distinction, constructors, references, fields, stack/heap mental model, multiple instances, and object tracing to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Adele Goldberg reviewing a student's INFO 5100 project for class/object distinction, constructors, references, fields, stack/heap mental model, multiple instances, and object tracing. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Alan Kay** — Connection: use this figure to connect class/object distinction, constructors, references, fields, stack/heap mental model, multiple instances, and object tracing to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Alan Kay reviewing a student's INFO 5100 project for class/object distinction, constructors, references, fields, stack/heap mental model, multiple instances, and object tracing. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Jean E. Sammet** — Connection: use this figure to connect class/object distinction, constructors, references, fields, stack/heap mental model, multiple instances, and object tracing to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Jean E. Sammet reviewing a student's INFO 5100 project for class/object distinction, constructors, references, fields, stack/heap mental model, multiple instances, and object tracing. Ask what evidence proves the student understood the design rather than merely accepted generated code."

Diversity note: computing history candidates skew U.S./Western European and male if the drafter uses only canonical language-design figures. Across the full book, preserve substantive candidates such as Grace Hopper, Adele Goldberg, Jean E. Sammet, Frances E. Allen, Margaret Hamilton, and Barbara Liskov where appropriate, and balance them against domain-specific figures for security, testing, UI, and software process.

---

## 6. Pedagogical Delivery Research

The target reader knows basic programming ideas from Python, R, or a prior scripting context, but does not yet have Java, OO design, debugging discipline, or a reliable way to supervise AI-generated code. Prior knowledge required for this chapter should be stated as capabilities from earlier modules, not as generic "knows programming."

Common misconceptions include "if it compiles, it works," "AI writes better code than I can," "debugging means reading error messages," and "OO is just Java syntax." The strongest delivery sequence is: run or inspect a concrete artifact, predict behavior, introduce vocabulary, work a library example, transfer to inventory/scheduling variants, then ask for an AI Use Disclosure that names what the student verified.

Known teaching failure modes are syntax-first lectures without running examples, letting AI produce complete answers before students can inspect them, and treating the threaded project as a set of disconnected labs. Students who understand the concept can explain the behavior of their own program and identify what evidence would falsify their design. Students who merely memorize can reproduce definitions but cannot debug, adapt, or reject plausible generated code.

---

## 7. Representation and Display Research

A memory-trace diagram should show reference variables separately from heap objects, with arrows, field values, and one method call changing only one instance.

---

## 8. Open Questions and Research Gaps

- Aging risk: Low for Java concepts; medium for visual simplification because stack/heap diagrams can overclaim implementation detail.
- Verify current JDK, NetBeans, JavaFX, Scene Builder, JUnit, and AI-tool instructions before each offering.
- Replace illustrative course-lab cases with documented student artifacts after the course has run, with permission and anonymization.
- Confirm whether the EDGE/Coursera gradebook, AI Use Disclosure form, and CLAUDE.md format match the final course deployment.
- Avoid overclaiming: compilation, passing tests, and AI fluency are evidence, but none alone proves the application satisfies requirements.

---

## 9. Sourcing Notes

Use official Java, OpenJFX, NetBeans, Scene Builder, and JUnit documentation for tool and API claims. Use Java books and OO design texts for durable conceptual explanation. Use AI coding-assistant research only for claims about observed assistance, usability, or risk; do not cite vendor marketing as evidence. Many sources are books or standards and may require library access for page-level citations.