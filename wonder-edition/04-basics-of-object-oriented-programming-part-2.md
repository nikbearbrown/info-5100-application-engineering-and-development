# Module 4 — Basics of Object-Oriented Programming Part 2: Wonder Edition
## Companion Chapter

> **Wonder Edition:** Read this alongside the chapter, not instead of it.

---

> **Content note:** Despite the title "Basics of Object-Oriented Programming Part 2 / Wrapper Classes / Strings," this chapter covers debugging methodology: the hypothesize–isolate–test loop, causal chain tracing, and the distinction between symptom, proximate cause, and root cause. This companion follows the actual chapter content.

---

## The Strange Question

A program compiles without error. It runs without crashing. It finishes cleanly and prints output.

The output is wrong — but only on the second execution of a specific operation. The first execution produces the correct result every time.

Both operations call the same method. Both call it with different arguments. Only the second one fails.

Here is the precise puzzle: if the code path is identical, what makes the second call behave differently from the first?

---

## First Intuition

The wrong name appears in the output. The natural move is to look at the output.

Someone checks the print statement. They check the method that formats the string. They check the variable passed to that method. The code there looks fine. Nothing obvious is broken near the end of the program.

This reaction comes from a deeply familiar experience: when something goes wrong in a physical process, it usually breaks near the end. A batch of cookies burns because the last few minutes of baking were too hot. A report has the wrong total because the last column was summed incorrectly. Proximity between the failure and the cause feels like a law.

That experience does not transfer cleanly to programs. But it shapes first intuitions anyway.

> **► Planning prompt:** Before reading further, write down exactly where you would look first and why. Name a specific method, variable, or line. Then write one sentence describing what assumption your answer depends on — what would have to be true about programs for that location to be the right place to start?

---

## The Surprise

But the print method is innocent. It prints exactly what it receives.

The variable passed to the print method holds the wrong value. Follow that variable backward. It was assigned in the checkout method from a field called `currentPatron`. Inspect `currentPatron` at the moment of that assignment.

`currentPatron` holds the first patron's name. Not the second patron's name. The second patron was never placed into `currentPatron`. Some earlier step — something that ran cleanly, returned no error, and finished without protest — simply did not update the field.

The question has moved. It is no longer about the output, or the print method, or the checkout method. It is about a method that ran before all of those, in a different part of the execution, and left a field in the wrong state. That method is upstream. The symptom is downstream.

> **► Monitoring prompt:** Your first intuition pointed toward the output. The evidence points to a method that ran earlier and finished without any visible signal of failure. Write down what assumption your first intuition was making. Name the specific thing the evidence has now contradicted. What part of the picture is still unexplained — why did that upstream method fail to update the field?

---

## The Hidden Structure

Every Java program is a sequence of state transformations.

An object begins in some initial state. A method runs. Fields are modified or references are reassigned. Another method runs. More fields change. This continues until the final output is produced. Every visible output is the consequence of every transformation that preceded it.

A bug is a transformation that went wrong. The state of some field diverges from its expected value at some point in the sequence. Everything that runs after that point operates on the wrong state. The symptom — wrong output, wrong name, wrong total — is the consequence of an earlier state error, not the error itself.

This makes the symptom a misleading starting point. It announces that something went wrong. It does not indicate where or when. The root cause may be several method calls upstream, in code that finished without throwing an exception and produced no visible warning.

The debugging workflow in this chapter — hypothesize, isolate, test — is a structured method for working backward through that causal chain. Each step narrows the search. Each step requires committing to a specific claim before gathering evidence.

**Misconception Checkpoint:**

> "It is tempting to think that finding the wrong output tells you where the bug is. But a symptom only marks the endpoint of the causal chain; the bug lives somewhere earlier in the chain, where a state transformation went wrong. The correct model holds that diagnosing a bug means tracing backward from the symptom through state changes until the first wrong transformation is found. The key distinction is between the location where wrong behavior becomes visible and the location where wrong state was introduced — these are almost never the same line."

**Code Trace:**

```java
// Second checkout: what the debugger shows at the breakpoint on line 3

String currentPatron;          // field — holds "Alice" (from first checkout)
currentPatron = getNextPatron(); // this call never ran; field was not reset
loan.setPatron(currentPatron); // assigns "Alice" — wrong patron for second book

// Symptom: output prints "Alice" for Bob's book
// Root cause: getNextPatron() was inside a branch that did not execute
```

The debugger pauses on line 3. The variables panel shows `currentPatron = "Alice"`. The hypothesis — that the field was not updated — is confirmed. The fix is upstream, in the branch logic that skipped `getNextPatron()`.

---

## Try Looking At It This Way

**Target:** Tracing a bug backward from its visible symptom to its upstream root cause in a Java program.

**Base:** A city water system that delivers discolored water to one faucet in a building.

**Features:**
- The discoloration is visible only at the endpoint — the faucet — not at any earlier point in the pipe run.
- The contamination source could be anywhere along the pipe: the main supply, the building's filtration unit, the distribution manifold, or a section of pipe specific to that faucet.
- The faucet itself is almost certainly not the source; it is the announcement point.
- The correct diagnostic method moves backward through the pipe from the faucet, testing sections one at a time, until it finds where clean water becomes discolored.
- Once the contamination point is found, the repair is made there — not at the faucet.

**Commonalities:**
- The symptom is visible only at the program's output, just as discoloration is visible only at the faucet. Both endpoints announce the problem without revealing its source.
- The cause could be anywhere upstream in the execution sequence, just as contamination could be anywhere upstream in the pipe run. Proximity to the symptom does not predict proximity to the cause.
- The diagnostic method in both cases is directional: start at the symptom, move upstream one step at a time, test the state at each step, stop at the first point where the state is wrong.
- Fixing the faucet while leaving the contamination source untouched would mask the symptom without solving the problem — exactly what happens when a developer patches output code without tracing the state error.
- Both systems require the investigator to form a hypothesis about where in the chain the fault is before intervening — random testing of pipe sections or random code changes wastes time and may introduce new problems.

**Boundaries:** The analogy has one significant limit. Contamination in a pipe travels forward continuously and passively. State in a Java program does not travel. A field holds one discrete value until an explicit assignment changes it. The bug in this chapter is not contamination spreading forward — it is an absence: the assignment that should have updated `currentPatron` was never reached. Absence bugs do not have a visible contamination trail. The field simply sits holding its old value, silent and wrong, until something reads it.

**Conclusions:** Tracing from symptom to root cause is a systematic spatial move upstream through a causal chain. The debugger is the tool that makes each discrete step in that chain inspectable. The pipe analogy conveys the directionality well but does not prepare a reader for bugs caused by things that did not happen rather than things that happened incorrectly.

---

## Where The Analogy Breaks

Unlike a water pipe, a Java program does not carry state forward continuously.

A field holds a value. It holds that value until a method explicitly assigns a new one. If the assignment is skipped — because it was inside a branch that did not execute, or inside a method that was not called — the field retains its previous value silently. There is no visible signal that the update was missed.

This matters because the most common class of absence bug produces no error output at all. The program runs. The field holds the wrong value. Every method that reads the field behaves correctly given the value it receives. Only the output is wrong.

The pipe analogy implies that contamination is something added to the system. Absence bugs are the opposite: something that should have been done was not done. The debugger reveals this by showing the field's value at the moment it is read — a value that should have been updated and was not.

---

## Small Discovery

Consider hospital medication administration.

A nurse prepares six medications for a patient over the course of a shift. At the end of the shift, the patient's blood pressure is within normal range. A supervisor reviewing the chart notices that medication four was documented as administered at 2:14 p.m. but the pharmacy dispensed it at 2:19 p.m. — five minutes later.

**Raw data:** The medication was supposedly given before it was dispensed. The patient's final vital signs are normal.

**Pattern search:** The final state — normal blood pressure — looks correct. Does that tell the supervisor whether medication four was actually given? Does the normal reading confirm that the process was executed correctly?

> **► Prediction:** Before reading the next paragraph, write down whether the supervisor can conclude from the normal blood pressure that everything was administered correctly. What would the supervisor need in order to be certain?

---

The supervisor cannot conclude that the administration was correct. The patient's blood pressure is normal. That is a final state. It does not reveal which interventions produced it. Medication four may have been given late and still worked. Another medication may have compensated. The normal reading may be coincidental. The supervisor needs the process record — each step, in sequence, with verified timestamps — not just the final value.

This is identical to the situation of a developer who patches output code until the wrong result disappears. The final output looks correct. That tells the developer nothing about whether the state transformation that was wrong has been corrected, or whether the wrong value is still sitting in a field that this particular test input happened not to reach.

The final state is evidence of the final state. It is not evidence of the process that produced it.

---

## What This Changes

A reader who completes this chapter can now answer a question that seemed simple before: when a program produces wrong output, where do you look first?

The answer is no longer "near the output." The answer is: form a hypothesis naming the specific object, the specific field, and the specific moment in execution where you expect the state to be wrong. Then set a breakpoint there. Then compare what the debugger shows against what the hypothesis predicted.

Specific code looks different after this. A method that reads from a field and passes the value to the output now raises a question about whether the field was correctly set before the method ran — not just whether the method's own logic is correct. Every output becomes the downstream consequence of an upstream state history.

**Practice Bridge:** In the semester project's library checkout module, identify one field that is read by more than one method. Write a hypothesis naming that field, a specific value it might hold incorrectly, and a moment in execution when that incorrect value would produce wrong output. Set a breakpoint at that moment. Document what the variables panel shows — specifically whether your hypothesis was confirmed, refined, or refuted — and write one sentence naming the root cause or explaining why your hypothesis was wrong.

The open question this chapter leaves: if state errors are the source of bugs, what design choices at the class level would make illegal state structurally harder to produce? That is the question Module 5 opens. Hold it now. Return to it after the lab.

---

## Wonder Questions

1. A program produces the same wrong output on every single run, regardless of input order. A different program produces wrong output only when two operations are called in a specific sequence. Which program is harder to debug using the hypothesize–isolate–test loop, and why? What property of reproducibility is the loop actually depending on?

2. The chapter argues that a wrong hypothesis is still useful because ruling it out tells you something true about the system. But testing a hypothesis requires setting a breakpoint, running the program, and reading the variables panel. What is the actual cost of a wrong hypothesis? Is there a point at which forming many wrong hypotheses becomes counterproductive, and what would that look like?

3. A developer argues that print statements are sufficient for all debugging and that the NetBeans debugger adds complexity without benefit. She is often correct. What exactly does she lose compared to a developer who uses breakpoints? Is there a class of bug for which she is right — where print statements genuinely are adequate — and how would you characterize that class?

4. The chapter says the gap between intent and execution is where bugs live. Can that gap ever produce a program that works correctly for reasons the developer did not intend? If a program produces correct output for the wrong internal reasons, what does that imply about output as evidence of correctness?

5. The module's AI boundary requires forming a hypothesis before presenting code to AI for analysis. A student objects that AI could help form the hypothesis by reading the code first. What specific cognitive work does the student's proposal skip? What does the student lose by not building the causal map independently?

---

**Precision Summary**

**What the concept is:** Debugging as causal diagnosis — a structured method for forming a falsifiable hypothesis about where state went wrong, isolating evidence at that location with a breakpoint, and tracing backward from symptom through proximate cause to root cause.

**What it explains:** Why changing code until the wrong output disappears is unreliable; why a bug's root cause is almost never located where the symptom appears; why the debugger's intermediate state view is categorically more informative than the program's final output alone.

**What it does NOT mean:** That every bug requires extensive investigation. Simple bugs still follow the same causal structure — the framework applies, just faster. The framework does not add work; it adds direction to work that would happen anyway, and it produces a verifiable diagnosis rather than a guess that happened to silence the symptom.

**What comes next:** If state errors upstream of symptoms are the source of bugs, how do you design a class so that illegal state is structurally difficult to introduce in the first place? That is the question Module 5 addresses through encapsulation, access control, and the design of object boundaries.
