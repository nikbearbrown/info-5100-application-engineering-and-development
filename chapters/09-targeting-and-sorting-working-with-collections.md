# Module 9: Targeting and Sorting: Working with Collections

**One-line:** Students learn to sort, filter, and search collections of objects - and to choose the right collection type for each task.

## Module Overview

By the end of this module, you will add one concrete capability to the semester project: the chapter connects collection type to access-pattern reasoning and performance consequences. The library example is the main path through the text. Inventory and healthcare scheduling follow the same design shape in the exercises.

## Prerequisites

Module 8 persistent collections and CRUD operations.

## Learning Objectives

- (Apply) Implement sorting using Comparator and Comparable.
- (Analyze) Choose between List, Map, and Set for collection tasks.
- (Apply) Implement search and filter operations.
- (Evaluate) Assess AI-generated sorting for correctness and performance.

## Opening Case

Five hundred books need to be sorted by title, then author, then year. The first solution sort-of works. The second solution names the ordering rule. That difference matters when the rule changes.

Do not define the concept too early. First, look at the failure. The point of the opening is to make the need for the concept visible before the word for it arrives.

## Core Content

### The Idea In Plain Language

Collections are design choices. `List`, `Map`, and `Set` do not just store things. They express access patterns: ordered display, keyed lookup, uniqueness, iteration, and membership.

### The Java Move

In Java, this idea becomes a concrete design move in source code. The student should be able to point to the class, method, field, collection, handler, test, or configuration line that carries the concept. If the concept cannot be found in code, it is still only a slogan.

### The AI Boundary

AI may write a comparator from a precise ordering rule. It may not choose the collection type before the student names common operations.

The boundary matters because the book's thesis is not anti-AI. It is anti-unverified delegation. The student may use AI when the task is appropriate and when the verification responsibility is still held by the engineer.

<!-- → [FIGURE: collection choice matrix for Module 9, showing the core concept, the Java artifact that carries it, the AI assistance boundary, and the human verification step.] -->

## Worked Example

**Situation.** The library uses `List<Book>` for display order and `Map<String, Book>` for ISBN lookup. A comparator sorts by title and author. A filter returns only available books.

**Analysis.** Work from observable behavior back to design intent. Name the object, method, handler, collection, file, or test involved. Then name what would count as evidence that the implementation is correct.

**Dead end.** The usual dead end is accepting code because it runs once, compiles cleanly, or matches an AI explanation. That is not enough. The student's job is to connect behavior to a requirement and then to a verifiable Java artifact.

**Resolution.** The implementation is accepted only when the student can trace the behavior, explain the design choice, and identify what AI did and did not decide.

<!-- → [TABLE: Module 9 verification table with columns: concept, Java artifact, what AI may do, what the student must verify, evidence before submission; rows should include the library example plus inventory and scheduling variants.] -->

**The lesson:** the engineer owns the explanation, not just the output.

**The limit:** this module gives a disciplined slice of practice; it does not make every downstream design decision automatic.

## Mid-Module Checkpoint

Before starting the lab, answer three questions in writing:

1. What is the specific project behavior this module adds?
2. Which Java artifact carries that behavior?
3. What evidence would convince you the behavior works for your requirements?

If any answer is vague, return to the worked example and make the artifact concrete.

## Lab Assignment

Implement three sort orders and one search/filter feature. Identify one collection choice in the project and justify it by expected operations.

The lab must include running evidence, a short explanation of the design choice, and the AI Use Disclosure described below.

## How To Use AI

**What AI does well here:** AI may write a comparator from a precise ordering rule. It may not choose the collection type before the student names common operations.

**Concrete prompt that works:**

```text
I am working on Module 9: Targeting and Sorting: Working with Collections in INFO 5100.
My domain is [library / inventory / scheduling].
My current specification is: [paste your written specification].
Help only within this boundary: AI may write a comparator from a precise ordering rule. It may not choose the collection type before the student names common operations.
Do not produce work that violates the phase gate: List the three most common operations and expected size before AI generates collection code.
```

**What AI cannot do here:** AI cannot know your business requirement, your instructor's acceptance standard, or whether the generated code fits the whole project. It can help with language, scaffolding, explanation, or candidate implementations only after you have stated what must be true.

**Phase gate:** List the three most common operations and expected size before AI generates collection code.

**Module CLAUDE.md constraint:**

```text
You are assisting a graduate Java student in Module 9: Targeting and Sorting: Working with Collections.
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

You can now the chapter connects collection type to access-pattern reasoning and performance consequences. You also have one more AI boundary: not a ban, but a rule for keeping verification in the student's hands.

## Key Terms

- **List:** define this term in the context of the semester project before using it in lab work.
- **Map:** define this term in the context of the semester project before using it in lab work.
- **Set:** define this term in the context of the semester project before using it in lab work.
- **Comparator:** define this term in the context of the semester project before using it in lab work.
- **Comparable:** define this term in the context of the semester project before using it in lab work.
- **filter:** define this term in the context of the semester project before using it in lab work.
- **stream:** define this term in the context of the semester project before using it in lab work.
- **complexity:** define this term in the context of the semester project before using it in lab work.

## Bridge Question

The data is organized. How does it appear in a GUI?

## Further Reading

- Java Language Specification and Java SE API documentation: use for language and library facts.
- Robins, Rountree, and Rountree, "Learning and Teaching Programming": use for common novice difficulties.
- Peng et al. and Vaithilingam et al.: use for cautious claims about AI coding assistance and verification.

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
