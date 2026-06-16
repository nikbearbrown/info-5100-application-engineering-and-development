# Module 0 — Welcome: Wonder Edition
## Companion Chapter

> **Wonder Edition:** Read this alongside the chapter, not instead of it.

> **Content note:** Despite the title "Welcome," this chapter covers environment verification, the JDK/JRE distinction, and a three-layer diagnostic model for Java development. This companion follows the actual chapter content.

## The Strange Question

A student runs Hello World. It prints. Three weeks later, that same student creates a second project and sees a compile error. They spend an hour debugging their class definition. The class definition is correct.

Here is the specific observable fact that makes this hard: both states — verified environment and phantom-broken environment — produce the same console output on day one.

What does a successful `Hello World` run actually prove, and what precise evidence would it take to prove something more?

## First Intuition

Consumer software trains a specific mental model: installation either works or it does not. The app opens or it crashes. There is no third state.

That model comes from a real experience — installing a browser, a game, a productivity tool. In those cases, a single launch confirms the install. Cause and effect are immediate, visible, and complete.

Applied to a Java development environment, the same logic feels sound. The IDE opens. Hello World prints. Setup must be complete.

> **► Planning prompt:** Before reading further, write down your current mental model of what "setup is done" means. What prior experience is that model drawn from? Predict specifically: if a second project fails three weeks later, where will you look first — the code or the environment? Write your answer before continuing.

## The Surprise

But a Java development environment is not a single installable thing. It is three overlapping layers, each capable of failing independently of the others.

Consider this specific terminal output from a real machine:

```
$ java --version
java 17.0.9 2023-10-17 LTS

$ javac --version
'javac' is not recognized as an internal or external command
```

Both commands ran on the same machine, same terminal session, same minute. The runtime is present. The compiler is absent. Hello World can execute because NetBeans cached a prior compilation — but no new source file can be compiled. The environment looks working. The compiler is missing.

The successful run did not certify the environment. It certified one narrow path through the environment, for one project template, at one moment.

> **► Monitoring prompt:** What did your prediction assume about the relationship between "program runs" and "environment is verified"? What does this output contradict? What does your original model still fail to explain about why the failure appears three weeks later rather than immediately?

## The Hidden Structure

Therefore, the chapter's core move is not describing setup steps. It is replacing a binary model — working or broken — with a layered one.

The **toolchain layer** holds the JDK, the JVM, and the PATH configuration. Its specific inspectable artifact is the output of two commands: `java --version` and `javac --version`. If both return the same version, the toolchain layer is verified. If one returns "command not found," the layer has a gap.

The **project layer** holds the directory structure NetBeans creates: the `src` folder, the build folder, and the `.class` file produced by compilation. Its artifact is the compiled bytecode file on disk — findable in a file explorer without opening the IDE.

The **program layer** holds the Java source code. Its artifacts are compile errors and runtime errors — the layer most students examine first, and the wrong layer to examine when the failure lives above it.

**Misconception Checkpoint:**
> "It is tempting to think that if a program compiles and runs, the environment must be correctly configured. But a JRE-only installation can allow certain execution paths to succeed — including cached compilations — while silently missing the compiler `javac` entirely. The correct model holds that environment verification requires direct artifact inspection of each layer separately. The key distinction is between *inferring* a layer's state from downstream output versus *inspecting* that layer's own specific artifact."

**Code Trace — Two Commands, Two Layers:**

```bash
# Toolchain layer: inspect both artifacts separately
$ java --version
java 17.0.9

$ javac --version
javac 17.0.9
```

Both return version 17.0.9. Both artifacts match. The toolchain layer is now verified — not assumed. A student who runs only `java --version` and stops has verified the runtime but left the compiler uninspected. That gap is the JRE-without-JDK failure.

## Try Looking At It This Way

**Target:** The three-layer diagnostic model for a Java development environment.

**Base:** A building inspector examining a newly constructed house before occupancy.

**Features:**
- The inspector tests electrical, plumbing, and structural systems as separate domains, each with its own protocol
- Each system has specific testable artifacts: circuit breakers, pipe pressure, load-bearing measurements
- A working lamp in the living room does not certify the electrical panel is safely wired — it only confirms current reached the bulb

**Commonalities:**
A lamp that lights confirms electricity reached the socket. It does not confirm that the circuit is correctly rated, that the breaker panel is properly labeled, or that the wiring terminates safely. The output is real; the inference about the underlying system is unsupported. This maps directly onto `Hello World` running: the output is real, but the inference that the compiler, the JDK, and the project structure are all correctly configured is unsupported. In both domains, each system requires inspection of its own artifacts — the breaker panel, not the lamp; `javac --version`, not just the console output.

**Boundaries:**
A house inspection is a one-time certification event. A building passes or fails and then holds that status. A Java development environment does not. It changes across a semester: new project templates, IDE updates that repoint the JDK, version-specific API calls in copied code. The analogy is most useful for understanding why layer-specific inspection matters. It fails as a model for how often verification must happen.

**Conclusions:**
Evidence-based verification means inspecting each layer through its own artifact rather than inferring one layer's health from another layer's output. The diagnostic habit transfers across every module, not just setup.

## Where The Analogy Breaks

Unlike a building inspection, which certifies a structure at a fixed point in time, a Java development environment is not static.

> "Unlike a building that holds its certified state after inspection, a Java environment does not hold its verified state across a semester. This matters because a student who treats the Module 0 checklist as a permanent certification will not notice when the environment drifts — and environment drift is exactly what produces the three-week-later failure the chapter describes."

A new project template changes the project layer. An OS update can repoint the IDE to a different JDK. A pasted code snippet may use a version-specific API unavailable in the installed JDK. Each of these changes a layer without touching the others. The inspection habit is not a checklist completed once. It is a repeated practice triggered whenever observed behavior diverges from expected behavior.

## Small Discovery

Here are raw terminal outputs from four machines. No labels. No explanations. Read them as data.

**Machine A:**
```
java 17.0.9
javac 17.0.9
```

**Machine B:**
```
java 17.0.9
'javac' is not recognized as an internal or external command
```

**Machine C:**
```
java 11.0.21
javac 17.0.9
```

**Machine D:**
```
java 17.0.9
javac 17.0.9 (build 17.0.9+9-LTS)
```

**Pattern search:** Which machines show alignment between the two commands? Which show a discrepancy? Is there more than one type of discrepancy, or is every mismatch the same kind of problem?

**Guided prediction:** Rank these four machines from most likely to least likely to produce a failure the student would misattribute to their code. What changes if Machine C is the one that runs Hello World successfully on day one? Write your ranking and your reasoning before continuing.

---

**Revelation:** Machine B has a JRE but no JDK. The compiler is absent. This failure is loud and immediate — the student cannot compile anything. Machine C has two Java installations: the runtime is version 11, the compiler is version 17. NetBeans may select either depending on project configuration, and that selection may differ between projects. Machine A and Machine D are both verified; Machine D includes build metadata that Machine A omits, but both pass inspection. The most dangerous machine is not B. The most dangerous machine is C, because it compiles and runs often enough to build false confidence, then fails in ways that look exactly like programming errors — wrong method signature, unexpected behavior, missing API. The concept at work is **layer-specific artifact inspection**: the discrepancy in Machine C is only visible when both commands are run and their outputs compared directly.

## What This Changes

A reader who has worked through this chapter can now answer a question that was previously unresolvable: given two students with identical Hello World output, which one has a verified environment? The answer requires naming which artifacts are present and which are uninspected — not which program ran.

In a specific piece of code or design decision, this changes how the first error of a new project is approached. The first question is no longer "what is wrong with my class?" It is "which layer is this failure in?" — a question that cuts the diagnostic surface before a single line of source is examined.

**Practice Bridge:** After running Hello World in NetBeans, close the IDE and navigate to the project folder in the file explorer. Locate the `src` directory and the compiled `.class` file inside `build/classes` or `target/classes`. Write down the full file path of each. If either is missing, return to the chapter's First Project section and identify which verification step was skipped. This is not a reading exercise — it is the act of inspecting the project layer's specific artifact.

The question this chapter leaves open is the one it explicitly names: once the toolchain is verified and the project layer is clean, what is a Java program actually modeling? Hello World already has a class, a method, and an entry point. That structure is not arbitrary. Module 1 begins with the first class definition for a real domain — and the question of why that structure exists.

## Wonder Questions

1. A student submits `java --version` output as evidence of a working environment but does not submit `javac --version` output. What specific failure mode remains possible — and what is the minimum additional artifact that would rule it out without running any program?

2. The chapter's AI boundary rule states: only accept AI suggestions that give you something you can inspect and verify yourself. A suggestion to "run `javac --version` to confirm the JDK is installed" passes this test. A suggestion to "switch to a Maven project" does not. What makes the first verifiable and the second not? Is the criterion about what the AI knows, or about what the student can inspect?

3. The three-layer model separates toolchain failures from project failures from program failures. But the chapter describes a failure that requires a specific project template combined with a specific NetBeans behavior. Which single layer does that failure belong to — and what does your answer reveal about whether the three-layer model describes reality or organizes inquiry?

4. Suppose a student runs both version commands, finds matching versions, locates the `.class` file on disk, and submits a complete evidence packet — but their JDK is version 11 and the course requires version 17. Which of the five checklist items is incomplete? What would make that item sufficient rather than merely present?

5. The chapter distinguishes between "trusted the output without understanding what produced it" and engineering judgment. Every program eventually produces output the programmer did not generate by hand. At what point does trusting output become legitimate inference, and at what point does it become unverified delegation? What is the precise criterion that separates them?

---

**Precision Summary**

> **What the concept is:** Evidence-based verification is the practice of inspecting each layer of a Java development environment — toolchain, project, program — through that layer's own specific artifacts, rather than inferring one layer's state from another layer's output.
>
> **What it explains:** Why a successful Hello World run coexists with a missing compiler; why environment failures appear weeks after setup rather than immediately; why the diagnostic question "which layer is this in?" reduces debugging time before any source code is examined.
>
> **What it does NOT mean:** Running a program is useless as a check. Running the program verifies one path through the program layer. It does not verify the toolchain layer or the project layer, each of which requires its own artifact inspection.
>
> **What comes next:** Once the toolchain is verified and the project layer is confirmed, the open question is structural — what is a Java program actually modeling, and why does even Hello World already have the shape it has? That question opens Module 1.
