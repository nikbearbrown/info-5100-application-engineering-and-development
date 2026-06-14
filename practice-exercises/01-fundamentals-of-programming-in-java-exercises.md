# Module 1 — Fundamentals of Programming in Java: Exercises

---

## Learning Objectives Covered

- Distinguish the object model from the procedural model (state vs. behavior)
- Identify what state and behavior each object in a domain should own
- Apply the three-kinds-of-wrong framework (compilation error, runtime error, silent wrong behavior)
- Use the verification loop to confirm a program satisfies its business requirement

*Every exercise below maps to at least one of these objectives. The `(Tests: ...)` tag on each exercise identifies which one(s).*

---

## Worked Example

*Study this example before attempting Tier 1. After reading it, close it and try to recall the key steps from memory before moving on.*

**Problem:** A student writes a `LibrarySystem` class that has a method `checkoutBook(String patronId, String bookId)`. The method looks up the patron and book, calls `book.isCheckedOut = true`, and prints "Checkout complete." The program compiles and runs. The student says it works. Is this correct?

**Approach:**
1. **Identify the objects and their state.** `Book` holds `isCheckedOut` as state. `Patron` holds a checkout history as state.
2. **Check state ownership.** Who changed `book.isCheckedOut`? The `LibrarySystem` class changed it directly — not the `Book` object itself. This violates the object model principle: behavior that changes an object's state belongs inside that object.
3. **Apply the three-kinds-of-wrong.** Does it compile? Yes. Does it crash? No. Could it produce wrong behavior silently? Yes — the patron's checkout history was never updated. The program printed "Checkout complete" but no record of the checkout was associated with the patron.
4. **Apply the verification loop.** Business question: does a checkout record the patron who borrowed the book? Java artifact: which method updates the patron's checkout history? Observed behavior: after calling `checkoutBook()`, does the patron object show one active checkout? — It does not. Silent wrong behavior.

**Answer:** The program is not correct. It compiles and runs without exceptions, but it silently fails to update the patron's state. The verification loop reveals the gap: the Java artifact (`checkoutBook`) does not satisfy the full business requirement.

**What to notice:** "It compiles and prints the right message" is not the same as "it is correct." The three-kinds-of-wrong framework exists precisely because silent wrong behavior produces no signal — you have to look for it actively using the verification loop.

---

## Tier 1 — Warm-Up

*(Tests: recall, conceptual identification, true/false with explanation)*

**Exercise 1** *(Tests: state vs. behavior — core object model distinction)*

In the object model, what is the difference between **state** and **behavior**?

Give one example of each from a `Book` class in a library system.

---

**Exercise 2** *(Tests: three-kinds-of-wrong — compilation does not prove correctness)*

**True or False:** "If a Java program compiles without errors, it is correct."

State whether this is true or false, then explain your reasoning in two to three sentences.

---

**Exercise 3** *(Tests: three-kinds-of-wrong — classifying error types)*

Label each of the following as a **compilation error**, a **runtime error**, or **silent wrong behavior**. For each, write one sentence explaining why.

(a) A missing semicolon at the end of a statement.
(b) A `NullPointerException` thrown when the program tries to access a patron's name.
(c) A checkout method that assigns a book to the wrong patron but throws no exception and prints no error.

---

**Exercise 4** *(Tests: state vs. behavior — contrastive classification)*

Label each of the following as **state** or **behavior** in a `Patron` class for a library system. For each, write one sentence explaining your classification.

- (a) `String name`
- (b) `checkout(Book book)`
- (c) `int activeCheckoutCount`
- (d) `getOverdueBooks()`
- (e) `LocalDate memberSince`

*(Why this is tempting to get wrong: students often classify methods that read state — like `getOverdueBooks()` — as state rather than behavior, because they seem "passive." The distinction is: state is what the object holds; behavior is what the object does.)*

---

**Exercise 5** *(Tests: verification loop — three questions in order)*

What is the verification loop? List its three questions in order.

---

**Exercise 6** *(Tests: state ownership — behavior belongs with the object that owns the state)*

**True or False:** "In the object model, a method that changes a book's checkout status belongs in the `Book` class because `Book` is the object whose state changes."

State whether this is true or false, then explain your reasoning in two to three sentences.

---

## Tier 2 — Application

*(Tests: applying the three-kinds-of-wrong, verification loop, object model design)*

**Exercise 7** *(Tests: three-kinds-of-wrong — output does not prove correctness)*

A program that tracks student course registrations produces this output:

```
Registration complete for STUDENT001.
```

A classmate says: "It works!"

Using the three-kinds-of-wrong framework, explain what this output does and does not prove. What additional evidence would you need before you could say the program is correct?

---

**Exercise 8 — Error Analysis** *(Tests: state ownership — behavior outside the owning object)*

A student is designing a library checkout system. They write all checkout logic — including finding available books, updating checkout status, and recording due dates — inside a `Main` class rather than inside `Book` or `Patron` classes. The program runs and produces correct output for the test cases they tried.

(a) Identify the design problem.
(b) Identify the object model principle the student violated.
(c) Describe what breaks when you need to add a second type of checkout — for example, distinguishing e-book checkout from physical book checkout.

---

**Exercise 9** *(Tests: state and behavior ownership — identifying objects in a domain)*

You are modeling a hospital appointment system. Identify **three objects** in this system. For each object:
- List one piece of **state**
- List one **behavior**

Then explain which object should own the "schedule appointment" behavior and why, using state/behavior vocabulary.

---

**Exercise 10 — AI Interaction** *(Tests: state vs. behavior — AI produces state without behavior)*

First, without consulting AI, write one sentence answering: what is the minimum a Java class needs to be considered an object model, not just a data container?

Then read this AI-generated response to "Write me a Java class for a Book object":

```java
public class Book {
    public String title;
    public String author;
    public boolean isCheckedOut;
}
```

The student says: "Great, now I'm done."

(a) Identify the strongest point in the AI's response.
(b) Identify the most significant gap — what did the AI produce that is not yet a working object model?
(c) Write one sentence describing what is still missing.
(d) State the specific test you would run to verify whether a Book class actually implements the object model — what would you call, and what would you observe?

---

**Exercise 11 — Self-Explanation** *(Tests: verification loop — why three questions are necessary)*

In this chapter, the verification loop asks three separate questions rather than simply checking whether the program's output looks correct. Explain in 2–3 sentences why asking three distinct questions is preferable to checking output alone. Your explanation must use the term **"silent wrong behavior"** correctly.

---

**Exercise 12 — Cumulative** *(Tests: verification loop + three-layer diagnostic model from Ch 0)*

In Ch 0, you learned that the three-layer diagnostic model assigns failures to the toolchain, project, or program layer before looking for a cause. In this chapter, the verification loop is a program-layer check.

A library checkout program compiles without errors and prints "Checkout complete — Book: Dune, Patron: Alice." Apply both frameworks:

(a) Which layer does successful compilation verify? Which layer does the verification loop operate at?
(b) What kind of wrong from the three-kinds-of-wrong framework could still exist even though compilation succeeded and the output message printed?
(c) Name one specific thing you would check at the program layer that the output message does not tell you.

---

**Exercise 13** *(Tests: verification loop — applying all three questions with evidence)*

A classmate shows you a library checkout program. The output looks correct.

Apply the verification loop: write the **three questions** you would ask, in order, to determine whether the program actually satisfies the business requirement — not just whether the output appears correct.

For each question, describe what specific evidence you would look for.

---

## Tier 3 — Synthesis

**Exercise 14** *(Connects: Module 1 three-kinds-of-wrong + Module 0 three-layer diagnostic model)*

A student builds a library checkout object model that compiles and runs correctly on their machine. A second student runs the same code on a different machine and gets a runtime error — the program crashes with a `NoClassDefFoundError`.

Using both the **three-kinds-of-wrong framework** (Ch 1) and the **three-layer diagnostic model** (Ch 0):

(a) Which layer of the environment is likely responsible for the failure?
(b) Which "kind of wrong" is this — and why is it *not* a compilation error?
(c) What should the developer verify first, and at which layer?

> **What distinguishes a surface answer from a strong one:**
> - Names the specific layer from Ch 0 (toolchain) — not just "environment" or "their computer"
> - Correctly explains why this is a runtime error, not a compilation error, with a specific reason
> - States that the verification step is at the environment/toolchain layer, not in the code itself

---

**Exercise 15** *(Connects: Module 1 verification loop + Module 0 AI boundary rules)*

You have built an object model that correctly models a library system with `Book`, `Patron`, and `Checkout` classes. You want to ask an AI to help you add a "return book" feature.

Using the **AI boundary rules** from Ch 0 and the **verification loop** from Ch 1:

(a) Write the specific prompt you would give the AI. It should follow the Ch 0 diagnostic template.
(b) Describe the specific evidence you would collect to verify the AI's output before accepting it into your codebase.

> **What distinguishes a surface answer from a strong one:**
> - The prompt asks the AI to *explain* a design approach, not to generate the implementation for you
> - Verification includes running the program *and* checking the behavior against the stated business requirement
> - Does not treat AI-generated code as finished without running the verification loop

---

## Tier 4 — Challenge

**Exercise 16** *(Tests: object model design — behavior ownership tension)*

The object model places behavior inside the object that owns the relevant state. Design a scenario where this principle creates a genuine design tension: a behavior that **two different objects** could reasonably claim ownership of.

Describe both ownership claims, explain the trade-off between them, and defend a specific design choice. There is no single correct answer — your reasoning matters more than your conclusion.

**Rubric (no answer key provided for Tier 4):**

| Criterion | Strong Response |
|---|---|
| Scenario | Names a specific, concrete scenario involving real objects — not "Foo and Bar" |
| Ownership claims | States both arguments using state and behavior vocabulary from Ch 1 |
| Trade-off | Identifies what each design choice gains and what it gives up |
| Defense | Makes a specific choice and defends it with a reason beyond "it seems better" |
| Vocabulary | Uses object model terminology (state, behavior, ownership) accurately throughout |

---

## Answer Key — Exercises 1–15

**Worked Example**
*No answer needed — the worked example is its own model.*

---

**Exercise 1**
**State** is the data an object holds — the information that describes what the object *is* at a given moment. **Behavior** is what an object can *do* — the actions it can perform or the responses it can give.

Example from a `Book` class:
- State: `isCheckedOut` (a boolean field indicating whether the book is currently on loan)
- Behavior: `checkout()` (a method that changes the book's status and records a due date)

*Common error:* Students give behavior examples that are really state (e.g., "whether it is checked out" as a behavior). The test: can you store it in a field? If yes, it's state. Can it only exist as an action or process? Then it's behavior.

---

**Exercise 2**
**False.** Compilation only verifies that the program's syntax and types are valid — that the code can be translated into bytecode. It does not verify that the program does what it is supposed to do. A program can compile without errors and still produce the wrong output (silent wrong behavior) or crash at runtime (runtime error). Correctness requires more than compilation.

*Common error:* Students write "True" because "no errors means it's good." This conflates the absence of compile-time errors with the presence of correctness — the most important conceptual gap in this chapter.

---

**Exercise 3**

(a) **Compilation error.** The Java compiler requires a semicolon at the end of every statement; the absence of one prevents the source file from being compiled at all.

(b) **Runtime error.** The program compiled successfully (the type structure was valid), but during execution, the program attempted to access a field on a null reference, which the JVM cannot handle and reports as an exception.

(c) **Silent wrong behavior.** The program ran to completion without crashing, but the result is incorrect — the wrong patron is recorded as holding the book. There is no error message, exception, or compilation failure to alert the developer.

*Common error:* Students classify (c) as a runtime error because "something is wrong." Runtime errors produce exceptions that stop execution. Silent wrong behavior produces no signal — the program finishes normally.

---

**Exercise 4**
- (a) `String name` — **state.** It is data the object holds that describes a property of the patron.
- (b) `checkout(Book book)` — **behavior.** It is an action the patron performs.
- (c) `int activeCheckoutCount` — **state.** It describes a current property of the patron's situation.
- (d) `getOverdueBooks()` — **behavior.** It is a method — an action the object performs, even if that action is just reading and returning information.
- (e) `LocalDate memberSince` — **state.** It is a stored data value describing when the patron joined.

*Common error:* Students classify `getOverdueBooks()` as state because it "returns data about the patron." The key: if it's a method (something the object does), it's behavior — even if it only reads without modifying.

*Why this is tempting:* Getter methods feel passive, like reading a label. But the object model classifies by type: fields = state, methods = behavior, regardless of whether the method reads or writes.

---

**Exercise 5**
The verification loop asks three questions, in this order:

1. What is the **business question** — what real-world outcome is this program supposed to produce?
2. What is the **Java artifact** — what class, method, or data structure is responsible for producing that outcome?
3. What is the **observed behavior** — does running the program produce the outcome the business question requires?

The loop is a check that connects intent (what should happen) to evidence (what actually happened), rather than accepting "it compiled" or "the output looks right" as sufficient verification.

---

**Exercise 6**
**True**, with a clarification. In the object model, behavior belongs to the object that owns the relevant state. A `Book` holds checkout status as part of its state, so a method that changes that status belongs in `Book` — the object that owns what is being changed. Placing that method in `Main` or another class would mean one object is directly modifying another object's state from the outside, which breaks the principle that objects manage their own state.

---

**Exercise 7**
The output proves that the program reached the print statement and executed it without crashing. It does not prove that the registration was recorded correctly — the line "Registration complete for STUDENT001" could be printed regardless of whether the underlying data was actually updated.

Using the three-kinds-of-wrong framework: there is no compilation error (the program ran) and no runtime error (no exception was thrown). But silent wrong behavior is still possible — the registration record might be missing, duplicated, or associated with the wrong course.

Additional evidence needed:
- Verify that STUDENT001 now appears in the enrollment list for the correct course
- Verify that the course capacity was decremented
- Verify that a duplicate registration for the same student/course is rejected

---

**Exercise 8**

(a) The design problem is that checkout logic — which depends on both `Book` state and `Patron` state — is placed in `Main`, which is not the object that owns either.

(b) The student violated the principle that **behavior belongs to the object that owns the relevant state**. `Book` owns checkout status; `Patron` owns borrowing history. Checkout logic that reads and modifies both belongs in one of those classes (or in a dedicated `Checkout` class), not in `Main`.

(c) When you need to add e-book checkout, you must either duplicate the checkout logic in `Main` for the new case, or untangle the existing logic to place it correctly. Because `Main` is not an object with defined state or identity, it cannot be extended, subclassed, or varied — you can only add more branches to a growing if-else chain.

---

**Exercise 9**
Three objects in a hospital appointment system:

1. **Patient** — State: `dateOfBirth`; Behavior: `updateContactInfo()`
2. **Doctor** — State: `specialization`; Behavior: `getAvailableSlots()`
3. **Appointment** — State: `scheduledDateTime`; Behavior: `cancel()`

The "schedule appointment" behavior should belong to **Appointment** (or an `AppointmentScheduler` service). Scheduling changes the state of an `Appointment` object — it sets the time and links the patient and doctor. Neither `Patient` nor `Doctor` owns the appointment's state; `Appointment` does.

---

**Exercise 10**

(a) Strongest point: The AI correctly identified the three core fields a `Book` object needs — title, author, and a boolean for checkout status. This is a reasonable starting vocabulary for the object's state.

(b) Most significant gap: The AI produced only **state** — three public fields. It did not produce any **behavior**. A field declaration is not an object model; it is a data container. Without methods, there is no behavior, no encapsulation, and no way for the object to manage its own state.

(c) What is still missing: "The class has no methods — it defines what a `Book` *holds* but not what a `Book` *does*, and its public fields mean any other class can modify its data directly, violating encapsulation."

(d) Verification test: Instantiate the `Book` class, call `checkout()` on it, then inspect `book.isCheckedOut` directly. If the field is `true` and the method exists, the object model is functioning. If no `checkout()` method exists, the class is a data container, not an object with behavior. The test reveals whether behavior is present and whether it correctly manages state.

*Common error:* Students accept the AI's output because it "looks like a Java class." The gap is the absence of any methods — but students who don't yet have a clear picture of "object model vs. data container" cannot see the absence.

---

**Exercise 11**
The verification loop asks three questions because each question targets a different failure mode. Checking output alone only catches cases where the program produces visibly wrong text — it cannot detect **silent wrong behavior**, where the program produces correct-looking output while recording incorrect data underneath. A registration system can print "Registration complete" while failing to update the enrollment list; a checkout system can print "Checked out" while recording the wrong patron. The three-question loop forces the developer to connect the output to the actual state change the business requirement demands, not just to the printed message.

*Common error:* Students describe the loop as "more thorough checking" without naming silent wrong behavior or explaining why output alone fails to detect it.

---

**Exercise 12**

(a) Successful compilation verifies that the source code satisfies the **toolchain and project layers** — the code translated to bytecode without syntax or type errors. The verification loop operates at the **program layer** — it checks whether the program's behavior matches the business requirement at runtime.

(b) **Silent wrong behavior.** The program could compile and print the correct message while failing to update the `Patron` object's checkout history, record the correct due date, or mark the book as unavailable in the catalog. None of these failures produce a compiler error or a runtime exception.

(c) One specific program-layer check: after calling `checkoutBook(book, patron)`, inspect `patron.getActiveCheckouts().size()` and `book.isCheckedOut()` directly. If `patron.getActiveCheckouts().size()` is still 0 after a checkout, the verification loop has found a silent wrong behavior that the output message concealed.

*Common error:* Students say compilation verifies the "program layer." Compilation is a toolchain/project-layer event — it confirms the code is structurally valid, not that it behaves correctly.

---

**Exercise 13**
Three verification loop questions applied to the checkout program:

1. **Business question:** What should a checkout do? (e.g., "Mark the book as unavailable, add the book to the patron's active checkouts, and record a due date.")
   *Evidence:* A stated or written requirement. Ask the classmate before running anything.

2. **Java artifact:** Which class and method is responsible? (e.g., "The `checkout()` method in `Book`, or `checkoutBook()` in `LibrarySystem`.")
   *Evidence:* Read the method to confirm it updates the correct fields on the correct objects.

3. **Observed behavior:** After calling the method, does the patron's `activeCheckouts` list contain the book, and is `book.isCheckedOut` true?
   *Evidence:* Print these field values directly after the call — do not accept the "Checkout complete" message as proof.

---

**Exercise 14**

(a) The **toolchain layer** is likely responsible. `NoClassDefFoundError` means the JVM found the `.class` file when compiling but cannot locate it at runtime on the second machine — typically a JDK version mismatch, missing output directory, or compiled class not included in the transfer.

(b) This is a **runtime error** — not a compilation error. The code compiled without issue; the failure occurs only when the JVM attempts to load the class during execution. A compilation error would have prevented the `.class` file from being produced at all.

(c) Verify first at the **toolchain layer**: confirm the JDK version on the second machine matches the source compatibility level, and confirm the full set of `.class` files was transferred.

*Common error:* Students name "the second student's computer" instead of the toolchain layer. The answer must use the Ch 0 vocabulary. Students also frequently call this a compilation error because "the class wasn't found" — but the class was found at compile time. The failure is at runtime.

---

**Exercise 15**

(a) Sample prompt:
> "I am working on a library checkout system with `Book`, `Patron`, and `Checkout` classes. `Book` has `isCheckedOut` (boolean) and `dueDate` (LocalDate). I want to add a 'return book' feature that marks the book as available and closes the checkout record. I have not yet written this method. Can you explain which class should own the return behavior and why, based on which class holds the relevant state? Please do not generate the full implementation."

(b) Evidence to collect:
- Run the program after implementing; call the return method
- Verify `book.isCheckedOut` is `false`
- Verify the `Checkout` record is closed
- Apply the verification loop: does observed behavior match the business requirement?
- Do not accept AI-generated code as done simply because it compiled

*Common error:* The prompt asks the AI to generate the implementation rather than explain the design. Students who accept AI code without running the verification loop have skipped the program-layer check entirely.

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
- Tier 2: appropriate for graded homework (0.5–1.0% of course grade per item)
- Tier 3: appropriate for discussion posts or written assignments (1.0–2.0% each)
- Tier 4: appropriate for optional extension, extra credit, or capstone work

**Worked example note:** The worked example targets silent wrong behavior — the highest-value concept in this chapter and the hardest to internalize. If students struggle with Tier 1 after reading it, ask them to close the example and reproduce the three-step diagnosis (identify objects, check state ownership, apply three-kinds-of-wrong) from memory.

**Exercise 4 (Contrastive Classification):** The target misconception is classifying getter methods (`getOverdueBooks()`) as state. Use this as a brief class discussion: draw a two-column table (state / behavior) and populate it together before releasing students to work independently.

**Exercise 10 (AI Interaction):** The verification step (part d) is the most pedagogically important part. Students who name a specific field to inspect — not "I would run it and see" — have connected the object model to the verification loop. Students who say "it looks good" have not.

**Exercise 11 (Self-Explanation):** Students often write "it catches more bugs" without using "silent wrong behavior." Require the specific term. A response that says "silent wrong behavior occurs when the output looks correct but the data is wrong" has understood the chapter's core argument.

**Exercise 12 (Cumulative):** This exercise is the first time students must connect two frameworks from different chapters. Watch for students who say compilation is a "program layer" check — that confusion is common and needs correction before Ch 2.

**Common errors to watch for:**
- Classifying getter methods as state rather than behavior (Exercise 4)
- Treating "it compiled" as proof of correctness (Exercises 2, 12)
- Accepting AI-generated field declarations as a complete object model (Exercise 10)

**Scaffolding adjustments:**
- *For students who struggle with Tier 1:* Have them re-read "The Object Model" section specifically, focusing on the state/behavior distinction. Ask them to make a two-column table for `Book` before re-attempting.
- *For students who complete Tier 4 quickly:* Ask them to identify a domain where three or four objects all have a plausible claim to the same behavior, and propose a design pattern (not covered in this chapter) that resolves the tension.

**DEI note:**
All scenarios use library catalogs, hospital scheduling, and course registration — domains accessible to students from any background. No cultural or socioeconomic assumptions are embedded in any scenario.
