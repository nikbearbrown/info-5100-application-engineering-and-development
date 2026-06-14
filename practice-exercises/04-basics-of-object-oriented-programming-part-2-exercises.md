# Module 4 — Basics of Object-Oriented Programming Part 2: Exercises
**Topic:** Debugging methodology, hypothesis-isolate-test loop

---

## Learning Objectives Covered

- Form hypotheses about state divergence that are specific and falsifiable
- Use breakpoints to isolate evidence at the right location in the call chain
- Distinguish symptom from proximate cause and root cause
- Trace causal chains from observable symptom back to the underlying defect

*Every exercise below maps to at least one of these objectives. The `(Tests: ...)` tag on each exercise identifies which one(s).*

---

## Worked Example

*Study this example before attempting Tier 1. After reading it, close it and try to recall the key steps from memory before moving on.*

**Problem:** A library app shows the wrong patron name on the confirmation screen after every checkout. The checkout itself seems to work — the right book is recorded. Only the patron name displayed is wrong. Apply the hypothesis-isolate-test loop.

**Approach:**
1. **Identify the symptom.** The confirmation screen displays "Alice" even when "Bob" checked out a book. This is the observable wrong behavior — the symptom.
2. **Form a hypothesis.** The confirmation screen's `patron` field is not being updated between checkouts. Hypothesis: `confirmationScreen.setPatron(patron)` is either not being called, or it is being called with the previous patron's reference rather than the current one.
3. **Isolate evidence.** Set a breakpoint at the line `confirmationScreen.setPatron(patron)` in the checkout handler. Inspect the `patron` variable — does it hold "Bob" or "Alice"?
4. **Test the hypothesis.** If the breakpoint shows `patron.name = "Alice"` even though the user selected "Bob," the bug is earlier in the call chain — the `patron` variable was set incorrectly before reaching the setter. If the breakpoint is never hit, the setter call is missing entirely.
5. **Identify the root cause.** Suppose the variable `patron` in the checkout handler was set at the wrong point — it was assigned when the form opened, not when the user confirmed. This is the root cause: the reference was captured too early.

**Answer:** The root cause is not the confirmation screen — the screen received a stale reference. The proximate cause is that `setPatron()` was called with the wrong value. The root cause is the checkout handler assigning `patron` at the wrong moment.

**What to notice:** The symptom (wrong name on screen) pointed to the confirmation screen. The root cause was in the handler. Without the hypothesis-isolate-test loop, you might "fix" the confirmation screen and leave the real defect untouched.

---

## Tier 1 — Warm-Up

*(Tests: recall, conceptual identification, true/false with explanation)*

**Exercise 1** *(Tests: three levels of a bug — symptom, proximate cause, root cause)*

What are the three levels of a bug? Define symptom, proximate cause, and root cause. Give one example of each from a library checkout scenario.

---

**Exercise 2** *(Tests: root cause vs. symptom fix — fixing the wrong level)*

> "If changing a line of code makes the wrong output go away, you have fixed the bug."

State whether this is true or false. Explain your reasoning in two to three sentences.

---

**Exercise 3** *(Tests: hypothesis formation — falsifiable vs. vague)*

What is a hypothesis in the context of debugging? What makes a hypothesis "falsifiable" rather than vague?

---

**Exercise 4** *(Tests: symptom vs. proximate cause vs. root cause — contrastive classification)*

A library checkout app shows the message "Patron: null" on the confirmation screen. A student investigates and finds three potential explanations:

- (a) The confirmation screen has a `patronLabel` that reads `null` when displayed.
- (b) The confirmation screen's `setPatron()` method was never called before the screen was shown.
- (c) The checkout handler was written so that it retrieves the patron from the database after navigating, not before.

Classify each as a **symptom**, a **proximate cause**, or a **root cause**. Write one sentence explaining each classification.

*(Why this is tempting to get wrong: (a) and the symptom feel like the same thing — but the symptom is what you observe as a user; the proximate cause is the first code-level condition that produces it. The root cause is why the proximate cause exists.)*

---

**Exercise 5** *(Tests: step over vs. step into — breakpoint strategy)*

What is the difference between "step over" and "step into" in a debugger? When would you use each?

---

**Exercise 6** *(Tests: debugging as understanding — not trial-and-error)*

> "The best debugging strategy is to change code until the output looks correct, then stop."

State whether this is true or false. Explain your reasoning in two to three sentences.

---

## Tier 2 — Application

*(Tests: forming hypotheses, using breakpoints, distinguishing levels of a bug)*

**Exercise 7** *(Tests: hypothesis formation + breakpoint placement)*

A student registration system shows the correct student name on the confirmation screen after the first registration. On the second registration, it shows the previous student's name.

- (a) State a precise hypothesis about where state diverges.
- (b) Describe exactly where you would set a breakpoint to test it.
- (c) Describe what you would look for in the variables panel at that breakpoint.

---

**Exercise 8 — Error Analysis** *(Tests: proximate vs. root cause — symptom-level fix)*

A student debugs a bug where the wrong patron appears on the confirmation screen. They find the bug and make this fix: they add `patronLabel.setText("")` at the start of the checkout method to clear the label before each checkout. The bug no longer appears in testing.

- (a) Which level of the three-level model did the student address?
- (b) What is wrong with this fix?
- (c) What root cause did they fail to address?

---

**Exercise 9** *(Tests: causal chain — tracing symptom to root cause)*

Trace the following causal chain for a grade submission bug: *"The confirmation screen shows the wrong student's grade."*

Working backward from the symptom, identify:
- (a) One plausible proximate cause
- (b) One plausible root cause that could produce that proximate cause
- (c) One breakpoint location and what variable you would inspect there

---

**Exercise 10 — AI Interaction** *(Tests: hypothesis-isolate-test loop — AI as code fixer vs. diagnosis partner)*

First, without consulting AI, write the hypothesis you would form for this bug: a checkout always assigns the book to the first patron in the system, regardless of which patron the user selected.

Then read this scenario: A student has this bug and asks an AI: *"My checkout assigns to the wrong patron. Can you fix my code?"* — and pastes their 80-line `CheckoutHandler`. The AI rewrites the handler with a fix. The student runs it and the bug is gone.

- Identify what the student did **correctly**.
- Identify what the student **failed to do**.
- Write the specific question the student should have asked instead, based on the hypothesis-isolate-test loop.
- State the specific inspection step you would use to verify that the AI's fix addressed the root cause rather than the symptom.

---

**Exercise 11 — Self-Explanation** *(Tests: hypothesis formation — why falsifiability matters)*

In this chapter, a hypothesis must be **falsifiable** — it must predict a specific observation that could prove it wrong. Explain in 2–3 sentences why a vague hypothesis ("something is wrong with the checkout") is less useful than a falsifiable one ("the patron reference is null at the point `setPatron()` is called"). Your explanation must use the term **"breakpoint"** correctly to show what a falsifiable hypothesis enables.

---

**Exercise 12 — Cumulative** *(Tests: hypothesis-isolate-test loop + verification loop from Ch 1)*

In Ch 1, the verification loop asks: does the Java artifact do what the business requirement demands? In this chapter, the debugging loop asks: where in the code does actual state diverge from intended state?

A library checkout program passes visual inspection — the output looks correct. A few days later, a new bug is discovered: patron checkout histories are incorrect.

(a) Which loop should have been used during development to catch this bug before deployment? What question would it have asked?
(b) Which loop applies now that the bug has been discovered? What is the first step?
(c) Explain the difference in what each loop detects — what the verification loop finds vs. what the debugging loop finds.

---

**Exercise 13** *(Tests: precise hypothesis + breakpoint — falsifiable prediction)*

You observe that a product inventory app correctly saves new products when the app first runs, but after editing a product and saving, the original unedited product reappears on restart.

Write a precise, falsifiable hypothesis about where state diverges. Identify the specific breakpoint and variable you would inspect to test it.

---

## Tier 3 — Synthesis

**Exercise 14** *(Connects: Module 4 + Module 2 reference semantics)*

In Ch 2, you learned that two references can point to the same object. In Ch 4, you learned that bugs often arise from the intent-execution gap.

Describe a scenario where a shared reference (Ch 2) creates a bug that manifests as a symptom (Ch 4) that looks like a logic error rather than a memory error. Explain:
- (a) The symptom a developer would observe
- (b) How you would form a hypothesis about the cause
- (c) Why the root cause is a reference issue, not a logic issue

**What distinguishes a surface answer from a strong one:**
- Scenario is concrete and plausible (use a library or student system)
- Hypothesis is falsifiable and specific
- Correctly identifies reference mechanics as root cause, not a conditional or calculation mistake

*Common error:* Students describe a scenario where "two variables have different values" — that's a value bug, not a reference bug. The target scenario requires mutation through a shared reference appearing as an unexpected change elsewhere in the program.

---

**Exercise 15** *(Connects: Module 4 + Module 1 verification loop)*

The verification loop from Ch 1 says to ask: "Does the Java artifact do what the business requires?" The debugging loop from Ch 4 says to form a hypothesis and isolate evidence.

Explain how these two loops relate:
- When does the verification loop detect that something is wrong?
- When does the debugging loop take over?
- Give a concrete example from a library or student system where you would use each loop.

**What distinguishes a surface answer from a strong one:**
- Uses specific vocabulary from both chapters
- Clearly distinguishes detection (verification) from diagnosis (debugging)
- Concrete example shows both loops applied correctly, not just described abstractly

*Common error:* Students treat the two loops as synonymous ("both check if the program works"). The distinction: verification loop detects *that* something is wrong by comparing observed behavior to a requirement; debugging loop diagnoses *why* by forming and testing hypotheses about state divergence.

---

## Tier 4 — Challenge

**Exercise 16 — Breakpoint-Resistant Bugs** *(No answer key — rubric only)*

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

**Worked Example**
*No answer needed — the worked example is its own model.*

### Tier 1 Answers

**Exercise 1**
- **Symptom:** The observable wrong behavior — what the user or tester sees. Example: the confirmation screen displays "Patron: null" after a checkout.
- **Proximate cause:** The immediate code condition that produces the symptom. Example: `confirmationScreen.patronLabel` is null when `setText(...)` is called.
- **Root cause:** The underlying design or logic error that created the proximate cause. Example: `setPatron(...)` was never called on the confirmation screen before it was displayed.

---

**Exercise 2**
**False.** Making the wrong output disappear addresses the symptom, not necessarily the root cause. The underlying defect may still exist and will resurface under different inputs or conditions. A correct fix requires understanding *why* the wrong output occurred and addressing that cause.

*Common error:* Students answer True because "if it's gone, it's fixed." The problem: the fix might have introduced a different code path that avoids the symptom without correcting the defect. The next input variation exposes it again.

---

**Exercise 3**
A hypothesis in debugging is a specific, testable claim about where and why state diverges from what the program intends. A hypothesis is falsifiable when it specifies a concrete location (a method, a variable, a line) and a predicted state (a specific value or reference) that can be confirmed or refuted by inspecting the program at runtime. A vague hypothesis — "something is wrong with the checkout" — cannot be tested because it does not predict what to observe.

---

**Exercise 4**
- (a) **Symptom.** "Patron: null" is what the user observes — it is the visible wrong behavior, not an explanation of why it occurs.
- (b) **Proximate cause.** The setter never being called is the immediate code-level condition that produces the null display. It is directly responsible for (a).
- (c) **Root cause.** The checkout handler retrieving the patron after navigating is the underlying design error that causes the setter to be absent. It is the reason (b) exists.

*Common error:* Students classify (a) and (b) as the same level because both involve "null." The distinction: (a) is what the user sees; (b) is the first code-level condition that produces it. The symptom is in the UI; the proximate cause is in the event flow.

*Why this is tempting:* "Patron: null" and "setPatron was never called" both describe "null" — but one is observable output, the other is a code-level event. The three-level model separates observation from cause.

---

**Exercise 5**
"Step over" executes the current line as a single unit and pauses on the next line, without entering any method called on that line. "Step into" enters the method being called on the current line and pauses at its first statement. Use step over when you are confident the called method is correct and want to move through the calling method quickly. Use step into when the bug may be inside the called method and you need to observe its internal execution.

---

**Exercise 6**
**False.** Changing code randomly until output looks correct is guessing, not debugging. It can mask symptoms without addressing the root cause, introduce new bugs, and leaves the developer without understanding of what was wrong. A correct debugging process requires forming a hypothesis, finding evidence, and confirming the root cause before making a change.

*Common error:* Students answer True because "the goal is to make it work." The problem: trial-and-error produces a program the developer doesn't understand. The next related bug will be just as mysterious.

---

### Tier 2 Answers

**Exercise 7**
- (a) Hypothesis: The confirmation screen's `Student` reference is not being updated between registrations. The screen was set with the first student object and never reset when the second registration began — either `setStudent(...)` is not called before the second display, or the same student object is being mutated rather than replaced.
- (b) Set a breakpoint at the line in the registration flow where `confirmationScreen.setStudent(student)` is called — specifically just before the second `layout.show(container, "confirmation")` call.
- (c) Inspect the `student` variable: confirm its `name` field matches the second student's name, not the first. Also inspect `confirmationScreen`'s student field to verify it is updated to the new reference after the setter call.

---

**Exercise 8**
- (a) The student addressed the **symptom** — the visible wrong text in the label — not even the proximate cause.
- (b) Clearing the label at the start of checkout hides the wrong display but does not fix the underlying issue. If the patron reference is incorrect, the label will still be populated with wrong data during the checkout — just with a blank flash first.
- (c) The root cause — likely that `setPatron(...)` was called with the wrong patron object, or that the confirmation screen's patron reference was never properly updated — was never identified or fixed.

---

**Exercise 9**
- (a) Proximate cause: The `GradeRecord` object displayed by the confirmation screen holds a reference to the previous student's data — `confirmationScreen.gradeRecord.student` points to the wrong `Student` object.
- (b) Root cause: The `GradeEntry` screen creates a new `GradeRecord` but assigns it a reference to a `Student` field that was never updated after the first submission — the field still holds the first student's reference.
- (c) Set a breakpoint inside the `GradeEntry` screen's submit handler, on the line that creates the `GradeRecord`. Inspect the `student` variable to verify it holds the correct second student's identity before the record is created.

---

**Exercise 10**
- **Correctly:** The student identified the symptom precisely ("assigns to the wrong patron") and provided enough context (the full handler) for the AI to attempt a fix.
- **Failed to do:** The student did not form a hypothesis, did not identify the proximate or root cause, and did not verify that the AI's fix addressed the actual defect. The student now has a working program they do not understand.
- **Better question:** "I suspect the bug is in how the selected patron is retrieved before being passed to the checkout method. My hypothesis is that `getSelectedPatron()` is returning the first patron in the list instead of the one the user selected. Can you help me understand what `getSelectedPatron()` does and whether my hypothesis is correct?"
- **Verification step:** After applying the AI's fix, set a breakpoint at the line where the patron is retrieved before the checkout is called. Inspect the patron's `name` field. If it matches the patron the user actually selected (not the first in the list), the root cause was addressed. If the name still doesn't match the user's selection, the AI changed something superficial and the root cause remains.

*Common error:* Students say "verify it works" without naming a specific inspection point. The verification step must identify what to look at and what result confirms root-cause resolution.

---

**Exercise 11**
A falsifiable hypothesis enables productive use of a **breakpoint** because it predicts what you will see at a specific location. "Something is wrong with the checkout" cannot be tested with a breakpoint — it tells you nothing about where to pause or what to look for. "The patron reference is null at the point `setPatron()` is called" tells you exactly where to set the breakpoint (the `setPatron()` call) and exactly what to inspect (the patron argument). If the patron is null there, the hypothesis is confirmed. If it is non-null, the hypothesis is refuted and you must revise it. Falsifiability converts debugging from guessing into evidence gathering.

*Common error:* Students say "a falsifiable hypothesis is more specific" without showing what it enables. The answer must explain the connection: falsifiability → predictable inspection point → breakpoint placement → evidence.

---

**Exercise 12**
(a) The **verification loop** from Ch 1 should have been used during development. It would have asked: does the checkout method actually update the patron's checkout history, not just print "Checkout complete"? Running the program and inspecting the patron's history field directly — not just the console output — would have caught the bug.

(b) The **debugging loop** from Ch 4 applies now. The first step: form a hypothesis about where patron histories diverge from expected state — e.g., "the `addToHistory()` call is being made on the wrong patron object, or it is not being called at all."

(c) The verification loop detects *that* something is wrong by comparing observed behavior to the business requirement — it surfaces the gap between intent and output. The debugging loop diagnoses *why* — it forms hypotheses and traces execution to find where state diverges. Verification is detection; debugging is diagnosis. You need both: verification tells you there is a bug; debugging tells you where it is.

---

**Exercise 13**
Hypothesis: The edit operation creates a modified `Product` object in memory but does not persist it to the data store — the original object in the store is never replaced, so on restart the store reloads the original. Specifically, the `save()` method may be updating a local variable rather than replacing the entry in the product list or file.

Breakpoint: Set a breakpoint at the end of the save method, after the persistence call. Inspect the data store (the list or file-write buffer) to verify the entry for the edited product ID now reflects the new field values. If the store still shows the old values at this point, the save method is not writing through correctly.

---

### Tier 3 Answers

**Exercise 14**
Consider a library search screen that stores the last-found `Book` in a field `currentBook`, then calls `detailScreen.setBook(currentBook)`. Later, the search is run again and the code calls `currentBook.setTitle(newTitle)` to update the displayed search result in-place rather than creating a new object. The symptom is that the detail screen now shows the new title — even though the user never navigated back to the detail screen. A developer observing this would form the hypothesis: "the detail screen's `setBook` method has a bug that makes it react to changes it was never told about." But the root cause is that both the search screen and the detail screen hold a reference to the *same* `Book` object; mutating it through one reference is immediately visible through the other. No logic bug exists in either screen — the design error is sharing a mutable object across screens without controlling mutation.

*Common error:* Students describe "two variables with the same value" or "a variable that changed unexpectedly" — these are value problems, not reference problems. The scenario must show mutation through one reference appearing as a change visible through another reference pointing to the same heap object.

---

**Exercise 15**
The verification loop from Ch 1 operates at the boundary between the program and the business requirement: you run the program, observe its output, and ask whether that output matches what was specified. It detects that something is wrong — a wrong value, a missing record, a crash — but does not explain why. The debugging loop from Ch 4 takes over once the verification loop has detected a failure: you form a hypothesis about where state diverged from intent, set a breakpoint to isolate evidence, and confirm or refute the hypothesis before changing code.

Example: In a library system, the verification loop detects that a checkout confirmation shows the wrong patron name (the output does not match the requirement "show the name of the patron who just checked out"). The debugging loop then takes over: form a hypothesis ("the confirmation screen's patron field was set before the user selected a patron"), set a breakpoint on `setPatron(...)`, inspect the patron reference, and confirm that the setter was called with a stale reference from a previous session. The verification loop told us *that* something was wrong; the debugging loop told us *why*.

*Common error:* Students treat the loops as sequential steps in one process, rather than two distinct activities. The verification loop is done at any time to confirm correctness; the debugging loop is triggered by a verification failure and focuses on a specific defect.

---

## Instructor Notes

**Suggested point distribution:**
- Tier 1: 5 points per item
- Tier 2: 10 points per item
- Tier 3: 15 points per item
- Tier 4: 20 points

**Bloom's distribution for this chapter:**

| Tier | Exercises | Bloom's Level | % of Set |
|---|---|---|---|
| Tier 1 — Warm-up | Ex 1–6 | Remember / Understand | ~25% |
| Tier 2 — Application | Ex 7–13 | Apply / Analyze | ~55% |
| Tier 3 — Synthesis | Ex 14–15 | Analyze / Evaluate | ~12% |
| Tier 4 — Challenge | Ex 16 | Evaluate / Create | ~8% |

**Assignment recommendations:**
- Tier 1: appropriate for completion credit or pre-class preparation
- Tier 2: appropriate for graded homework
- Tier 3: appropriate for discussion posts or written assignments
- Tier 4: appropriate for optional extension or extra credit

**Worked example note:** The worked example traces the full hypothesis-isolate-test loop on a patron name bug. After students read it, ask them to close it and reconstruct the five steps from memory. Students who can name "symptom → hypothesis → isolate → test → root cause" from memory are ready for Tier 2.

**Exercise 4 (Contrastive Classification):** The most common error is classifying (a) and (b) as both being the symptom. Use the clarification: symptom = what the user observes; proximate cause = first code-level condition. Draw a vertical chain: root cause → proximate cause → symptom. Students need to place each item at exactly one level.

**Exercise 8 (Error Analysis):** Exercise 8 is the critical item in this module. Students who say the student "fixed the bug" have not grasped the three-level model. Use this item to open discussion about what "fixing" means. Award zero points for answers that call the symptom-fix a valid solution.

**Exercise 10 (AI Interaction):** The verification step (part 4) is the most important part. Students who name a specific breakpoint location and specific variable value to inspect have understood the hypothesis-isolate-test loop. Students who say "run the program and check it works" have not — they are still in symptom-checking mode.

**Exercise 11 (Self-Explanation):** Students often write "a falsifiable hypothesis is more precise" without connecting precision to the breakpoint. The target explanation must show the chain: falsifiable → predicts observation → tells you where to place the breakpoint → produces confirming or refuting evidence.

**Exercise 12 (Cumulative):** This exercise is the key cross-chapter connection. Students who conflate the verification loop and debugging loop are treating "does it work?" and "why doesn't it work?" as the same question. Require them to distinguish detection (verification) from diagnosis (debugging).

**Exercise 14 (Synthesis):** Students frequently describe a scenario where "the bug is hard to find" — without explaining the reference mechanism. Require them to name the specific object, the specific mutation, and the specific reference holder that sees the unexpected change.

**Exercise 16 (Tier 4):** Common strong answers identify: (1) timing/concurrency bugs where pausing a thread changes interleaving; (2) bugs that only manifest under production load; (3) bugs involving serialized/deserialized state not visible as live objects. Do not penalize students for identifying fewer than two if the explanation and alternative strategy are rigorous.

**DEI note:**
All scenarios use library catalogs, hospital scheduling, and student grade systems — domains universally accessible regardless of background.
