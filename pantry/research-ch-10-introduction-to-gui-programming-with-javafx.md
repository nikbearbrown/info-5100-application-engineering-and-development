# Research: Chapter 10 — Introduction to GUI Programming with JavaFX
## Programming with Java: An Object-Oriented Practicum

**Chapter one-line:** Students learn to connect the object model they have built to a visual interface — understanding that the GUI is a view of the model, not the model itself.
**Research date:** 2026-05-23

---

## 1. Primary Sources

### Foundational papers and texts
- OpenJFX Documentation, JavaFX controls, layout, properties, and TableView guides, current version. OpenJFX is the living source for JavaFX after its decoupling from the JDK. Verify version and setup instructions before each offering.
- Oracle, JavaFX 8 documentation and tutorials, especially scene graph and property binding. Some official materials remain useful conceptually, but version details may age.
- Krasner, Glenn E. and Pope, Stephen T., "A Cookbook for Using the Model-View-Controller User Interface Paradigm in Smalltalk-80," Journal of Object-Oriented Programming, 1988. This is a foundational MVC source that supports separating model, view, and controller.
- Robins, Anthony, Rountree, Janet, and Rountree, Nathan, "Learning and Teaching Programming: A Review and Discussion," Computer Science Education, 2003. This review documents recurring novice difficulties with tracing, abstraction, syntax, and mental models. It supports the course's emphasis on prediction, tracing, and explanation before delegation.
- Sweller, John, "Cognitive Load During Problem Solving: Effects on Learning," Cognitive Science, 1988. Cognitive load theory supports worked examples, staged scaffolding, and avoiding too many new representations at once. It is especially relevant for JavaFX and debugging modules.

### Key empirical cases
- Illustrative course lab: the same `Book` objects displayed as console output and as a JavaFX TableView. Students identify what changed and what stayed model-level.
- GUI leakage case: AI puts search logic and persistence directly in the view code. Students refactor to preserve model-view separation.
- Setup friction case: JavaFX module/path configuration fails even when Java itself works. This reinforces Module 0 setup verification.

---

## 2. The Core Concept — State of the Field

### What is settled
The settled instructional core is that introductory application engineering students need executable mental models, not just syntax exposure. Java's type system, class model, object references, collections, exceptions, GUI APIs, and testing tools are documented in official specifications and API references, while programming-education research shows that students learn these concepts more reliably when they predict, trace, test, and explain code. For this chapter, the author can confidently treat JavaFX scene graph, panes, controls, TableView, property binding, model-view-controller separation, and AI GUI boilerplate audit as a design-and-verification problem, not only an implementation topic.

### What is disputed
The disputed issues are how early to introduce AI assistance, how much code generation to allow, whether object-oriented design remains the right first paradigm for applied graduate students, and how formal the verification layer should be. The book's position is that AI can be introduced, but only behind explicit phase gates: students must understand enough to inspect, explain, and reject output. Drafters should avoid claiming that AI is either harmless or categorically inappropriate; the point is disciplined delegation.

### What has changed recently (last 5 years)
AI coding assistants have changed the meaning of beginner programming assignments: students can obtain plausible code before they understand it. Java platform content is comparatively stable, but JavaFX setup, IDE workflows, JUnit integration, and AI-tool interfaces are high-aging-risk. Current-source claims about Claude, Copilot, NetBeans, Scene Builder, JavaFX packaging, or academic integrity policy should be rechecked before each offering.

---

## 3. Application Domain Examples

- Library: TableView of `Book` objects with title, author, availability columns.
- Inventory: TableView of products with stock status highlighting.
- Scheduling: TableView or ListView of appointment slots filtered by date.

---

## 4. The Book's Thesis Connection

This chapter serves the book's central thesis by making JavaFX scene graph, panes, controls, TableView, property binding, model-view-controller separation, and AI GUI boilerplate audit part of the student's own verification capacity. The book argues that productive AI-assisted development requires genuine object-oriented understanding because the student cannot safely delegate what they cannot identify, design, or verify.

In the threaded project, this chapter contributes one concrete layer to that capacity. The learner must supply the business meaning, object boundary, failure expectation, user workflow, or verification criterion. AI can help explain, scaffold, or implement only after that human layer exists.

The research literature supports the thesis in a calibrated way. AI coding-assistant studies support the usefulness of generated code and productivity assistance, but usability and security studies show that generated code still requires human review. Programming-education research supports worked examples, tracing, prediction, testing, and reflection as the route from copied code to understanding.

---

## 5. The AI Wayback Machine — Candidate Figures

- **Adele Goldberg** — Connection: use this figure to connect JavaFX scene graph, panes, controls, TableView, property binding, model-view-controller separation, and AI GUI boilerplate audit to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Adele Goldberg reviewing a student's INFO 5100 project for JavaFX scene graph, panes, controls, TableView, property binding, model-view-controller separation, and AI GUI boilerplate audit. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Trygve Reenskaug** — Connection: use this figure to connect JavaFX scene graph, panes, controls, TableView, property binding, model-view-controller separation, and AI GUI boilerplate audit to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Trygve Reenskaug reviewing a student's INFO 5100 project for JavaFX scene graph, panes, controls, TableView, property binding, model-view-controller separation, and AI GUI boilerplate audit. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Ben Shneiderman** — Connection: use this figure to connect JavaFX scene graph, panes, controls, TableView, property binding, model-view-controller separation, and AI GUI boilerplate audit to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Ben Shneiderman reviewing a student's INFO 5100 project for JavaFX scene graph, panes, controls, TableView, property binding, model-view-controller separation, and AI GUI boilerplate audit. Ask what evidence proves the student understood the design rather than merely accepted generated code."

Diversity note: computing history candidates skew U.S./Western European and male if the drafter uses only canonical language-design figures. Across the full book, preserve substantive candidates such as Grace Hopper, Adele Goldberg, Jean E. Sammet, Frances E. Allen, Margaret Hamilton, and Barbara Liskov where appropriate, and balance them against domain-specific figures for security, testing, UI, and software process.

---

## 6. Pedagogical Delivery Research

The target reader knows basic programming ideas from Python, R, or a prior scripting context, but does not yet have Java, OO design, debugging discipline, or a reliable way to supervise AI-generated code. Prior knowledge required for this chapter should be stated as capabilities from earlier modules, not as generic "knows programming."

Common misconceptions include "if it compiles, it works," "AI writes better code than I can," "debugging means reading error messages," and "OO is just Java syntax." The strongest delivery sequence is: run or inspect a concrete artifact, predict behavior, introduce vocabulary, work a library example, transfer to inventory/scheduling variants, then ask for an AI Use Disclosure that names what the student verified.

Known teaching failure modes are syntax-first lectures without running examples, letting AI produce complete answers before students can inspect them, and treating the threaded project as a set of disconnected labs. Students who understand the concept can explain the behavior of their own program and identify what evidence would falsify their design. Students who merely memorize can reproduce definitions but cannot debug, adapt, or reject plausible generated code.

---

## 7. Representation and Display Research

A model-view-controller diagram should map domain object fields to TableView columns, controller methods, and forbidden model logic in view code.

---

## 8. Open Questions and Research Gaps

- Aging risk: High: JavaFX setup, module configuration, Scene Builder compatibility, and examples require review before each offering.
- Verify current JDK, NetBeans, JavaFX, Scene Builder, JUnit, and AI-tool instructions before each offering.
- Replace illustrative course-lab cases with documented student artifacts after the course has run, with permission and anonymization.
- Confirm whether the EDGE/Coursera gradebook, AI Use Disclosure form, and CLAUDE.md format match the final course deployment.
- Avoid overclaiming: compilation, passing tests, and AI fluency are evidence, but none alone proves the application satisfies requirements.

---

## 9. Sourcing Notes

Use official Java, OpenJFX, NetBeans, Scene Builder, and JUnit documentation for tool and API claims. Use Java books and OO design texts for durable conceptual explanation. Use AI coding-assistant research only for claims about observed assistance, usability, or risk; do not cite vendor marketing as evidence. Many sources are books or standards and may require library access for page-level citations.