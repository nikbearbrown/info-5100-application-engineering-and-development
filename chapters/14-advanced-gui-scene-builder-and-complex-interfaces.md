# Module 12: Advanced GUI: Scene Builder and Complex Interfaces

**One-line:** Students learn to use Scene Builder to design complex interfaces while maintaining a clean boundary between the visual design and the application logic.

## Module Overview

By the end of this module, you will add one concrete capability to the semester project: the chapter keeps visual design and controller logic connected but separate. The library example is the main path through the text. Inventory and healthcare scheduling follow the same design shape in the exercises.

## Prerequisites

Module 11 event handling and MVC discipline.

## Learning Objectives

- (Apply) Design a multi-screen interface using Scene Builder.
- (Analyze) Explain how FXML relates to JavaFX code.
- (Apply) Connect FXML to a controller using `@FXML`.
- (Evaluate) Assess a Scene Builder design against the Module 3 user flow.

## Opening Case

The screen flow from Module 3 returns. It worked on paper, then in hand-written JavaFX. Now a visual editor can rearrange the interface. The question is whether the controller still connects to the same model decisions.

Do not define the concept too early. First, look at the failure. The point of the opening is to make the need for the concept visible before the word for it arrives.

## Core Content

### The Idea In Plain Language

FXML is a representation of a JavaFX object graph. Scene Builder changes how the view is authored, not who owns the behavior. The controller remains the boundary where visual components become application actions.

### The Java Move

In Java, this idea becomes a concrete design move in source code. The student should be able to point to the class, method, field, collection, handler, test, or configuration line that carries the concept. If the concept cannot be found in code, it is still only a slogan.

### The AI Boundary

AI may generate controller stubs from provided FXML. It may not invent FXML for an unspecified workflow or implement handlers.

The boundary matters because the book's thesis is not anti-AI. It is anti-unverified delegation. The student may use AI when the task is appropriate and when the verification responsibility is still held by the engineer.

<!-- → [FIGURE: FXML to controller mapping table for Module 12, showing the core concept, the Java artifact that carries it, the AI assistance boundary, and the human verification step.] -->

## Worked Example

**Situation.** The checkout screen is redesigned in Scene Builder. The FXML declares `checkoutButton` and `bookTable`. The controller has matching `@FXML` fields and handler stubs. Every `fx:id` must be traceable.

**Analysis.** Work from observable behavior back to design intent. Name the object, method, handler, collection, file, or test involved. Then name what would count as evidence that the implementation is correct.

**Dead end.** The usual dead end is accepting code because it runs once, compiles cleanly, or matches an AI explanation. That is not enough. The student's job is to connect behavior to a requirement and then to a verifiable Java artifact.

**Resolution.** The implementation is accepted only when the student can trace the behavior, explain the design choice, and identify what AI did and did not decide.

<!-- → [TABLE: Module 12 verification table with columns: concept, Java artifact, what AI may do, what the student must verify, evidence before submission; rows should include the library example plus inventory and scheduling variants.] -->

**The lesson:** the engineer owns the explanation, not just the output.

**The limit:** this module gives a disciplined slice of practice; it does not make every downstream design decision automatic.

## Mid-Module Checkpoint

Before starting the lab, answer three questions in writing:

1. What is the specific project behavior this module adds?
2. Which Java artifact carries that behavior?
3. What evidence would convince you the behavior works for your requirements?

If any answer is vague, return to the worked example and make the artifact concrete.

## Lab Assignment

Redesign one project screen in Scene Builder and submit an FXML-controller mapping table.

The lab must include running evidence, a short explanation of the design choice, and the AI Use Disclosure described below.

## How To Use AI

**What AI does well here:** AI may generate controller stubs from provided FXML. It may not invent FXML for an unspecified workflow or implement handlers.

**Concrete prompt that works:**

```text
I am working on Module 12: Advanced GUI: Scene Builder and Complex Interfaces in INFO 5100.
My domain is [library / inventory / scheduling].
My current specification is: [paste your written specification].
Help only within this boundary: AI may generate controller stubs from provided FXML. It may not invent FXML for an unspecified workflow or implement handlers.
Do not produce work that violates the phase gate: For every `@FXML` field and handler, trace the FXML element, run the app, and verify the connection.
```

**What AI cannot do here:** AI cannot know your business requirement, your instructor's acceptance standard, or whether the generated code fits the whole project. It can help with language, scaffolding, explanation, or candidate implementations only after you have stated what must be true.

**Phase gate:** For every `@FXML` field and handler, trace the FXML element, run the app, and verify the connection.

**Module CLAUDE.md constraint:**

```text
You are assisting a graduate Java student in Module 12: Advanced GUI: Scene Builder and Complex Interfaces.
Follow the module phase gate exactly.
Explain before generating. Mark every design decision.
If a requirement is missing, ask for it instead of guessing.
Never let plausible Java substitute for verified Java.
```

## AI Use Disclosure Form

Complete this paragraph for the lab:

> I used AI for [specific task]. My prompt was [summary or pasted prompt]. I verified [specific Java artifact or behavior] by [running, tracing, debugging, testing, or inspection]. The AI output was wrong or incomplete in this way: [specific issue]. The part I did not delegate was [design or verification judgment].

## Common Misconceptions

**If it compiles, it works.** Compilation checks whether Java accepts the form. It does not prove the behavior matches the requirement.

**If AI explains it, I understand it.** Understanding means you can predict, trace, change, and defend the code without repeating the AI's phrasing.

**The lab is the code.** The lab is the code plus the explanation, verification evidence, and AI disclosure. The artifact is proof that a process happened.

## Exercises

1. **Apply:** Add the module capability to the library version of the project.
2. **Apply:** Translate the same capability to either inventory or scheduling.
3. **Analyze:** Identify one failure mode that would pass a superficial run but violate the requirement.
4. **Evaluate:** Ask AI for help within the allowed boundary, then reject or revise at least one part of the output and explain why.

## What Would Change My Mind

I would revise this module's central claim if classroom evidence showed that students who used unrestricted AI generation could explain, debug, adapt, and defend their project code as well as students who passed through the module's phase gate. The evidence would need to include transfer to a new feature, not only successful completion of the same lab.

## Still Puzzling

- How much tool assistance improves confidence without reducing ownership?
- Which errors in this module are productive learning moments, and which are avoidable friction?
- How should the instructor distinguish weak Java syntax from weak design reasoning?
- What project evidence should become part of the instructor manual after the next course run?

## Module Summary

You can now the chapter keeps visual design and controller logic connected but separate. You also have one more AI boundary: not a ban, but a rule for keeping verification in the student's hands.

## Key Terms

- **Scene Builder:** define this term in the context of the semester project before using it in lab work.
- **FXML:** define this term in the context of the semester project before using it in lab work.
- **fx:id:** define this term in the context of the semester project before using it in lab work.
- **@FXML:** define this term in the context of the semester project before using it in lab work.
- **controller:** define this term in the context of the semester project before using it in lab work.
- **injection:** define this term in the context of the semester project before using it in lab work.
- **layout:** define this term in the context of the semester project before using it in lab work.

## Bridge Question

The interface is connected. How do you prove the behavior still works after changes?

## Further Reading

- Java Language Specification and Java SE API documentation: use for language and library facts.
- Robins, Rountree, and Rountree, "Learning and Teaching Programming": use for common novice difficulties.
- OpenJFX documentation: use for JavaFX, FXML, and event-handling details.

## CLI Quick Reference

```bash
java --version
javac --version
# Run from your project directory when checking environment and compiled output.
```

## Sources and Drafting Notes

Research base: Java Language Specification and Java SE API; OpenJFX and NetBeans documentation where relevant; Robins, Rountree, and Rountree on programming education; Sweller on cognitive load; Collins, Brown, and Newman on cognitive apprenticeship; Peng et al., Vaithilingam et al., and Pearce et al. on AI coding assistance and verification risk.

Current tool instructions, version-specific setup, and AI platform behavior require pre-offering verification. [verify]

---

## Prompts

Use these prompts with Claude to generate interactive D3 v7 versions of the
figures in this chapter. Each produces a standalone HTML file you can open
in a browser and modify freely.

**Prerequisites:** Load `brutalist/CLAUDE.md` and `brutalist/DESIGN.md` into
your Claude project context before using these prompts. They define the stack,
naming conventions, color system, and typography the figures use.
