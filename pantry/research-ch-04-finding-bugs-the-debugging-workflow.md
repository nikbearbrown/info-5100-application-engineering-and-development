# Research: Chapter 04 — Finding Bugs: The Debugging Workflow
## Programming with Java: An Object-Oriented Practicum

**Chapter one-line:** Students learn a systematic debugging methodology — hypothesis, isolation, test — using the IDE debugger and their own reasoning, not error message reading alone.
**Research date:** 2026-05-23

---

## 1. Primary Sources

### Foundational papers and texts
- Zeller, Andreas, Why Programs Fail: A Guide to Systematic Debugging, 2nd ed., 2009. Zeller provides a rigorous and teachable framing of debugging as systematic hypothesis testing. It is directly relevant to symptom, cause, isolation, and experiment.
- Eisenstadt, Marc, "My Hairiest Bug War Stories," Communications of the ACM, 1997. This source documents the messy reality of debugging and why expert strategies matter beyond reading error messages.
- Robins, Anthony, Rountree, Janet, and Rountree, Nathan, "Learning and Teaching Programming: A Review and Discussion," Computer Science Education, 2003. This review documents recurring novice difficulties with tracing, abstraction, syntax, and mental models. It supports the course's emphasis on prediction, tracing, and explanation before delegation.
- Sweller, John, "Cognitive Load During Problem Solving: Effects on Learning," Cognitive Science, 1988. Cognitive load theory supports worked examples, staged scaffolding, and avoiding too many new representations at once. It is especially relevant for JavaFX and debugging modules.
- Collins, Allan, Brown, John Seely, and Newman, Susan, "Cognitive Apprenticeship: Teaching the Crafts of Reading, Writing, and Mathematics," 1989. Cognitive apprenticeship supports making expert debugging, design, and verification moves visible before students perform them independently.
- Chi, Michelene T. H. and Wylie, Ruth, "The ICAP Framework," Educational Psychologist, 2014. ICAP supports active and constructive learning through prediction, explanation, debugging, peer discussion, and defense rather than passive reading of code.
- Peng, Siddharth et al., "The Impact of AI on Developer Productivity: Evidence from GitHub Copilot," arXiv, 2023. The study supports the claim that AI assistance can accelerate programming tasks, while leaving open whether learners can verify outputs safely. Use it to motivate disciplined AI use rather than AI replacement.
- Vaithilingam, Priyan et al., "Expectation vs. Experience: Evaluating the Usability of Code Generation Tools Powered by Large Language Models," CHI Extended Abstracts, 2022. This paper is useful for the gap between plausible generated code and user understanding. It supports the course's requirement that students explain and verify AI-assisted work.
- Pearce, Hammond et al., "Asleep at the Keyboard? Assessing the Security of GitHub Copilot's Code Contributions," IEEE Symposium on Security and Privacy Workshops, 2022. This gives empirical caution that generated code can look plausible while embedding risks. Use it where the book argues that AI output requires human auditing.

### Key empirical cases
- Illustrative course lab: library checkout assigns a book to the wrong patron after a particular operation sequence. Students must form a hypothesis before seeing the fix.
- Documented educational failure mode: novices often patch symptoms or follow error messages without forming a causal model. Programming education research supports structured tracing and explanation.
- AI debugging case: a generated fix changes a return value and hides the symptom while leaving the design defect. This is illustrative but strongly aligned with AI usability findings.

---

## 2. The Core Concept — State of the Field

### What is settled
The settled instructional core is that introductory application engineering students need executable mental models, not just syntax exposure. Java's type system, class model, object references, collections, exceptions, GUI APIs, and testing tools are documented in official specifications and API references, while programming-education research shows that students learn these concepts more reliably when they predict, trace, test, and explain code. For this chapter, the author can confidently treat debugging workflow, symptom/proximate/root cause, breakpoints, stepping, object inspection, and AI debugging phase gate as a design-and-verification problem, not only an implementation topic.

### What is disputed
The disputed issues are how early to introduce AI assistance, how much code generation to allow, whether object-oriented design remains the right first paradigm for applied graduate students, and how formal the verification layer should be. The book's position is that AI can be introduced, but only behind explicit phase gates: students must understand enough to inspect, explain, and reject output. Drafters should avoid claiming that AI is either harmless or categorically inappropriate; the point is disciplined delegation.

### What has changed recently (last 5 years)
AI coding assistants have changed the meaning of beginner programming assignments: students can obtain plausible code before they understand it. Java platform content is comparatively stable, but JavaFX setup, IDE workflows, JUnit integration, and AI-tool interfaces are high-aging-risk. Current-source claims about Claude, Copilot, NetBeans, Scene Builder, JavaFX packaging, or academic integrity policy should be rechecked before each offering.

---

## 3. Application Domain Examples

- Use NetBeans breakpoints to inspect `book.currentPatron` before and after checkout.
- Write a bug hypothesis in plain English before asking AI whether it is plausible.
- Classify evidence as symptom, proximate cause, or root cause.

---

## 4. The Book's Thesis Connection

This chapter serves the book's central thesis by making debugging workflow, symptom/proximate/root cause, breakpoints, stepping, object inspection, and AI debugging phase gate part of the student's own verification capacity. The book argues that productive AI-assisted development requires genuine object-oriented understanding because the student cannot safely delegate what they cannot identify, design, or verify.

In the threaded project, this chapter contributes one concrete layer to that capacity. The learner must supply the business meaning, object boundary, failure expectation, user workflow, or verification criterion. AI can help explain, scaffold, or implement only after that human layer exists.

The research literature supports the thesis in a calibrated way. AI coding-assistant studies support the usefulness of generated code and productivity assistance, but usability and security studies show that generated code still requires human review. Programming-education research supports worked examples, tracing, prediction, testing, and reflection as the route from copied code to understanding.

---

## 5. The AI Wayback Machine — Candidate Figures

- **Grace Hopper** — Connection: use this figure to connect debugging workflow, symptom/proximate/root cause, breakpoints, stepping, object inspection, and AI debugging phase gate to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Grace Hopper reviewing a student's INFO 5100 project for debugging workflow, symptom/proximate/root cause, breakpoints, stepping, object inspection, and AI debugging phase gate. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Edsger W. Dijkstra** — Connection: use this figure to connect debugging workflow, symptom/proximate/root cause, breakpoints, stepping, object inspection, and AI debugging phase gate to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Edsger W. Dijkstra reviewing a student's INFO 5100 project for debugging workflow, symptom/proximate/root cause, breakpoints, stepping, object inspection, and AI debugging phase gate. Ask what evidence proves the student understood the design rather than merely accepted generated code."
- **Andreas Zeller** — Connection: use this figure to connect debugging workflow, symptom/proximate/root cause, breakpoints, stepping, object inspection, and AI debugging phase gate to the deeper lineage of programming languages, software design, computing practice, or professional judgment. Selection criteria: Wikipedia-accessible; final portrait pass should verify date/eligibility and avoid repeating figures across chapters. Example prompt: "Imagine Andreas Zeller reviewing a student's INFO 5100 project for debugging workflow, symptom/proximate/root cause, breakpoints, stepping, object inspection, and AI debugging phase gate. Ask what evidence proves the student understood the design rather than merely accepted generated code."

Diversity note: computing history candidates skew U.S./Western European and male if the drafter uses only canonical language-design figures. Across the full book, preserve substantive candidates such as Grace Hopper, Adele Goldberg, Jean E. Sammet, Frances E. Allen, Margaret Hamilton, and Barbara Liskov where appropriate, and balance them against domain-specific figures for security, testing, UI, and software process.

---

## 6. Pedagogical Delivery Research

The target reader knows basic programming ideas from Python, R, or a prior scripting context, but does not yet have Java, OO design, debugging discipline, or a reliable way to supervise AI-generated code. Prior knowledge required for this chapter should be stated as capabilities from earlier modules, not as generic "knows programming."

Common misconceptions include "if it compiles, it works," "AI writes better code than I can," "debugging means reading error messages," and "OO is just Java syntax." The strongest delivery sequence is: run or inspect a concrete artifact, predict behavior, introduce vocabulary, work a library example, transfer to inventory/scheduling variants, then ask for an AI Use Disclosure that names what the student verified.

Known teaching failure modes are syntax-first lectures without running examples, letting AI produce complete answers before students can inspect them, and treating the threaded project as a set of disconnected labs. Students who understand the concept can explain the behavior of their own program and identify what evidence would falsify their design. Students who merely memorize can reproduce definitions but cannot debug, adapt, or reject plausible generated code.

---

## 7. Representation and Display Research

A debugging workflow diagram should show symptom → hypothesis → isolation → test → fix or revise hypothesis, with AI allowed only after the hypothesis is stated.

---

## 8. Open Questions and Research Gaps

- Aging risk: Low for methodology; medium for NetBeans debugger UI steps.
- Verify current JDK, NetBeans, JavaFX, Scene Builder, JUnit, and AI-tool instructions before each offering.
- Replace illustrative course-lab cases with documented student artifacts after the course has run, with permission and anonymization.
- Confirm whether the EDGE/Coursera gradebook, AI Use Disclosure form, and CLAUDE.md format match the final course deployment.
- Avoid overclaiming: compilation, passing tests, and AI fluency are evidence, but none alone proves the application satisfies requirements.

---

## 9. Sourcing Notes

Use official Java, OpenJFX, NetBeans, Scene Builder, and JUnit documentation for tool and API claims. Use Java books and OO design texts for durable conceptual explanation. Use AI coding-assistant research only for claims about observed assistance, usability, or risk; do not cite vendor marketing as evidence. Many sources are books or standards and may require library access for page-level citations.