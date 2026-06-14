# Module 0 — Welcome: Wonder Edition
## Companion Chapter

> **Wonder Edition:** Read this alongside the chapter, not instead of it.

---

## The Strange Question

A student installs Java, opens an IDE, and clicks Run. The program executes. Three weeks later, on a different project, the same student sees an error. They spend an hour debugging their class definition. The class definition is fine.

Nothing in their code changed. The environment changed — and they have no way to see it, because they never looked at the environment to begin with.

Here is the puzzle: two students can produce identical console output from Hello World, yet one of them has a verified environment and the other has only a belief. What is the difference between those two states, and why does it matter exactly when the semester grows harder?

---

## First Intuition

Most learners treat setup as a binary outcome. Either the program runs or it does not. If it runs, setup is done. This intuition comes from everyday software installation: you install an app, the app opens, the installation succeeded. Cause and effect are immediate and visible.

Applied to a development environment, this feels equally reasonable. The IDE opens. Hello World prints. Setup is complete.

**Before reading further:** Predict what a learner using this intuition will do the first time a second project fails. Will they check the environment, or will they check the code? Write down your answer.

---

## The Surprise

But a Java development environment is not a single thing. It is three overlapping layers — toolchain, project, and program — and each layer can fail independently of the others.

A JRE installation lets Hello World run without a JDK present. Hello World succeeds. The compiler is missing. The output is real. The absence is invisible until the student tries to compile something the IDE cannot shortcut around.

The running program did not verify the environment. It only verified one narrow path through the environment, at one moment, for one project template.

**Stop here:** If the same output can come from a verified environment and an unverified one, what exactly does a successful run confirm? Hold that question as you read the next section.

---

## The Hidden Structure

Therefore, the distinction the chapter builds is not between broken and working. It is between belief and evidence.

A **belief-based verification** treats a successful run as proof. A **evidence-based verification** treats output as data and asks: what layer produced this, and can I inspect it directly?

The toolchain layer holds the JDK and JVM. The project layer holds the directory structure and build configuration NetBeans creates. The program layer holds the Java source code. Each layer has specific artifacts that can be inspected: `javac --version` for the toolchain, the `.class` file on disk for the project layer, compile errors for the program layer.

The diagnostic habit is not running the program and hoping. The diagnostic habit is identifying which layer a failure lives in before beginning to debug.

**Misconception Checkpoint:** It is tempting to think that if the program compiles and runs, the environment must be correctly configured. But a JRE-only installation can allow certain compilation paths to succeed while silently disabling others. The correct model holds that a verified environment requires direct inspection of each layer's artifacts — not inference from program output alone.

---

## Try Looking At It This Way

**Target:** The three-layer diagnostic model for a Java environment.

**Base:** A building inspector examining a newly constructed house.

**Base features:** A house inspector does not light a candle to test whether the electrical system works. They open the panel, read the breaker labels, check wire gauges, and confirm each circuit terminates correctly. A candle burning confirms the room is not completely dark. It does not confirm the wiring is safe.

**Shared relational structure:** In both the house and the Java environment, a surface-level output (the candle lights, the program runs) can coexist with deep structural failures (faulty wiring, a missing compiler). The inspector's method is layer-specific: each system has its own artifacts, and each artifact requires its own inspection protocol.

The Java developer who runs `javac --version` separately from `java --version` is doing what the inspector does when they test the electrical panel independently from the plumbing. The systems share a building, but they fail independently.

**Mapping to Java:** `java --version` is the plumbing test. `javac --version` is the electrical test. Running Hello World is lighting the candle. The checklist is the inspection protocol.

**Conclusions:** Evidence-based verification means inspecting each layer's specific artifact directly — not inferring one layer's health from another layer's output.

---

## Where The Analogy Breaks

Unlike a building inspection, which is a one-time certification event, a Java environment changes across a semester. New projects use different templates. The IDE may point at a different JDK after an operating system update. A classmate's code may reference a version-specific API.

The building inspector analogy suggests that verification happens once and stays true. Java environment verification does not work that way. A verified environment at Module 0 is not a verified environment at Module 6. This matters because a student who treats the Module 0 checklist as a permanent certification will not notice when the environment drifts — and environment drift is exactly the failure mode the chapter describes in the three-week-later scenario.

The diagnostic habit is not a checklist completed once. It is a repeated practice triggered whenever behavior diverges from expectation.

---

## Small Discovery

Here are four terminal sessions. Each session ran two commands: `java --version` and `javac --version`. Here are the outputs, with no labels or explanations:

**Session A:**
```
java 17.0.9
javac 17.0.9
```

**Session B:**
```
java 17.0.9
'javac' is not recognized as an internal or external command
```

**Session C:**
```
java 11.0.21
javac 17.0.9
```

**Session D:**
```
java 17.0.9
javac 17.0.9 (build 17.0.9+9-LTS)
```

Look at these four outputs. Do not read ahead.

**Pattern search:** Which sessions show alignment between the two commands? Which sessions show a discrepancy? Is there more than one type of discrepancy?

**Prediction:** Rank these four sessions from most to least likely to cause a failure the student would misattribute to their code rather than their environment. Write down your ranking before continuing.

**Revelation:** Session B has a JRE but no JDK. The student can run programs others compiled but cannot compile their own. Session C has two Java installations: the runtime is version 11, the compiler is version 17. NetBeans may pick either one depending on project configuration — and the choice may differ between projects. Session A and Session D are both verified, though Session D includes build metadata that Session A omits. The most dangerous session is not B — it fails immediately and visibly. The most dangerous session is C, because it succeeds often enough to build false confidence, then fails in ways that look like programming errors.

---

## What This Changes

A learner who has worked through this chapter can now distinguish between a program that ran and an environment that is verified. They can look at two identical Hello World outputs and identify which one came from an inspected environment and which came from an assumed one.

They can also apply the three-layer model to any unexpected failure: the first question is not "what is wrong with my code?" but "which layer is this failure in?" That question cuts the diagnostic surface before a single line of code is examined.

The question this module prepares the learner to take up next is structural: once the environment is verified, what does a Java program actually model, and why does it take the shape it does? Module 1 begins with the first class definition — not Hello World ceremony, but a deliberate choice about how the language organizes programs around objects and their relationships. A verified toolchain is the prerequisite for that question to be answerable without interruption.

---

## Wonder Questions

1. If two students submit identical Hello World output as evidence of a working environment, and one has a JDK while the other has only a JRE, what additional artifact — inspectable without running any program — would distinguish their environments? What does the existence of that artifact tell you about what verification actually certifies?

2. The chapter argues that a student who "trusted the output without understanding what produced it" created the conditions for a later failure. But every program produces output the programmer did not generate by hand. At what point does trusting output become engineering judgment, and at what point does it become unverified delegation? What is the distinguishing criterion?

3. The three-layer model separates toolchain failures from project failures from program failures. But the chapter also describes a failure that requires a specific project template combined with a specific NetBeans behavior. Which layer does that failure live in? What does your answer reveal about whether the three-layer model is a description of reality or a tool for organizing inquiry?

4. The AI boundary rule in the chapter says: only accept AI suggestions that give you something you can inspect and verify yourself. A student applies this rule strictly and rejects all AI suggestions that do not produce a verifiable output. What category of AI assistance does this rule exclude that might still be legitimate? Is the rule too strict, or is the restriction load-bearing?

5. Suppose a student completes the five-item verification checklist, submits the evidence packet, and receives full credit — but their JDK version is 11 while the course requires 17. The checklist did not catch this. Which checklist item is incomplete, and what would make that item sufficient rather than merely necessary?

---

**Precision Summary**

The core concept of this module is **evidence-based verification**: the practice of inspecting each layer of a development environment through its specific artifacts rather than inferring layer health from program output.

This concept explains why identical program output can coexist with fundamentally different environment states, why failures appear weeks after setup rather than immediately, and why the diagnostic question "which layer is this in?" cuts debugging time before any code is examined.

This concept does not mean that running a program is useless as a check. Running the program verifies the program layer. It does not verify the toolchain layer or the project layer. Each layer requires its own artifact.

This concept prepares the learner to ask the structural question that opens Module 1: once the toolchain is verified and the project layer is clean, what is a Java program actually modeling — and what decisions by the language designers produced the shape that even Hello World already carries?
