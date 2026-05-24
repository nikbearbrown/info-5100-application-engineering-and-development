# Research: Chapter 03 — User Interaction Design
## Programming with Java: An Object-Oriented Practicum

**Chapter one-line:** Students learn to design user flows as navigation between screens, connecting what the user sees to what the objects do.
**Research date:** 2026-05-23

---

## 1. Primary Sources

### Foundational papers and texts
- Norman, Donald A., The Design of Everyday Things, revised ed., 2013. Norman supports teaching user actions, feedback, and conceptual models before GUI code. This is useful for connecting screens to user goals.
- Shneiderman, Ben et al., Designing the User Interface, 6th ed., 2016. This provides a human-computer interaction base for screen flows, feedback, and task-centered design.
- Gosling, James, Joy, Bill, Steele, Guy, Bracha, Gilad, Buckley, Alex, and Smith, Daniel, The Java Language Specification, Java SE 21 Edition, Oracle, 2023. This is the authoritative language source for Java classes, objects, fields, methods, inheritance, lambdas, and exceptions. Use it to anchor factual claims about Java behavior rather than relying on tutorial simplifications.
- Oracle, Java SE 21 API Specification, 2023. The API docs are the correct source for standard library contracts such as `List`, `Map`, `Set`, `Comparator`, I/O classes, and exception behavior. The chapter drafter should cite API contracts when explaining what a library type promises.
- Robins, Anthony, Rountree, Janet, and Rountree, Nathan, "Learning and Teaching Programming: A Review and Discussion," Computer Science Education, 2003. This review documents recurring novice difficulties with tracing, abstraction, syntax, and mental models. It supports the course's emphasis on prediction, tracing, and explanation before delegation.
- Sweller, John, "Cognitive Load During Problem Solving: Effects on Learning," Cognitive Science, 1988. Cognitive load theory supports worked examples, staged scaffolding, and avoiding too many new representations at once. It is especially relevant for JavaFX and debugging modules.
- Collins, Allan, Brown, John Seely, and Newman, Susan, "Cognitive Apprenticeship: Teaching the Crafts of Reading, Writing, and Mathematics," 1989. Cognitive apprenticeship supports making expert debugging, design, and verification moves visible before students perform them independently.
- Chi, Michelene T. H. and Wylie, Ruth, "The ICAP Framework," Educational Psychologist, 2014. ICAP supports active and constructive learning through prediction, explanation, debugging, peer discussion, and defense rather than passive reading of code.

### Key empirical cases
- Illustrative course lab: Search → Result → Checkout → Confirmation for library checkout, with a `Book` object passed between screens. This case ties visual flow to object lifecycle.
- Common UI state bug: one screen displays stale object data because the student copied values rather than passing a reference or refreshing from the model.
- AI scaffold case: AI generates CardLayout skeleton while the student owns business behavior. This illustrates the module's structure-versus-behavior boundary.

---

## 2. The Core Concept — State of the Field

### What is settled
The settled instructional core is that introductory application engineering students need executable mental models, not just syntax exposure. Java's type system, class model, object references, collections, exceptions, GUI APIs, and testing tools are documented in official specifications and API references, while programming-education research shows that students learn these concepts more reliably when they predict, trace, test, and explain code. For this chapter, the author can confidently treat screen navigation, CardLayout, object state across screens, references, user-flow diagrams, and separation of concerns as a design-and-verification problem, not only an implementation topic.

### What is disputed
The disputed issues are how early to introduce AI assistance, how much code generation to allow, whether object-oriented design remains the right first paradigm for applied graduate students, and how formal the verification layer should be. The book's position is that AI can be introduced, but only behind explicit phase gates: students must understand enough to inspect, explain, and reject output. Drafters should avoid claiming that AI is either harmless or categorically inappropriate; the point is disciplined delegation.

### What has changed recently (last 5 years)
AI coding assistants have changed the meaning of beginner programming assignments: students can obtain plausible code before they understand it. Java platform content is comparatively stable, but JavaFX setup, IDE workflows, JUnit integration, and AI-tool interfaces are high-aging-risk. Current-source claims about Claude, Copilot, NetBeans, Scene Builder, JavaFX packaging, or academic integrity policy should be rechecked before each offering.

---

## 3. Application Domain Examples

- Library flow: a selected `Book` reference moves from search result to checkout confirmation.
- Inventory flow: a selected `Product` moves from list to adjustment screen.
- Scheduling flow: a selected `AppointmentSlot` moves from calendar to booking confirmation.

---

## 4. The Book's Thesis Connection

This chapter serves the book's central thesis by making screen navigation, CardLayout, object state across screens, references, user-flow diagrams, and separation of concerns part of the student's own verification capacity. The book argues that productive AI-assisted development requires genuine object-oriented understanding because the student cannot safely delegate what they cannot identify, design, or verify.

In the threaded project, this chapter contributes one concrete layer to that capacity. The learner must supply the business meaning, object boundary, failure expectation, user workflow, or verification criterion. AI can help explain, scaffold, or implement only after that human layer exists.

The research literature supports the thesis in a calibrated way. AI coding-assistant studies support the usefulness of generated code and productivity assistance, but usability and security studies show that generated code still requires human review. Programming-education research supports worked examples, tracing, prediction, testing, and reflection as the route from copied code to understanding.

---

## 5. The AI Wayback Machine — Candidate Figures

- **Douglas Engelbart** — Connection: use this figure to connect screen navigation, CardLayout, object state across screens, references, user-flow diagrams, and separation of concerns to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Douglas Engelbart reviewing a student's INFO 5100 project for screen navigation, CardLayout, object state across screens, references, user-flow diagrams, and separation of concerns. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Ben Shneiderman** — Connection: use this figure to connect screen navigation, CardLayout, object state across screens, references, user-flow diagrams, and separation of concerns to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Ben Shneiderman reviewing a student's INFO 5100 project for screen navigation, CardLayout, object state across screens, references, user-flow diagrams, and separation of concerns. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Adele Goldberg** — Connection: use this figure to connect screen navigation, CardLayout, object state across screens, references, user-flow diagrams, and separation of concerns to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Adele Goldberg reviewing a student's INFO 5100 project for screen navigation, CardLayout, object state across screens, references, user-flow diagrams, and separation of concerns. Ask what evidence proves the student understood the design rather than merely accepted generated code."

Diversity note: computing history candidates skew U.S./Western European and male if the drafter uses only canonical language-design figures. Across the full book, preserve substantive candidates such as Grace Hopper, Adele Goldberg, Jean E. Sammet, Frances E. Allen, Margaret Hamilton, and Barbara Liskov where appropriate, and balance them against domain-specific figures for security, testing, UI, and software process.

---

## 6. Pedagogical Delivery Research

The target reader knows basic programming ideas from Python, R, or a prior scripting context, but does not yet have Java, OO design, debugging discipline, or a reliable way to supervise AI-generated code. Prior knowledge required for this chapter should be stated as capabilities from earlier modules, not as generic "knows programming."

Common misconceptions include "if it compiles, it works," "AI writes better code than I can," "debugging means reading error messages," and "OO is just Java syntax." The strongest delivery sequence is: run or inspect a concrete artifact, predict behavior, introduce vocabulary, work a library example, transfer to inventory/scheduling variants, then ask for an AI Use Disclosure that names what the student verified.

Known teaching failure modes are syntax-first lectures without running examples, letting AI produce complete answers before students can inspect them, and treating the threaded project as a set of disconnected labs. Students who understand the concept can explain the behavior of their own program and identify what evidence would falsify their design. Students who merely memorize can reproduce definitions but cannot debug, adapt, or reject plausible generated code.

---

## 7. Representation and Display Research

A screen-flow diagram should show screens, user actions, object references passed, object fields populated, and where state is stored after each transition.

---

## 8. Open Questions and Research Gaps

- Aging risk: Medium: CardLayout examples are stable but UI teaching may shift toward JavaFX later in the course.
- Verify current JDK, NetBeans, JavaFX, Scene Builder, JUnit, and AI-tool instructions before each offering.
- Replace illustrative course-lab cases with documented student artifacts after the course has run, with permission and anonymization.
- Confirm whether the EDGE/Coursera gradebook, AI Use Disclosure form, and CLAUDE.md format match the final course deployment.
- Avoid overclaiming: compilation, passing tests, and AI fluency are evidence, but none alone proves the application satisfies requirements.

---

## 9. Sourcing Notes

Use official Java, OpenJFX, NetBeans, Scene Builder, and JUnit documentation for tool and API claims. Use Java books and OO design texts for durable conceptual explanation. Use AI coding-assistant research only for claims about observed assistance, usability, or risk; do not cite vendor marketing as evidence. Many sources are books or standards and may require library access for page-level citations.