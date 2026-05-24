# Research: Chapter 14 — Final Project: Complete Application with Ecosystem Design
## Programming with Java: An Object-Oriented Practicum

**Chapter one-line:** Students complete, defend, and present a full GUI business application — and demonstrate, for every AI-assisted decision, what required their own engineering judgment.
**Research date:** 2026-05-23

---

## 1. Primary Sources

### Foundational papers and texts
- Schön, Donald A., The Reflective Practitioner, 1983. Schön supports the final defense as professional reflection-in-action rather than a recitation of features. It gives a research basis for asking students to defend decisions under questioning.
- Fagan, Michael E., "Design and Code Inspections to Reduce Errors in Program Development," IBM Systems Journal, 1976. Fagan supports structured review and inspection as professional practice. Use it for code review and final audit discipline.
- Bass, Len, Clements, Paul, and Kazman, Rick, Software Architecture in Practice, 4th ed., 2021. This supports tradeoff reasoning and architecture decisions in the final defense. Use beginner-level concepts: quality attributes, alternatives, and consequences.
- Peng, Siddharth et al., "The Impact of AI on Developer Productivity: Evidence from GitHub Copilot," arXiv, 2023. The study supports the claim that AI assistance can accelerate programming tasks, while leaving open whether learners can verify outputs safely. Use it to motivate disciplined AI use rather than AI replacement.
- Vaithilingam, Priyan et al., "Expectation vs. Experience: Evaluating the Usability of Code Generation Tools Powered by Large Language Models," CHI Extended Abstracts, 2022. This paper is useful for the gap between plausible generated code and user understanding. It supports the course's requirement that students explain and verify AI-assisted work.
- Pearce, Hammond et al., "Asleep at the Keyboard? Assessing the Security of GitHub Copilot's Code Contributions," IEEE Symposium on Security and Privacy Workshops, 2022. This gives empirical caution that generated code can look plausible while embedding risks. Use it where the book argues that AI output requires human auditing.
- Collins, Allan, Brown, John Seely, and Newman, Susan, "Cognitive Apprenticeship: Teaching the Crafts of Reading, Writing, and Mathematics," 1989. Cognitive apprenticeship supports making expert debugging, design, and verification moves visible before students perform them independently.
- Chi, Michelene T. H. and Wylie, Ruth, "The ICAP Framework," Educational Psychologist, 2014. ICAP supports active and constructive learning through prediction, explanation, debugging, peer discussion, and defense rather than passive reading of code.

### Key empirical cases
- Course-internal final demo: a running GUI application with source, AI disclosures, and examiner questions. This is the principal case once the course has run; until then it remains a designed assessment case.
- Professional code review: documented inspection practices show that software quality depends on reviewable decisions, not just working code.
- AI-assisted integration case: code generated for one component conflicts with earlier design decisions. The student must show what was verified, changed, or rejected.

---

## 2. The Core Concept — State of the Field

### What is settled
The settled instructional core is that introductory application engineering students need executable mental models, not just syntax exposure. Java's type system, class model, object references, collections, exceptions, GUI APIs, and testing tools are documented in official specifications and API references, while programming-education research shows that students learn these concepts more reliably when they predict, trace, test, and explain code. For this chapter, the author can confidently treat final GUI application, ecosystem design, code review, AI Use Disclosure synthesis, design defense, deployment awareness, and professional handoff as a design-and-verification problem, not only an implementation topic.

### What is disputed
The disputed issues are how early to introduce AI assistance, how much code generation to allow, whether object-oriented design remains the right first paradigm for applied graduate students, and how formal the verification layer should be. The book's position is that AI can be introduced, but only behind explicit phase gates: students must understand enough to inspect, explain, and reject output. Drafters should avoid claiming that AI is either harmless or categorically inappropriate; the point is disciplined delegation.

### What has changed recently (last 5 years)
AI coding assistants have changed the meaning of beginner programming assignments: students can obtain plausible code before they understand it. Java platform content is comparatively stable, but JavaFX setup, IDE workflows, JUnit integration, and AI-tool interfaces are high-aging-risk. Current-source claims about Claude, Copilot, NetBeans, Scene Builder, JavaFX packaging, or academic integrity policy should be rechecked before each offering.

---

## 3. Application Domain Examples

- Library: final GUI supports catalog search, patron login, checkout/return, persistence, tests, and disclosure.
- Inventory: final GUI supports product search, stock movement, user roles, persistence, tests, and disclosure.
- Scheduling: final GUI supports provider schedule, appointment booking, persistence, tests, and disclosure.

---

## 4. The Book's Thesis Connection

This chapter serves the book's central thesis by making final GUI application, ecosystem design, code review, AI Use Disclosure synthesis, design defense, deployment awareness, and professional handoff part of the student's own verification capacity. The book argues that productive AI-assisted development requires genuine object-oriented understanding because the student cannot safely delegate what they cannot identify, design, or verify.

In the threaded project, this chapter contributes one concrete layer to that capacity. The learner must supply the business meaning, object boundary, failure expectation, user workflow, or verification criterion. AI can help explain, scaffold, or implement only after that human layer exists.

The research literature supports the thesis in a calibrated way. AI coding-assistant studies support the usefulness of generated code and productivity assistance, but usability and security studies show that generated code still requires human review. Programming-education research supports worked examples, tracing, prediction, testing, and reflection as the route from copied code to understanding.

---

## 5. The AI Wayback Machine — Candidate Figures

- **Margaret Hamilton** — Connection: use this figure to connect final GUI application, ecosystem design, code review, AI Use Disclosure synthesis, design defense, deployment awareness, and professional handoff to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Margaret Hamilton reviewing a student's INFO 5100 project for final GUI application, ecosystem design, code review, AI Use Disclosure synthesis, design defense, deployment awareness, and professional handoff. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Watts Humphrey** — Connection: use this figure to connect final GUI application, ecosystem design, code review, AI Use Disclosure synthesis, design defense, deployment awareness, and professional handoff to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Watts Humphrey reviewing a student's INFO 5100 project for final GUI application, ecosystem design, code review, AI Use Disclosure synthesis, design defense, deployment awareness, and professional handoff. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Donald Schön** — Connection: use this figure to connect final GUI application, ecosystem design, code review, AI Use Disclosure synthesis, design defense, deployment awareness, and professional handoff to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Donald Schön reviewing a student's INFO 5100 project for final GUI application, ecosystem design, code review, AI Use Disclosure synthesis, design defense, deployment awareness, and professional handoff. Ask what evidence proves the student understood the design rather than merely accepted generated code."

Diversity note: computing history candidates skew U.S./Western European and male if the drafter uses only canonical language-design figures. Across the full book, preserve substantive candidates such as Grace Hopper, Adele Goldberg, Jean E. Sammet, Frances E. Allen, Margaret Hamilton, and Barbara Liskov where appropriate, and balance them against domain-specific figures for security, testing, UI, and software process.

---

## 6. Pedagogical Delivery Research

The target reader knows basic programming ideas from Python, R, or a prior scripting context, but does not yet have Java, OO design, debugging discipline, or a reliable way to supervise AI-generated code. Prior knowledge required for this chapter should be stated as capabilities from earlier modules, not as generic "knows programming."

Common misconceptions include "if it compiles, it works," "AI writes better code than I can," "debugging means reading error messages," and "OO is just Java syntax." The strongest delivery sequence is: run or inspect a concrete artifact, predict behavior, introduce vocabulary, work a library example, transfer to inventory/scheduling variants, then ask for an AI Use Disclosure that names what the student verified.

Known teaching failure modes are syntax-first lectures without running examples, letting AI produce complete answers before students can inspect them, and treating the threaded project as a set of disconnected labs. Students who understand the concept can explain the behavior of their own program and identify what evidence would falsify their design. Students who merely memorize can reproduce definitions but cannot debug, adapt, or reject plausible generated code.

---

## 7. Representation and Display Research

A final defense matrix should list component, AI assistance used, human verification, evidence, design decision, rejected alternative, and examiner question.

---

## 8. Open Questions and Research Gaps

- Aging risk: Medium: final project requirements stable, but AI disclosure expectations and platform details age.
- Verify current JDK, NetBeans, JavaFX, Scene Builder, JUnit, and AI-tool instructions before each offering.
- Replace illustrative course-lab cases with documented student artifacts after the course has run, with permission and anonymization.
- Confirm whether the EDGE/Coursera gradebook, AI Use Disclosure form, and CLAUDE.md format match the final course deployment.
- Avoid overclaiming: compilation, passing tests, and AI fluency are evidence, but none alone proves the application satisfies requirements.

---

## 9. Sourcing Notes

Use official Java, OpenJFX, NetBeans, Scene Builder, and JUnit documentation for tool and API claims. Use Java books and OO design texts for durable conceptual explanation. Use AI coding-assistant research only for claims about observed assistance, usability, or risk; do not cite vendor marketing as evidence. Many sources are books or standards and may require library access for page-level citations.