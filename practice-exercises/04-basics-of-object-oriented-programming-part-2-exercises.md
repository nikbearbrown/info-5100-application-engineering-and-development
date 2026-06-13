# Module 4 — Basics of Object-Oriented Programming Part 2: Exercises
**Topic:** Debugging methodology, hypothesis-isolate-test loop
**Learning Objectives:**
1. Form hypotheses about state divergence
2. Use breakpoints to isolate evidence
3. Distinguish symptom from proximate and root cause
4. Trace causal chains

---

## Tier 1: Warm-up

**1. Recall** *(Tests: LO3 — three levels of a bug)*

What are the three levels of a bug? Define symptom, proximate cause, and root cause. Give one example of each from a library checkout scenario.

---

**2. True/False + Explain** *(Tests: LO3 — root cause vs. symptom fix)*

> "If changing a line of code makes the wrong output go away, you have fixed the bug."

State whether this is true or false. Explain your reasoning in two to three sentences.

---

**3. Vocabulary** *(Tests: LO1 — hypothesis formation)*

What is a hypothesis in the context of debugging? What makes a hypothesis "falsifiable" rather than vague?

---

**4. Breakpoint** *(Tests: LO2 — step over vs. step into)*

What is the difference between "step over" and "step into" in a debugger? When would you use each?

---

**5. True/False + Explain** *(Tests: LO1, LO3 — debugging as understanding)*

> "The best debugging strategy is to change code until the output looks correct, then stop."

State whether this is true or false. Explain your reasoning in two to three sentences.

---

## Tier 2: Application

**6. Scenario** *(Tests: LO1, LO2 — hypothesis and breakpoint placement)*

A student registration system shows the correct student name on the confirmation screen after the first registration. On the second registration, it shows the previous student's name.

- (a) State a precise hypothesis about where state diverges.
- (b) Describe exactly where you would set a breakpoint to test it.
- (c) Describe what you would look for in the variables panel at that breakpoint.

---

**7. Error Analysis** *(Tests: LO3 — proximate vs. root cause)*

A student debugs a bug where the wrong patron appears on the confirmation screen. They find the bug and make this fix: they add `patronLabel.setText("")` at the start of the checkout method to clear the label before each checkout. The bug no longer appears in testing.

- (a) Which level of the three-level model did the student address?
- (b) What is wrong with this fix?
- (c) What root cause did they fail to address?

---

**8. Causal Chain** *(Tests: LO3, LO4 — tracing symptom to root cause)*

Trace the following causal chain for a grade submission bug: *"The confirmation screen shows the wrong student's grade."*

Working backward from the symptom, identify:
- (a) One plausible proximate cause
- (b) One plausible root cause that could produce that proximate cause
- (c) One breakpoint location and what variable you would inspect there

---

**9. AI Interaction** *(Tests: LO1 — hypothesis-isolate-test loop)*

A student has a bug where a checkout always assigns to the first patron in the system, regardless of which patron is selected. They ask an AI: *"My checkout assigns to the wrong patron. Can you fix my code?"* and paste their 80-line `CheckoutHandler`. The AI rewrites the handler with a fix. The student runs it and the bug is gone.

- Identify what the student did **correctly**.
- Identify what the student **failed to do**.
- Write the specific question the student should have asked instead, based on the hypothesis-isolate-test loop.

---

**10. Hypothesis Formation** *(Tests: LO1, LO2 — precise hypothesis and breakpoint)*

You observe that a product inventory app correctly saves new products when the app first runs, but after editing a product and saving, the original unedited product reappears on restart.

Write a precise, falsifiable hypothesis about where state diverges. Identify the specific breakpoint and variable you would inspect to test it.

---

## Tier 3: Synthesis

**11. Synthesis (Ch 4 + Ch 2)** *(Tests: LO1, LO3 + Ch 2 reference semantics)*

In Ch 2, you learned that two references can point to the same object. In Ch 4, you learned that bugs often arise from the intent-execution gap.

Describe a scenario where a shared reference (Ch 2) creates a bug that manifests as a symptom (Ch 4) that looks like a logic error rather than a memory error. Explain:
- (a) The symptom a developer would observe
- (b) How you would form a hypothesis about the cause
- (c) Why the root cause is a reference issue, not a logic issue

**What distinguishes a surface answer:**
- Scenario is concrete and plausible (use a library or student system)
- Hypothesis is falsifiable and specific
- Correctly identifies reference mechanics as root cause, not a conditional or calculation mistake

---

**12. Synthesis (Ch 4 + Ch 1)** *(Tests: LO1, LO3 + Ch 1 verification loop)*

The verification loop from Ch 1 says to ask: "Does the Java artifact do what the business requires?" The debugging loop from Ch 4 says to form a hypothesis and isolate evidence.

Explain how these two loops relate:
- When does the verification loop detect that something is wrong?
- When does the debugging loop take over?
- Give a concrete example from a library or student system where you would use each loop.

**What distinguishes a surface answer:**
- Uses specific vocabulary from both chapters
- Clearly distinguishes detection (verification) from diagnosis (debugging)
- Concrete example shows both loops applied correctly, not just described abstractly

---

## Tier 4: Challenge

**13. Capstone — Breakpoint-Resistant Bugs** *(No answer key — rubric only)*

The debugging methodology in this chapter assumes you can observe state through breakpoints. Describe a class of bugs where breakpoints cannot help — where the act of pausing execution changes the program's behavior, or where the relevant state is not visible in the variables panel.

For each type you identify:
- Explain why it resists standard debugging
- Propose a debugging strategy that does not rely on breakpoints

**Rubric — a strong response will:**
- Name at least two distinct classes of breakpoint-resistant bugs
- Explain the specific mechanism that makes breakpoints ineffective for each (not just "it's hard")
- Propose a concrete alternative strategy for each class (logging, instrumentation, deterministic replay, etc.)
- Acknowledge any limitations of the proposed alternative strategy

---

## Full Answer Key (Tiers 1–3)

### Tier 1 Answers

**1.**
- **Symptom:** The observable wrong behavior — what the user or tester sees. Example: the confirmation screen displays "Patron: null" after a checkout.
- **Proximate cause:** The immediate code condition that produces the symptom. Example: `confirmationScreen.patronLabel` is null when `setText(...)` is called.
- **Root cause:** The underlying design or logic error that created the proximate cause. Example: `setPatron(...)` was never called on the confirmation screen before it was displayed.

**2. False.** Making the wrong output disappear addresses the symptom, not necessarily the root cause. The underlying defect may still exist and will resurface under different inputs or conditions. A correct fix requires understanding *why* the wrong output occurred and addressing that cause.

**3.** A hypothesis in debugging is a specific, testable claim about where and why state diverges from what the program intends. A hypothesis is falsifiable when it specifies a concrete location (a method, a variable, a line) and a predicted state (a specific value or reference) that can be confirmed or refuted by inspecting the program at runtime. A vague hypothesis — "something is wrong with the checkout" — cannot be tested because it does not predict what to observe.

**4.** "Step over" executes the current line as a single unit and pauses on the next line, without entering any method called on that line. "Step into" enters the method being called on the current line and pauses at its first statement. Use step over when you are confident the called method is correct and want to move through the calling method quickly. Use step into when the bug may be inside the called method and you need to observe its internal execution.

**5. False.** Changing code randomly until output looks correct is guessing, not debugging. It can mask symptoms without addressing the root cause, introduce new bugs, and leaves the developer without understanding of what was wrong. A correct debugging process requires forming a hypothesis, finding evidence, and confirming the root cause before making a change.

---

### Tier 2 Answers

**6.**
- (a) Hypothesis: The confirmation screen's `Student` reference is not being updated between registrations. The screen was set with the first student object and never reset when the second registration began — either `setStudent(...)` is not called before the second display, or the same student object is being mutated rather than replaced.
- (b) Set a breakpoint at the line in the registration flow where `confirmationScreen.setStudent(student)` is called — specifically just before the second `layout.show(container, "confirmation")` call.
- (c) Inspect the `student` variable: confirm its `name` field matches the second student's name, not the first. Also inspect `confirmationScreen`'s student field to verify it is updated to the new reference after the setter call.

**7.**
- (a) The student addressed the **symptom** — the visible wrong text in the label — not even the proximate cause.
- (b) Clearing the label at the start of checkout hides the wrong display but does not fix the underlying issue. If the patron reference is incorrect, the label will still be populated with wrong data during the checkout — just with a blank flash first.
- (c) The root cause — likely that `setPatron(...)` was called with the wrong patron object, or that the confirmation screen's patron reference was never properly updated — was never identified or fixed.

**8.**
- (a) Proximate cause: The `GradeRecord` object displayed by the confirmation screen holds a reference to the previous student's data — `confirmationScreen.gradeRecord.student` points to the wrong `Student` object.
- (b) Root cause: The `GradeEntry` screen creates a new `GradeRecord` but assigns it a reference to a `Student` field that was never updated after the first submission — the field still holds the first student's reference.
- (c) Set a breakpoint inside the `GradeEntry` screen's submit handler, on the line that creates the `GradeRecord`. Inspect the `student` variable to verify it holds the correct second student's identity before the record is created.

**9.**
- **Correctly:** The student identified the symptom precisely ("assigns to the wrong patron") and provided enough context (the full handler) for the AI to attempt a fix.
- **Failed to do:** The student did not form a hypothesis, did not identify the proximate or root cause, and did not verify that the AI's fix addressed the actual defect rather than coincidentally changing behavior. The student now has a working program they do not understand.
- **Better question:** "I suspect the bug is in how the selected patron is retrieved before being passed to the checkout method. My hypothesis is that `getSelectedPatron()` is returning the first patron in the list instead of the one the user selected. Can you help me understand what `getSelectedPatron()` does and whether my hypothesis is correct?"

**10.**
Hypothesis: The edit operation creates a modified `Product` object in memory but does not persist it to the data store — the original object in the store is never replaced, so on restart the store reloads the original. Specifically, the `save()` method may be updating a local variable rather than replacing the entry in the product list or file.

Breakpoint: Set a breakpoint at the end of the save method, after the persistence call. Inspect the data store (the list or file-write buffer) to verify the entry for the edited product ID now reflects the new field values. If the store still shows the old values at this point, the save method is not writing through correctly.

---

### Tier 3 Answers

**11.**
Consider a library search screen that does this: it stores the last-found `Book` in a field `currentBook`, then calls `detailScreen.setBook(currentBook)`. Later, the search is run again and the code calls `currentBook.setTitle(newTitle)` to update the displayed search result in-place rather than creating a new object. The symptom is that the detail screen now shows the new title — even though the user never navigated back to the detail screen. A developer observing this would form the hypothesis: "the detail screen's `setBook` method has a bug that makes it react to changes it was never told about." But the root cause is that both the search screen and the detail screen hold a reference to the *same* `Book` object; mutating it through one reference is immediately visible through the other. No logic bug exists — the detail screen is displaying exactly what it was given. Recognizing this requires understanding that the intent (pass a snapshot) diverged from the execution (pass a live shared reference).

**12.**
The verification loop from Ch 1 operates at the boundary between the program and the business requirement: you run the program, observe its output, and ask whether that output matches what was specified. It detects that something is wrong — a wrong value, a missing record, a crash — but does not explain why. The debugging loop from Ch 4 takes over once the verification loop has detected a failure: you form a hypothesis about where state diverged from intent, set a breakpoint to isolate evidence, and confirm or refute the hypothesis before changing code.

Example: In a library system, the verification loop detects that a checkout confirmation shows the wrong patron name (the output does not match the requirement "show the name of the patron who just checked out"). The debugging loop then takes over: form a hypothesis ("the confirmation screen's patron field was set before the user selected a patron"), set a breakpoint on `setPatron(...)`, inspect the patron reference, and confirm that the setter was called with a stale reference from a previous session. The verification loop told us *that* something was wrong; the debugging loop told us *why*.

---

## Instructor Notes

- **Exercise 7** is the critical item in this module. Students who say the student "fixed the bug" have not grasped the three-level model. Use this item to open discussion about what "fixing" means. Award zero points for answers that call the symptom-fix a valid solution.
- **Exercise 9 (AI Interaction)** is designed to surface the danger of treating AI as an oracle rather than a collaborator. The key insight students should reach is that accepting a working fix without understanding it produces a developer who cannot debug the next bug. Assess whether the student's "better question" engages the hypothesis-isolate-test loop or just asks for a better explanation.
- **Exercise 6** rewards precision. Weak answers say "check the student variable." Strong answers name a specific line in a specific method and predict a specific value to inspect.
- **Exercise 13 (Challenge)** is open-ended. Common strong answers identify: (1) timing/concurrency bugs where pausing a thread changes interleaving; (2) bugs that only manifest under production load, not in a debugger; (3) bugs involving serialized/deserialized state not visible as live objects. Do not penalize students for identifying fewer than two if the explanation and alternative strategy are rigorous.
- Recommended sequence: Tier 1 as individual warm-up (5 min), Tier 2 items 6 and 7 as pair work, items 8–10 as individual written work, Tier 3 as take-home, Tier 4 as optional extension.
