# Module 0 — Welcome: Exercises

> **Note:** This is the first chapter in the sequence. Tier 3 (Synthesis) is omitted because there are no prior chapters to connect to. Synthesis exercises begin in Module 1.

---

## Learning Objectives Covered

- Verify that the Java development environment (JDK, `javac`, NetBeans) is correctly installed and produces inspectable evidence
- Apply the three-layer diagnostic model (toolchain / project / program) to classify and locate failures
- Distinguish appropriate from inappropriate AI use during environment setup

*Every exercise below maps to at least one of these objectives. The `(Tests: ...)` tag on each exercise identifies which one(s).*

---

## Worked Example

*Study this example before attempting Tier 1. After reading it, close it and try to recall the key steps from memory before moving on.*

**Problem:** A student runs `java --version` and gets `openjdk 17.0.2`. They run `javac --version` and get `'javac' is not recognized as an internal or external command`. They conclude that Java is broken. Which layer has the problem, what is the likely cause, and what should they do next?

**Approach:**
1. **Identify what each command tests.** `java` launches the JVM — it belongs to the JRE. `javac` is the compiler — it belongs to the JDK. One works, one does not.
2. **Apply the three-layer model.** The program layer (source code) is untouched. The project layer (NetBeans project) is not involved yet. The failure is in the toolchain layer: the JDK is either not installed, or its `bin` directory is not on the system PATH.
3. **Form the hypothesis.** The most likely cause: the JRE was installed from java.com (which provides the runtime only) rather than the JDK from jdk.java.net or adoptium.net.
4. **Plan the verification.** Navigate to `C:\Program Files\Java` (Windows) or `/usr/lib/jvm` (Linux/Mac) and check whether a JDK directory exists alongside the JRE directory. If it does, add its `bin` folder to PATH. If it does not, install the JDK.

**Answer:** The toolchain layer has the problem. The JRE is installed but the JDK is not (or is not on PATH). The student should install the full JDK from jdk.java.net and verify with `javac --version` before opening NetBeans.

**What to notice:** The symptom ("Java is broken") is at the wrong layer. The program layer is fine — the student hasn't written any code yet. Assigning the failure to the correct layer first cuts the repair time dramatically.

---

## Tier 1 — Warm-Up (Recall, True/False, Definition)

*(Tests: recall, conceptual identification, true/false with explanation)*

**Exercise 1** *(Tests: JDK vs. JRE distinction)*

What is the difference between the JDK and the JRE? Why does a developer need the JDK and not just the JRE?

---

**Exercise 2** *(Tests: evidence-based verification — javac required)*

**True or False:** "If `java --version` returns a version number, your Java development environment is fully set up and ready for writing and compiling code."

State whether this is true or false, then explain your reasoning in two to three sentences.

---

**Exercise 3** *(Tests: three-layer diagnostic model — layer classification)*

A student opens NetBeans and sees a red error banner: "Project has no Java platform set."

Which of the three layers — toolchain, project, or program — does this error belong to? Explain your reasoning.

---

**Exercise 4** *(Tests: toolchain layer vs. project layer — contrastive classification)*

Classify each of the following failures as a **toolchain layer** problem, a **project layer** problem, or a **program layer** problem. For each one, write one sentence explaining your classification.

- (a) `javac` is not found on the system PATH
- (b) NetBeans shows "Project has no Java platform set" even though `javac --version` works fine
- (c) The program compiles but prints `null` instead of a student's name
- (d) The `.class` file is missing from the `build/classes` folder after running the project

*(Why this is tempting to get wrong: (a) and (b) both involve Java installation, so students often call both "toolchain." The distinction is whether the failure is in the global system — toolchain — or in the per-project configuration — project.)*

---

**Exercise 5** *(Tests: javac command — compilation output)*

What is the purpose of the `javac` command? What does it produce, and where does that output go in a NetBeans project?

---

**Exercise 6** *(Tests: source file vs. compiled artifact — bytecode)*

**True or False:** "A `.class` file contains Java source code that humans can read and edit."

State whether this is true or false, then explain your reasoning in two to three sentences.

---

## Tier 2 — Application (Scenarios, Error Analysis, AI Interaction)

*(Tests: applying the three-layer model, AI boundary rules, diagnostic prompt construction)*

**Exercise 7** *(Tests: three-layer diagnostic model — missing evidence)*

A student emails you: "My program works fine — I ran it and it printed the right output." You ask them to close NetBeans, navigate to their project folder, and show you the `.class` file. They cannot find it.

Using the three-layer model, explain:

(a) Which layer is unverified?
(b) What specific evidence is missing?
(c) What risk does this leave them exposed to?

---

**Exercise 8 — Error Analysis** *(Tests: AI boundary rules — inappropriate delegation)*

A student is setting up their environment and pastes this into an AI assistant:

> "Set up my Java project for me. I'm using NetBeans. Just make the settings correct automatically."

(a) Identify two problems with this AI request based on the AI boundary rules from this module.
(b) Rewrite the request as a well-formed diagnostic prompt that follows the template from this module.

---

**Exercise 9** *(Tests: three-layer diagnostic model — javac missing from PATH)*

You run `java --version` and get:

```
openjdk 17.0.2 2022-01-18
```

You run `javac --version` and get:

```
'javac' is not recognized as an internal or external command
```

(a) Which layer has the problem?
(b) What is the likely cause?
(c) What is the appropriate next step?

---

**Exercise 10 — AI Interaction** *(Tests: AI boundary rules — JRE vs. JDK error in AI output)*

First, without consulting AI, write in one sentence: what is the most important thing a student needs to install to compile Java programs?

Then read the following AI response:

> "Download and install the latest JRE from java.com. Then open NetBeans, go to Tools > Java Platforms, and add the JRE. You're ready to code!"

(a) Identify the strongest point in this response.
(b) Identify the most significant error or gap.
(c) Write a corrected version of the problematic sentence.
(d) State the specific command you would run to verify whether the AI's suggested installation actually gives you a working compiler.

---

**Exercise 11 — Self-Explanation** *(Tests: evidence-based verification vs. belief-based assumption)*

In this module, the author requires students to run `javac --version` separately from `java --version`, even though most students assume that installing Java installs both. Explain in 2–3 sentences why running both commands separately is preferable to assuming both are installed. Your explanation must use the term **"toolchain layer"** correctly.

---

**Exercise 12** *(Tests: diagnostic prompt construction — AI boundary in practice)*

Write the diagnostic prompt you would use for the following error: NetBeans shows `error: package does not exist` on the line `import java.util.ArrayList`.

Your prompt must follow this template:
- State what you are trying to do
- Describe the exact error message
- List what you have already verified
- Ask a specific question

Your prompt must **not** ask the AI to fix your project structure on your behalf.

---

## Tier 3 — Synthesis

*Omitted — this is the first chapter. Synthesis exercises begin in Module 1.*

---

## Tier 4 — Challenge

**Exercise 13** *(Tests: three-layer diagnostic model — cross-layer failure)*

The three-layer model (toolchain, project, program) is described in this module as a simplification.

Identify a failure mode that does not fit cleanly into a single layer — one that requires both the **project layer** and the **toolchain layer** to be in a specific state simultaneously. Describe the failure, explain why it crosses layers, and propose a verification step that would catch it before it surfaces as a programming error.

**Rubric (no answer key provided for Tier 4):**

| Criterion | Strong Response |
|---|---|
| Failure identification | Describes a concrete, realistic failure — not a hypothetical abstraction |
| Layer analysis | Correctly explains why neither layer alone is sufficient to produce the failure |
| Verification proposal | Names a specific, executable verification step (a command, a setting check, etc.) |
| Precision | Uses toolchain/project/program vocabulary accurately throughout |

---

## Answer Key — Exercises 1–12

**Worked Example**
*No answer needed — the worked example is its own model.*

---

**Exercise 1**
The JRE (Java Runtime Environment) contains only what is needed to *run* compiled Java programs: the JVM and standard libraries. The JDK (Java Development Kit) includes everything in the JRE plus the compiler (`javac`) and other development tools. A developer needs the JDK because writing code requires compiling `.java` source files into `.class` bytecode — the JRE alone cannot do this.

---

**Exercise 2**
**False.** The `java` command is the runtime launcher; it only verifies that the JVM is installed and runnable. It does not confirm that the compiler (`javac`) is present or accessible. A machine can have a JRE without a JDK, meaning you could run existing Java programs but not compile new ones. Verification of a development environment requires checking both `java --version` and `javac --version`.

*Common error:* Students answer True because "Java is installed" feels like it covers everything. The misconception is treating Java as a single thing when JRE and JDK are separate packages with different capabilities.

---

**Exercise 3**
This error belongs to the **project layer**. The toolchain (JDK installation) may be fully functional, but the NetBeans project has not been configured to point to it. The error is not in the student's code (program layer), and it does not indicate the JDK is missing (toolchain layer) — it indicates that the project does not know where to find the platform. The fix is a project configuration step, not a JDK installation step.

*Common error:* Students say "toolchain layer" because the error mentions Java. The distinguishing question: is the JDK missing from the system, or does the project not know where to find it? Those are different layers.

---

**Exercise 4**
- (a) **Toolchain layer** — `javac` missing from PATH is a global system configuration issue, not specific to any project.
- (b) **Project layer** — `javac` works fine system-wide; the project configuration has not been pointed at it. Same symptom surface, different layer.
- (c) **Program layer** — the program compiles and runs; the logic or state is wrong.
- (d) **Project layer** — the `.class` file not appearing is a build output path issue, which is project-level configuration.

*Common error:* Students classify (b) as toolchain because both (a) and (b) involve Java installation. The key: toolchain = system-wide; project = per-project configuration. Both can produce Java-related errors, but they are fixed in different places.

*Why this is tempting:* The error messages for (a) and (b) can look nearly identical. The three-layer model's value is precisely that it forces you to distinguish them before guessing a fix.

---

**Exercise 5**
`javac` is the Java compiler. It reads `.java` source files and produces `.class` bytecode files. In a standard NetBeans project, the compiled `.class` files are placed in the `build/classes` directory (or a similar output folder configured by the project), not in the same directory as the source files.

---

**Exercise 6**
**False.** A `.class` file contains Java *bytecode* — compiled, binary instructions intended for the JVM, not for human readers. The human-readable source code is in the `.java` file. Bytecode is not the same as source code; you cannot edit a `.class` file as you would a `.java` file.

---

**Exercise 7**

(a) The **project layer** is unverified. The student has evidence that the program ran (program layer), but has not confirmed that the compiled artifact exists outside the IDE.

(b) The missing evidence is the existence of the `.class` file in the project's output directory. Without this, it is unclear whether the code was actually compiled and run from disk, or whether the IDE executed it through an in-memory or temporary mechanism.

(c) The risk is that the student's project cannot be submitted, transferred to another machine, or run outside of NetBeans. If the compiled output does not persist to disk, the "working program" only exists inside the IDE's runtime — not as a portable artifact.

---

**Exercise 8**

(a) Two problems:
1. The request asks the AI to take autonomous action ("make the settings correct automatically") — this crosses the AI boundary rule that prohibits delegating configuration decisions to an AI that cannot see, test, or verify your environment.
2. The request provides no context: no error message, no operating system, no current state. The AI has no basis for useful guidance and is likely to produce generic or incorrect instructions.

(b) Model rewritten prompt:
> "I am trying to configure a new Java project in NetBeans 17 on Windows 11. When I try to create a new Java Application project, I get the message 'No Java platforms found.' I have already confirmed that `java --version` returns 17.0.2 and `javac --version` returns 17.0.2. I have not yet added a platform in Tools > Java Platforms. Can you explain what the difference is between a JDK installation and a NetBeans Java Platform, and what I should look for when adding one?"

---

**Exercise 9**

(a) The **toolchain layer** has the problem.

(b) The `java` command works because the JRE (or a JVM) is on the system PATH, but `javac` is not. This typically means the JDK was not installed, only the JRE was installed, or the JDK `bin` directory is not included in the system PATH variable.

(c) The appropriate next step is to verify whether the JDK is installed at all (check the installation directory), and if it is, add the JDK `bin` directory to the system PATH. If the JDK is not installed, download and install it from the official source (jdk.java.net or adoptium.net), not java.com (which distributes the JRE).

---

**Exercise 10**

(a) Strongest point: The response correctly identifies that NetBeans needs to be told where Java is, and points the student to Tools > Java Platforms — this is accurate and actionable.

(b) Most significant error: The response instructs the student to install the **JRE** from java.com. A developer needs the **JDK**, not the JRE. The JRE does not include `javac` and cannot be used to compile Java programs. Installing the JRE would leave the student unable to compile code.

(c) Corrected sentence: "Download and install the latest **JDK** from **jdk.java.net** or **adoptium.net** — not the JRE from java.com, which does not include the compiler."

(d) Verification command: `javac --version`. If this returns a version number after the installation, the compiler is present. If it returns "command not found," the JDK is either not installed or not on PATH — regardless of what the installer reported.

*Common error:* Students accept the AI's answer because it sounds authoritative and they don't yet know the JRE/JDK distinction. This exercise works best after students have tried `javac --version` themselves and know what it feels like to have it fail.

---

**Exercise 11**
Running `javac --version` separately from `java --version` is preferable because the **toolchain layer** has two distinct components — the runtime (JRE) and the compiler (JDK) — that are packaged and installed separately. Assuming both are present because one works is belief-based, not evidence-based: the JRE can be installed from java.com without the JDK, leaving `javac` absent from the system PATH. A development environment is only verified when each component has produced inspectable output, not when the installer said "complete."

*Common error:* Students explain that it is "good practice" without invoking the toolchain layer distinction or the JRE/JDK separation. A strong answer must name why the two commands test different things.

---

**Exercise 12**
Sample well-formed prompt:

> "I am trying to use `ArrayList` in a Java class I am writing in NetBeans 17. When I add the line `import java.util.ArrayList;` at the top of my file, NetBeans underlines it in red and shows the error: `error: package does not exist`. I have already verified that `javac --version` returns 17.0.2 and that my NetBeans project has a Java platform set in Tools > Java Platforms. I have not changed any library or classpath settings. Can you explain under what circumstances the `java.util` package would be unavailable in a standard NetBeans Java Application project, and what configuration I should check?"

Key elements to check in student responses:
- States the goal (using ArrayList)
- Quotes the exact error message
- Lists prior verification steps
- Asks a specific, bounded question
- Does not ask the AI to "fix my project"

---

## Instructor Notes

**Suggested point distribution:**
- Tier 1: 5 points per item
- Tier 2: 10 points per item
- Tier 3: n/a (omitted — first chapter)
- Tier 4: 20 points

**Bloom's distribution for this chapter:**

| Tier | Exercises | Bloom's Level | % of Set |
|---|---|---|---|
| Tier 1 — Warm-up | Ex 1–6 | Remember / Understand | ~25% |
| Tier 2 — Application | Ex 7–12 | Apply / Analyze | ~67% |
| Tier 3 — Synthesis | omitted | — | — |
| Tier 4 — Challenge | Ex 13 | Evaluate / Create | ~8% |

**Assignment recommendations:**
- Tier 1: appropriate for completion credit or pre-class preparation
- Tier 2: appropriate for graded homework (0.5–1.0% of course grade per item)
- Tier 4: appropriate for optional extension or extra credit

**Worked example note:** The worked example targets the `javac`-missing-from-PATH failure, which is the most common setup failure. If students struggle with Tier 1 after reading it, ask them to close the example and reproduce the three diagnostic steps from memory before re-attempting.

**Exercise 4 (Contrastive Classification):** The most common error is classifying item (b) as toolchain. Use this as a class discussion anchor: draw the three layers on a whiteboard and ask students where each fix lives. The project layer / toolchain distinction is the highest-value conceptual separation in this module.

**Exercise 8 (Error Analysis):** The most common student error is rewriting the prompt as a better phrasing of the same inappropriate request ("Can you please set up my Java project?"). Push students to change the *structure* of the request, not just the tone.

**Exercise 10 (AI Interaction):** The verification step (part d) is the most important part. Students who name `javac --version` specifically — not "I would check if it works" — have understood the evidence-based principle. Students who say "run the installer again" have not.

**Exercise 11 (Self-Explanation):** Students often describe the two approaches instead of explaining why running both commands is preferable. The target vocabulary: "toolchain layer," "JRE," "JDK," "evidence." Watch for answers that say "because it is more thorough" without naming the mechanism (two separate packages, two separate PATH entries).

**Common errors to watch for:**
- Conflating toolchain and project layer (Exercises 3, 4, 7)
- Accepting AI output that recommends JRE instead of JDK (Exercise 10)
- Writing a diagnostic prompt that asks the AI to fix the problem rather than explain it (Exercise 12)

**Scaffolding adjustments:**
- *For students who struggle with Tier 1:* Have them re-read "The Machinery" and "The Diagnostic Habit in Practice" sections specifically — not the whole chapter.
- *For students who complete Tier 4 quickly:* Ask them to identify a fourth layer the model ignores (e.g., the network/cloud layer for remote development environments) and describe a failure mode it would produce.

**DEI note:**
All scenarios in this exercise set have been written to avoid cultural, regional, or socioeconomic assumptions. The environment setup context is universal to any student with access to a computer, regardless of background.
