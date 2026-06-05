# Worked Exercises: Welcome

*Chapter 0 of INFO 5100 Application Engineering and Development*

> These exercises follow a research-backed sequence: full worked example → matched practice → completion problem → error-recognition → transfer → interleaved review. Each section builds on the previous. Do not skip ahead.

---

## Prerequisites

- You understand the **three-layer diagnostic model**: the *toolchain layer* (JDK, JVM, PATH), the *project layer* (NetBeans project structure and template choices), and the *program layer* (your Java source). Most setup failures live in the first two layers, not the third.
- You understand the **JDK vs. JRE** distinction: the JDK contains the compiler (`javac`); the JRE contains only the runtime (`java`). A JRE-only installation can run someone else's `.class` files but cannot compile your own.
- You understand the chapter's central principle — **a working environment is evidence, not belief**. You do not trust that setup worked because the installer said "Setup Complete." You run a command and inspect the output it prints.

---

## Part A — Full Worked Example

**What this demonstrates:** How to use the two verification commands as *evidence* to place a setup symptom into the correct layer of the three-layer model, rather than debugging a phantom in the program layer.

**The problem:** A student creates their NetBeans Java Application project, pastes Hello World, and clicks Run. They get a red error in the output panel that reads, in part, `Compiler not found`. They open Stack Overflow and start reading about Java syntax errors. Before they write a single fix, diagnose the failure: which layer is it in, what is the most likely cause, and what evidence confirms it?

**The solution:**

**Step 1 — Refuse the phantom: ask "what layer is this in?" before "what is wrong with my code?"**
The error appeared *before any interesting code ran* — it fired on the attempt to compile Hello World, a program the student did not really write. Treat the symptom as a layer question first.
*Why:* The chapter's diagnostic habit is "what layer is this failure in?" not "what is wrong with my code?" A compile failure on Hello World — the most trivial program possible — is strong evidence the fault is *below* the program layer.
*Check:* Confirm the error appears even with code you are confident is correct (Hello World). If trivial code fails to compile, the program layer is almost certainly not the culprit.

**Step 2 — Gather toolchain evidence: run both verification commands**
Do not assume. Run both commands and read both outputs:
```bash
java --version
javac --version
```
Suppose the output is:
```
java 17.0.2 2022-01-18 LTS
javac: command not found
```
*Why:* A working environment is evidence, not belief. The two commands ask the system to *produce output we can inspect*. `java` answering and `javac` not answering is the signature pattern the chapter names explicitly.
*Check:* You now have two concrete strings to reason about, not a feeling. If both had returned matching version numbers, the toolchain would be cleared and you would look at the project layer next.

**Step 3 — Read the evidence against the JDK/JRE model**
`java --version` returns a version; `javac --version` says "command not found." Map this to the chapter: the runtime exists, the compiler does not.
*Why:* The JDK contains `javac`; the JRE contains only `java`. A `javac` that is missing while `java` works is the textbook signature of a **JRE-without-JDK** installation — "the JRE-without-JDK problem I just described."
*Check:* The two outputs are *consistent* with exactly one diagnosis. There is no other common cause that makes `java` work while `javac` is absent.

**Step 4 — Place the failure in the correct layer and name the fix domain**
Conclude: this is a **toolchain-layer** failure (missing compiler), not a program-layer failure (bad Java).
*Why:* "command not found" errors and compile failures that appear before any interesting code are the toolchain layer's characteristic signature. Knowing the layer cuts the debugging surface dramatically.
*Check:* The fix is "install a JDK and re-verify," not "edit Hello World." If your proposed fix touches the `.java` file, you have mis-located the layer.

**Final answer:** The failure lives in the **toolchain layer**. The cause is a JRE-only installation: `java --version` reports `17.0.2` but `javac --version` reports `command not found`. The fix is to install a JDK (not a JRE) and re-run both commands until they report the same supported version. No edit to Hello World can resolve this, because the program layer was never the problem.

**What made this work:** The central concept is **evidence-based, layered diagnosis**. The naive approach fails because the student trusted that the symptom (a compile error) named its own cause (bad code). It did not. Setup failures and programming failures produce nearly identical symptoms; the only way to tell them apart is to know what a working toolchain looks like and to run the commands that produce inspectable evidence. The two `--version` commands convert a vague "Java is broken" into a specific, located, fixable fault.

**Self-explanation prompt:** Close the page and write one sentence: what principle did Step 3 rely on, and when would that diagnosis *not* apply (i.e., what output pattern would rule out the JRE-without-JDK explanation)?

---

## Part B — Matched Practice Problem

**Same structure, different surface.** A student runs the two verification commands and gets:
```
java 11.0.16 2022-07-19 LTS
javac 17.0.4
```
Both commands answer, so this is not a JRE-without-JDK problem. Yet NetBeans throws an error the student does not understand when running a program that uses a Java 17 language feature. Diagnose it: which layer is the failure in, what is the most likely cause given the two outputs, and what evidence (from this chapter's commands and checklist) confirms it? Produce a full Step 1–4 diagnosis and a Final answer naming the layer and the fix domain.

**Stuck?** Return to Part A and map each of its steps to your obstacle — especially Step 3, where the two outputs were read *against a model* (there the JDK/JRE model; here the chapter's "multiple Java installations" case where `java` and `javac` differ significantly).

*Instructor note: No worked solution provided for Part B — the point is production, not verification.*

---

## Part C — Completion Problem

**What's missing:** Steps 3 and 4 are removed.

**The problem:** A classmate insists "Java works on my machine — Hello World printed fine in NetBeans." You ask them to close NetBeans and find the compiled `.class` file on disk. They cannot find it, and they cannot tell you the path to their `.java` source file either. Using the three-layer model and the Module 0 verification checklist, diagnose what is and is not actually verified.

**Step 1 — Separate "ran" from "verified" (complete)**
"Hello World printed" establishes that *something* executed and produced output in the output panel — checklist item 4. It does not establish items 2, 3, or 5.
*Why:* A working environment is evidence, not belief. "It printed" is one piece of evidence; the chapter's checklist requires five. Running is not the same as a verified toolchain and project layer.

**Step 2 — Name which checklist items are still open (complete)**
Open items: item 2 (project has a known name and location), item 3 (the `main` entry point can be identified), and item 5 (the source file and compiled `.class` file can be located on disk).
*Why:* The classmate "trusted the output without understanding what produced it." Until the artifacts are located, the project layer is unverified — they do not know what their environment looks like, so they cannot see when it changes.

**Step 3 — [BLANK] Identify which LAYER is unverified and why locating the `.class` file matters**
*Your work here:*
_______________________________________________
_______________________________________________
*Why (your explanation):*
_______________________________________________

**Step 4 — [BLANK] Name the specific forward failure this exposes them to in a later module**
*Your work here:*
_______________________________________________
_______________________________________________
*Why (your explanation):*
_______________________________________________

**Step 5 — Prescribe the remedy (complete)**
Have them re-walk the First Project section: open the project folder, locate the `src` directory and the `.java` file, then the `build`/`dist` `classes` folder and the `.class` file, and write down both full paths.
*Why:* The habit being built is *knowing what the environment looks like* so that when it changes — and it will — they notice. Locating the artifacts converts belief into evidence.

**Final answer:** The classmate has verified only checklist item 4 (visible output). The **project layer** remains unverified because the source and compiled artifacts have never been located. Until they can point to the `.java` and `.class` files on disk, they cannot detect a later structural change (e.g., a different project template in a future module) and will misattribute a project-layer failure to their own code.

**Self-explanation prompt:** Compare your Steps 3–4 to Part A's Steps 3–4. In Part A you placed a failure that had *already manifested*; here you are predicting a failure that *has not happened yet*. What in the verification checklist makes that forward prediction possible?

---

## Part D — Error-Recognition Problem

> **Use this section only after completing Parts A–C.**

**What's wrong:** one error, marked ⚠.

**The problem:** A student gets `error: package does not exist` when running their project. They want to diagnose it with AI and then verify the fix themselves. Here is their process.

**Step 1 — (correct) Place the symptom in a layer**
The error references a *package*, which is part of how NetBeans organizes the project. The student suspects the project layer and notes the program compiled cleanly last week, so the change is recent.
*Why correct:* "class not found / package" errors at build time are characteristic project-layer signatures in the three-layer model.

**Step 2 — (correct) Construct a diagnostic prompt with the required fields**
The student fills in the chapter's prompt template: OS and version, JDK version from `java --version`, NetBeans version, and the exact error message.
*Why correct:* A diagnostic prompt includes enough context (OS, versions, exact error) to get a useful explanation.

**Step 3 ⚠ — Act on every AI suggestion the same way**
The AI returns two suggestions: (a) "run `javac --version` to confirm the JDK is installed and on PATH," and (b) "switch this to a Maven project so dependencies resolve automatically." The student decides both came from the AI, so both are equally trustworthy, and begins converting the project to Maven.
*Why it looks fine:* The Maven suggestion is fluent, confident, and formatted exactly like the correct suggestion — and converting the project does make the immediate error vanish, which looks like success.

**Step 4 — (correct, and that is what makes it dangerous) Observe that the error disappeared**
After the conversion, the `package does not exist` error no longer appears. The student concludes the problem is solved.
*Why this is a trap:* The error vanished, producing a plausible-looking success, while the student silently abandoned the course-required project template — a structural change that will produce hard-to-diagnose incompatibilities in later modules.

**Your tasks:**
1. **Identify and explain the error.** Step 3 treats an AI suggestion that requires a *design decision* as if it were an AI suggestion that requires a *verifiable inspection*. Suggestion (b) — switching to Maven — chooses a different project template, which the chapter states "is outside its authority here": IDE and version (and template) are set by the course, not the AI.
2. **Write the corrected Step 3.** Apply the AI boundary test to each suggestion separately: *does acting on it require you to verify something you can actually verify?* Suggestion (a) is appropriate — run `javac --version` and inspect the output. Suggestion (b) is out of bounds — reject it; the project template belongs to the course structure. Pursue (a), keep the NetBeans Application project.
3. **Name the principle violated.** *Unverified delegation*: outsourcing an engineering/structural decision to the AI rather than restricting the AI to explanation and keeping the decision yourself.
4. **Describe a test to catch this class of error.** Before acting on any AI suggestion, ask the boundary-test question. If acting on it produces something you can *inspect* (a command output, a file path), it is in bounds; if it requires you to *change a course-set decision* (IDE, JDK version, project template), it is out of bounds — flag it and do not act.

**Why this error is common:** AI's plausible-but-wrong guesses arrive with the same confidence and clean formatting as its correct answers, so a student who does not apply the boundary test treats an authority-violating structural suggestion as interchangeable with a verifiable diagnostic one.

---

## Part E — Transfer Problem

**Same principle, new context.** You have never used Python, but you are asked to help a friend whose Python script fails the instant they run it with the message `python: command not found` in one terminal, while a different terminal on the same machine runs the same script fine. Without learning Python, apply this chapter's *evidence-not-belief* and *layered diagnosis* habits: design a short sequence of commands whose **output** would let you locate the failure (is it a missing interpreter, a PATH difference between terminals, or the script's own code?), and state what output pattern would point to each cause. You do not need to fix anything — produce the *evidence-gathering plan*.

**Hint (use only if stuck after 10 minutes):** The chapter's toolchain layer is the runtime plus the *PATH configuration that lets your terminal find it*. Two terminals behaving differently on the same machine is a PATH-layer signature, not a program-layer signature — and the way to prove it is to ask each terminal to print what it can find, rather than to believe either one.

**Reflection prompt:** (1) What concept from this chapter did you apply, and how did you recognize that it transferred even though the language was different? (2) What was structurally different about the Python case compared to the Java JDK/JRE case in Part A — and what stayed exactly the same?

---

## Part F — Interleaved Review

**Mixed problem set.** Decide which concept applies before solving — that selection is the point.

**Problem F1:** A student's `java --version` reports `21.0.1` and `javac --version` reports `21.0.1`, both matching the course's supported version. NetBeans runs Hello World and prints output. Walk the full Module 0 verification checklist and state which of the five items this evidence does and does not satisfy, and what remaining evidence the student must still gather before declaring setup *done* rather than *assumed*. *Chapter this draws from: Chapter 0 (Welcome).*

**Problem F2:** You are handed a working Hello World project. Without running it, identify the `main` method in the main class and explain, in the chapter's terms, why the JVM "starts here" — what role the entry point plays between the compiled `.class` bytecode and execution. *Chapter this draws from: Chapter 0 (Welcome) — the First Project and The Machinery sections.* *(This is the within-module prior concept; later modules will draw F2 from earlier chapters.)*

**Problem F3:** A program fails to run with a message about a missing class at runtime. It could superficially look like a program-layer bug (you wrote a class wrong) but it may actually be a project-layer bug (the project template places compiled output where the runtime does not look). Decide which layer you will investigate first, justify the choice with the chapter's guidance on *where* most runtime "class not found" failures live, then describe the single piece of evidence that would settle it. *Note to instructor: intentionally ambiguous; commit to an approach, then reflect.*

**After F1–F3:** State which concept you reached for first in each problem and whether it was the right one — especially for F3, where the surface symptom (a missing class) invites a program-layer guess that the three-layer model warns against.

---

## Instructor Notes

**Common errors to watch for:**
- Students conflate "Hello World printed" with "setup is verified," satisfying checklist item 4 while leaving items 2, 3, and 5 untouched — the exact gap Part C targets.
- Students treat all AI suggestions as equally authoritative and act on a structural one (switch IDE/JDK/template) instead of restricting AI to explanation — the *unverified delegation* error in Part D.
- Students diagnose a toolchain or project failure as a program failure, reading Stack Overflow about Java syntax when `javac` is missing — debugging a phantom (Part A).

**Signs a student needs to return to the chapter:**
- They cannot, from memory, state what `java --version` answering while `javac --version` says "command not found" implies (the JRE-without-JDK signature).
- They describe their environment as "working" but cannot produce the file path of their `.class` file — evidence the project layer is unverified.

**Scaffolding adjustments:** *For students who struggle with Part A:* give them the two command outputs printed on paper and ask only "which one is missing, and which package (JDK or JRE) contains the missing tool?" — isolate the JDK/JRE read before adding the layer vocabulary. *For students who finish Part F quickly:* have them attempt the chapter's Challenge exercise — find a failure that crosses two layers simultaneously (e.g., a project-template choice that only fails under a specific JDK version) and propose a verification step that catches it before it surfaces as a program error.

**Domain adaptation note:** The library, inventory, and healthcare-scheduling domains do not change Module 0 at all — the JDK check, project template, and five-item checklist are identical; the domain only changes what classes get named later, never the toolchain.
