# Module 11: Event-Driven Programming: Making the Application Respond

**One-line:** Students learn to connect user actions to application behavior using JavaFX event handling - and to maintain the model-view separation under the pressure of deadline.

## Module Overview

By the end of this module, you will add one concrete capability to the semester project: the chapter makes user actions traceable through event, handler, model update, and view refresh. The library example is the main path through the text. Inventory and healthcare scheduling follow the same design shape in the exercises.

## Prerequisites

Module 10 JavaFX view and model-view separation.

## Learning Objectives

- (Apply) Implement event handlers for primary user actions.
- (Analyze) Trace click to model state change to view update.
- (Apply) Use inner classes and lambdas for event handling.
- (Evaluate) Assess handlers for responsibility violations.

## Opening Case

One button handler validates input, updates the model, formats output, refreshes three controls, and writes a file. It works until anything changes. Then no one knows where the behavior lives.

Do not define the concept too early. First, look at the failure. The point of the opening is to make the need for the concept visible before the word for it arrives.

## Core Content

### The Idea In Plain Language

Event-driven programs wait for actions. A handler should translate one event into a small sequence of named responsibilities. The handler is not a closet for all the code the programmer did not know where to put.

### The Java Move

In Java, this idea becomes a concrete design move in source code. The student should be able to point to the class, method, field, collection, handler, test, or configuration line that carries the concept. If the concept cannot be found in code, it is still only a slogan.

### The AI Boundary

AI may generate event registration boilerplate and method-call skeletons. It may not fill business logic bodies.

The boundary matters because the book's thesis is not anti-AI. It is anti-unverified delegation. The student may use AI when the task is appropriate and when the verification responsibility is still held by the engineer.

<!-- → [FIGURE: event trace responsibility diagram for Module 11, showing the core concept, the Java artifact that carries it, the AI assistance boundary, and the human verification step.] -->

## Worked Example

**Situation.** Clicking Checkout calls `validateSelection()`, `performCheckout()`, `refreshCatalogView()`, and `showConfirmation()`. Each method owns one responsibility and can be tested or inspected separately.

**Analysis.** Work from observable behavior back to design intent. Name the object, method, handler, collection, file, or test involved. Then name what would count as evidence that the implementation is correct.

**Dead end.** The usual dead end is accepting code because it runs once, compiles cleanly, or matches an AI explanation. That is not enough. The student's job is to connect behavior to a requirement and then to a verifiable Java artifact.

**Resolution.** The implementation is accepted only when the student can trace the behavior, explain the design choice, and identify what AI did and did not decide.

<!-- → [TABLE: Module 11 verification table with columns: concept, Java artifact, what AI may do, what the student must verify, evidence before submission; rows should include the library example plus inventory and scheduling variants.] -->

**The lesson:** the engineer owns the explanation, not just the output.

**The limit:** this module gives a disciplined slice of practice; it does not make every downstream design decision automatic.

## Mid-Module Checkpoint

Before starting the lab, answer three questions in writing:

1. What is the specific project behavior this module adds?
2. Which Java artifact carries that behavior?
3. What evidence would convince you the behavior works for your requirements?

If any answer is vague, return to the worked example and make the artifact concrete.

## Lab Assignment

Implement handlers for three user actions. Decompose one handler that has more than one responsibility.

The lab must include running evidence, a short explanation of the design choice, and the AI Use Disclosure described below.

## How To Use AI

**What AI does well here:** AI may generate event registration boilerplate and method-call skeletons. It may not fill business logic bodies.

**Concrete prompt that works:**

```text
I am working on Module 11: Event-Driven Programming: Making the Application Respond in INFO 5100.
My domain is [library / inventory / scheduling].
My current specification is: [paste your written specification].
Help only within this boundary: AI may generate event registration boilerplate and method-call skeletons. It may not fill business logic bodies.
Do not produce work that violates the phase gate: Write the action sequence in plain English before generating a handler.
```

**What AI cannot do here:** AI cannot know your business requirement, your instructor's acceptance standard, or whether the generated code fits the whole project. It can help with language, scaffolding, explanation, or candidate implementations only after you have stated what must be true.

**Phase gate:** Write the action sequence in plain English before generating a handler.

**Module CLAUDE.md constraint:**

```text
You are assisting a graduate Java student in Module 11: Event-Driven Programming: Making the Application Respond.
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

You can now the chapter makes user actions traceable through event, handler, model update, and view refresh. You also have one more AI boundary: not a ban, but a rule for keeping verification in the student's hands.

## Key Terms

- **event:** define this term in the context of the semester project before using it in lab work.
- **handler:** define this term in the context of the semester project before using it in lab work.
- **registration:** define this term in the context of the semester project before using it in lab work.
- **lambda:** define this term in the context of the semester project before using it in lab work.
- **inner class:** define this term in the context of the semester project before using it in lab work.
- **responsibility:** define this term in the context of the semester project before using it in lab work.
- **model update:** define this term in the context of the semester project before using it in lab work.

## Bridge Question

Handlers work. How do you build more complex interfaces without tangling layout and logic?

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
