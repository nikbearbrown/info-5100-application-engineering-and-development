# Research: Chapter 00 — Setup
## Programming with Java: An Object-Oriented Practicum

**Chapter one-line:** Install the JDK, NetBeans, and configure your first Java project without losing a lab session to tooling.
**Research date:** 2026-05-23

---

## 1. Primary Sources

### Foundational papers and texts
- Oracle, JDK Installation Guide and Java SE Downloads documentation, current release. This is the source of record for installing the supported JDK and verifying `java --version`. The chapter should treat installer screenshots as high-aging-risk and verify them before each offering.
- Apache NetBeans, NetBeans User Guide and installation documentation, current release. NetBeans setup is the practical bottleneck for the course; cite the project docs for project creation and Java platform configuration.
- OpenJDK, JEP 223: New Version-String Scheme, 2014. This helps explain Java version strings and why students must report exact versions when debugging setup problems.
- Sweller, John, "Cognitive Load During Problem Solving: Effects on Learning," Cognitive Science, 1988. Cognitive load theory supports worked examples, staged scaffolding, and avoiding too many new representations at once. It is especially relevant for JavaFX and debugging modules.
- Collins, Allan, Brown, John Seely, and Newman, Susan, "Cognitive Apprenticeship: Teaching the Crafts of Reading, Writing, and Mathematics," 1989. Cognitive apprenticeship supports making expert debugging, design, and verification moves visible before students perform them independently.

### Key empirical cases
- Documented setup friction in introductory programming courses: tool installation and IDE configuration consume early lab time and can derail learning before concepts begin. Use this as the rationale for Module 0 being a setup appendix rather than an informal preface.
- Illustrative course lab case: one student has the JRE but not the JDK; NetBeans opens but cannot compile. The insight is that 'Java is installed' is too vague; the verification step must include compiler availability and IDE platform selection.
- Illustrative AI case: a student asks AI to fix a NetBeans error and receives instructions for IntelliJ or Maven. This shows why Module 0 constrains AI to diagnosis and requires local version evidence.

---

## 2. The Core Concept — State of the Field

### What is settled
The settled instructional core is that introductory application engineering students need executable mental models, not just syntax exposure. Java's type system, class model, object references, collections, exceptions, GUI APIs, and testing tools are documented in official specifications and API references, while programming-education research shows that students learn these concepts more reliably when they predict, trace, test, and explain code. For this chapter, the author can confidently treat tooling setup, version verification, NetBeans project creation, first run, and diagnostic-only AI constraints as a design-and-verification problem, not only an implementation topic.

### What is disputed
The disputed issues are how early to introduce AI assistance, how much code generation to allow, whether object-oriented design remains the right first paradigm for applied graduate students, and how formal the verification layer should be. The book's position is that AI can be introduced, but only behind explicit phase gates: students must understand enough to inspect, explain, and reject output. Drafters should avoid claiming that AI is either harmless or categorically inappropriate; the point is disciplined delegation.

### What has changed recently (last 5 years)
AI coding assistants have changed the meaning of beginner programming assignments: students can obtain plausible code before they understand it. Java platform content is comparatively stable, but JavaFX setup, IDE workflows, JUnit integration, and AI-tool interfaces are high-aging-risk. Current-source claims about Claude, Copilot, NetBeans, Scene Builder, JavaFX packaging, or academic integrity policy should be rechecked before each offering.

---

## 3. Application Domain Examples

- Run `java --version` and `javac --version`, screenshot or paste both, and compare to course-required versions.
- Create a NetBeans Java project, run Hello World, then identify which file contains `main` and which tool compiled it.
- Ask AI to explain a setup error without letting it rewrite project structure.

---

## 4. The Book's Thesis Connection

This chapter serves the book's central thesis by making tooling setup, version verification, NetBeans project creation, first run, and diagnostic-only AI constraints part of the student's own verification capacity. The book argues that productive AI-assisted development requires genuine object-oriented understanding because the student cannot safely delegate what they cannot identify, design, or verify.

In the threaded project, this chapter contributes one concrete layer to that capacity. The learner must supply the business meaning, object boundary, failure expectation, user workflow, or verification criterion. AI can help explain, scaffold, or implement only after that human layer exists.

The research literature supports the thesis in a calibrated way. AI coding-assistant studies support the usefulness of generated code and productivity assistance, but usability and security studies show that generated code still requires human review. Programming-education research supports worked examples, tracing, prediction, testing, and reflection as the route from copied code to understanding.

---

## 5. The AI Wayback Machine — Candidate Figures

- **James Gosling** — Connection: use this figure to connect tooling setup, version verification, NetBeans project creation, first run, and diagnostic-only AI constraints to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine James Gosling reviewing a student's INFO 5100 project for tooling setup, version verification, NetBeans project creation, first run, and diagnostic-only AI constraints. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Bill Joy** — Connection: use this figure to connect tooling setup, version verification, NetBeans project creation, first run, and diagnostic-only AI constraints to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Bill Joy reviewing a student's INFO 5100 project for tooling setup, version verification, NetBeans project creation, first run, and diagnostic-only AI constraints. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Grace Hopper** — Connection: use this figure to connect tooling setup, version verification, NetBeans project creation, first run, and diagnostic-only AI constraints to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Grace Hopper reviewing a student's INFO 5100 project for tooling setup, version verification, NetBeans project creation, first run, and diagnostic-only AI constraints. Ask what evidence proves the student understood the design rather than merely accepted generated code."

Diversity note: computing history candidates skew U.S./Western European and male if the drafter uses only canonical language-design figures. Across the full book, preserve substantive candidates such as Grace Hopper, Adele Goldberg, Jean E. Sammet, Frances E. Allen, Margaret Hamilton, and Barbara Liskov where appropriate, and balance them against domain-specific figures for security, testing, UI, and software process.

---

## 6. Pedagogical Delivery Research

The target reader knows basic programming ideas from Python, R, or a prior scripting context, but does not yet have Java, OO design, debugging discipline, or a reliable way to supervise AI-generated code. Prior knowledge required for this chapter should be stated as capabilities from earlier modules, not as generic "knows programming."

Common misconceptions include "if it compiles, it works," "AI writes better code than I can," "debugging means reading error messages," and "OO is just Java syntax." The strongest delivery sequence is: run or inspect a concrete artifact, predict behavior, introduce vocabulary, work a library example, transfer to inventory/scheduling variants, then ask for an AI Use Disclosure that names what the student verified.

Known teaching failure modes are syntax-first lectures without running examples, letting AI produce complete answers before students can inspect them, and treating the threaded project as a set of disconnected labs. Students who understand the concept can explain the behavior of their own program and identify what evidence would falsify their design. Students who merely memorize can reproduce definitions but cannot debug, adapt, or reject plausible generated code.

---

## 7. Representation and Display Research

A setup verification checklist should show operating system, JDK version, compiler version, NetBeans version, project template, first run result, and diagnostic-only AI rule.

---

## 8. Open Questions and Research Gaps

- Aging risk: High: installer UI, JDK versions, NetBeans menus, and screenshots age before each offering.
- Verify current JDK, NetBeans, JavaFX, Scene Builder, JUnit, and AI-tool instructions before each offering.
- Replace illustrative course-lab cases with documented student artifacts after the course has run, with permission and anonymization.
- Confirm whether the EDGE/Coursera gradebook, AI Use Disclosure form, and CLAUDE.md format match the final course deployment.
- Avoid overclaiming: compilation, passing tests, and AI fluency are evidence, but none alone proves the application satisfies requirements.

---

## 9. Sourcing Notes

Use official Java, OpenJFX, NetBeans, Scene Builder, and JUnit documentation for tool and API claims. Use Java books and OO design texts for durable conceptual explanation. Use AI coding-assistant research only for claims about observed assistance, usability, or risk; do not cite vendor marketing as evidence. Many sources are books or standards and may require library access for page-level citations.