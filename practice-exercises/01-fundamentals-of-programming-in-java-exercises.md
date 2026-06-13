# Module 1 — Fundamentals of Programming in Java: Exercises

---

## Tier 1 — Warm-Up (Recall, True/False, Definition)

**Exercise 1** (Tests: LO1 — distinguish object model from procedural model)

In the object model, what is the difference between **state** and **behavior**?

Give one example of each from a `Book` class in a library system.

---

**Exercise 2** (Tests: LO3 — apply the three-kinds-of-wrong framework)

**True or False:** "If a Java program compiles without errors, it is correct."

State whether this is true or false, then explain your reasoning in two to three sentences.

---

**Exercise 3** (Tests: LO3 — apply the three-kinds-of-wrong framework)

Label each of the following as a **compilation error**, a **runtime error**, or **silent wrong behavior**. For each, write one sentence explaining why.

(a) A missing semicolon at the end of a statement.
(b) A `NullPointerException` thrown when the program tries to access a patron's name.
(c) A checkout method that assigns a book to the wrong patron but throws no exception and prints no error.

---

**Exercise 4** (Tests: LO4 — use the verification loop)

What is the verification loop? List its three questions in order.

---

**Exercise 5** (Tests: LO1 — distinguish object model from procedural model; LO2 — identify object state and behavior)

**True or False:** "In the object model, a method that changes a book's checkout status belongs in the `Book` class because `Book` is the object whose state changes."

State whether this is true or false, then explain your reasoning in two to three sentences.

---

## Tier 2 — Application (Scenarios, Error Analysis, AI Interaction)

**Exercise 6** (Tests: LO3 — apply the three-kinds-of-wrong framework)

A program that tracks student course registrations produces this output:

```
Registration complete for STUDENT001.
```

A classmate says: "It works!"

Using the three-kinds-of-wrong framework, explain what this output does and does not prove. What additional evidence would you need before you could say the program is correct?

---

**Exercise 7 — Error Analysis** (Tests: LO1 — distinguish object model from procedural model; LO2 — identify object state and behavior)

A student is designing a library checkout system. They write all checkout logic — including finding available books, updating checkout status, and recording due dates — inside a `Main` class rather than inside `Book` or `Patron` classes. The program runs and produces correct output for the test cases they tried.

(a) Identify the design problem.
(b) Identify the object model principle the student violated.
(c) Describe what breaks when you need to add a second type of checkout — for example, distinguishing e-book checkout from physical book checkout.

---

**Exercise 8** (Tests: LO2 — identify object state and behavior)

You are modeling a hospital appointment system. Identify **three objects** in this system. For each object:
- List one piece of **state**
- List one **behavior**

Then explain which object should own the "schedule appointment" behavior and why, using state/behavior vocabulary.

---

**Exercise 9 — AI Interaction** (Tests: LO2 — identify object state and behavior; LO4 — use the verification loop)

A student asked an AI: "Write me a Java class for a Book object."

The AI produced:

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

---

**Exercise 10** (Tests: LO4 — use the verification loop)

A classmate shows you a library checkout program. The output looks correct.

Apply the verification loop: write the **three questions** you would ask, in order, to determine whether the program actually satisfies the business requirement — not just whether the output appears correct.

For each question, describe what specific evidence you would look for.

---

## Tier 3 — Synthesis

**Exercise 11** (Tests: LO3 — Ch 1 × Ch 0) (Connects: Module 1 three-kinds-of-wrong + Module 0 three-layer diagnostic model)

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

**Exercise 12** (Tests: LO4 — Ch 1 × Ch 0) (Connects: Module 1 verification loop + Module 0 AI boundary rules)

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

**Exercise 13** (Tests: LO1, LO2 — object model design)

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

## Answer Key — Exercises 1–12

**Exercise 1**
**State** is the data an object holds — the information that describes what the object *is* at a given moment. **Behavior** is what an object can *do* — the actions it can perform or the responses it can give.

Example from a `Book` class:
- State: `isCheckedOut` (a boolean field indicating whether the book is currently on loan)
- Behavior: `checkout()` (a method that changes the book's status and records a due date)

---

**Exercise 2**
**False.** Compilation only verifies that the program's syntax and types are valid — that the code can be translated into bytecode. It does not verify that the program does what it is supposed to do. A program can compile without errors and still produce the wrong output (silent wrong behavior) or crash at runtime (runtime error). Correctness requires more than compilation.

---

**Exercise 3**

(a) **Compilation error.** The Java compiler requires a semicolon at the end of every statement; the absence of one prevents the source file from being compiled at all.

(b) **Runtime error.** The program compiled successfully (the type structure was valid), but during execution, the program attempted to access a field on a null reference, which the JVM cannot handle and reports as an exception.

(c) **Silent wrong behavior.** The program ran to completion without crashing, but the result is incorrect — the wrong patron is recorded as holding the book. There is no error message, exception, or compilation failure to alert the developer.

---

**Exercise 4**
The verification loop asks three questions, in this order:

1. What is the **business question** — what real-world outcome is this program supposed to produce?
2. What is the **Java artifact** — what class, method, or data structure is responsible for producing that outcome?
3. What is the **observed behavior** — does running the program produce the outcome the business question requires?

The loop is a check that connects intent (what should happen) to evidence (what actually happened), rather than accepting "it compiled" or "the output looks right" as sufficient verification.

---

**Exercise 5**
**True**, with a clarification. In the object model, behavior belongs to the object that owns the relevant state. A `Book` holds checkout status as part of its state, so a method that changes that status belongs in `Book` — the object that owns what is being changed. Placing that method in `Main` or another class would mean one object is directly modifying another object's state from the outside, which breaks the principle that objects manage their own state.

---

**Exercise 6**
The output proves that the program reached the print statement and executed it without crashing. It does not prove that the registration was recorded correctly — the line "Registration complete for STUDENT001" could be printed regardless of whether the underlying data was actually updated.

Using the three-kinds-of-wrong framework: there is no compilation error (the program ran) and no runtime error (no exception was thrown). But silent wrong behavior is still possible — the registration record might be missing, duplicated, or associated with the wrong course.

Additional evidence needed:
- Verify that STUDENT001 now appears in the enrollment list for the correct course
- Verify that the course capacity was decremented
- Verify that a duplicate registration for the same student/course is rejected

---

**Exercise 7**

(a) The design problem is that checkout logic — which depends on both `Book` state and `Patron` state — is placed in `Main`, which is not the object that owns either.

(b) The student violated the principle that **behavior belongs to the object that owns the relevant state**. `Book` owns checkout status; `Patron` owns borrowing history. Checkout logic that reads and modifies both belongs in one of those classes (or in a dedicated `Checkout` class), not in `Main`.

(c) When you need to add e-book checkout, you must either duplicate the checkout logic in `Main` for the new case, or untangle the existing logic to place it correctly. Because `Main` is not an object with defined state or identity, it cannot be extended, subclassed, or varied — you can only add more branches to a growing if-else chain. If the logic had been placed in `Book` (or a `CheckoutStrategy`), you could add a new subclass or implementation without touching existing code.

---

**Exercise 8**
Three objects in a hospital appointment system:

1. **Patient**
   - State: `dateOfBirth` (LocalDate)
   - Behavior: `updateContactInfo()` — updates the patient's stored phone number or address

2. **Doctor**
   - State: `specialization` (String)
   - Behavior: `getAvailableSlots()` — returns the doctor's open appointment times

3. **Appointment**
   - State: `scheduledDateTime` (LocalDateTime)
   - Behavior: `cancel()` — marks the appointment as cancelled and notifies affected parties

The "schedule appointment" behavior should belong to **Appointment** (or an `AppointmentScheduler` service), not to `Patient` or `Doctor`. The reason: scheduling an appointment changes the state of an `Appointment` object — it sets the time, links the patient and doctor, and creates a new record. Neither `Patient` nor `Doctor` owns the appointment's state; `Appointment` does. Placing the behavior where the state lives keeps the design coherent.

---

**Exercise 9**

(a) Strongest point: The AI correctly identified the three core fields a `Book` object needs — title, author, and a boolean for checkout status. This is a reasonable starting vocabulary for the object's state.

(b) Most significant gap: The AI produced only **state** — three public fields. It did not produce any **behavior**. A field declaration is not an object model; it is a data container. Without methods, there is no behavior, no encapsulation, and no way for the object to manage its own state. Making the fields `public` also removes encapsulation entirely.

(c) What is still missing: "The class has no methods — it defines what a `Book` *holds* but not what a `Book` *does*, and its public fields mean any other class can modify its data directly, violating encapsulation."

---

**Exercise 10**
Three verification loop questions applied to the checkout program:

1. **Business question:** What is the checkout program supposed to do? (Example: "When a patron checks out a book, the book's status should change to unavailable, the patron's checkout history should be updated, and the due date should be recorded.")

   *Evidence to look for:* A written or stated requirement. If none exists, ask the classmate to state the expected behavior before running anything.

2. **Java artifact:** Which class and method is responsible for producing this outcome? (Example: "The `checkout()` method in the `Book` class, or the `checkoutBook()` method in a `LibrarySystem` class.")

   *Evidence to look for:* The specific method — read it to confirm it is connected to the right state fields.

3. **Observed behavior:** Does running the program actually update the book's status, the patron's history, and the due date — not just print a message?

   *Evidence to look for:* After calling the checkout method, query the `Book` object's status field directly and print it. Query the `Patron` object's checkout history. Verify the due date was set to the correct value. Do not accept a printed message as proof.

---

**Exercise 11**

(a) The **toolchain layer** is likely responsible. The `NoClassDefFoundError` means the JVM found the `.class` file when compiling (or one machine compiled successfully) but cannot locate it at runtime on the second machine. This is typically caused by a difference in JDK version, missing output directory on the classpath, or a compiled class that was not included when the project was transferred.

(b) This is a **runtime error** — not a compilation error. The code compiled without issue; the failure occurs only when the JVM attempts to load the class during execution. A compilation error would have prevented the `.class` file from being produced at all. A `NoClassDefFoundError` means the class was available at compile time but not at runtime, which is an environment configuration issue, not a code syntax issue.

(c) The developer should verify first at the **toolchain/environment layer**: confirm that the JDK version on the second machine matches the source compatibility level the code was compiled with, and confirm that the full set of `.class` files was transferred, not just the `.java` source files.

---

**Exercise 12**

(a) Sample prompt following the Ch 0 diagnostic template:

> "I am working on a library checkout system in Java with three classes: `Book`, `Patron`, and `Checkout`. Each `Book` has a `title`, `author`, and `isCheckedOut` boolean. Each `Checkout` records a patron ID, book ID, and due date. I want to add a 'return book' feature that marks the book as available and closes the checkout record. I have not yet written any code for this. Can you explain which class should own the return behavior and why, based on which class holds the relevant state? Please do not generate the full implementation — I want to understand the design decision first."

(b) Evidence to collect before accepting the AI's output:
- Run the program after implementing the suggested design and call the return method
- Verify that `book.isCheckedOut` is `false` after the return
- Verify that the `Checkout` record is closed (not just that a message was printed)
- Apply the verification loop: confirm the observed behavior matches the business requirement (book is returnable, patron's active checkout count decreases)
- Do not accept the AI's code as done simply because it compiled

---

## Instructor Notes

**Pacing:** Tier 1 exercises work well as a 10-minute warm-up at the start of the session after students have read the chapter. Exercise 3 (classification) is particularly effective as a quick poll — show each scenario and ask for a show of hands before revealing the answer.

**Exercise 6 (Scenario):** Students frequently conflate "the output looks right" with "the program is correct." This exercise is designed to surface that conflation explicitly. Press students: *what would you have to see in the data, not the console, to believe it?*

**Exercise 7 (Error Analysis):** The most common shallow response is "it should be more organized." Push students to use specific vocabulary: which object owns the state that the behavior changes? The goal is for students to articulate *why* the placement is wrong, not just that it feels wrong.

**Exercise 9 (AI Interaction):** Many students will initially say the AI's response is complete because it "looks like a Java class." The pedagogical goal is for students to notice the absence of methods — and to recognize that fields alone are not an object model.

**Exercise 11 (Synthesis):** Students often answer (a) with "the second student's computer" rather than naming the toolchain layer. Require the specific layer name. Students also frequently confuse the `NoClassDefFoundError` with a compilation failure — the key distinction is that compilation succeeded on the first machine; the error only appeared at runtime on the second.

**Exercise 13 (Tier 4):** Good concrete scenarios for this exercise: a `processPayment()` method in an e-commerce system (does it belong to `Order`, `PaymentProcessor`, or `Customer`?); a `transferFunds()` method in a banking system (does it belong to the source `Account` or a `Transaction` object?). Weak responses will describe a trivial case or fail to argue both sides. Strong responses will acknowledge that both placements have merit and make a choice based on which object's state is primarily affected.

**LO Coverage:**
- LO1 (object model vs procedural): Ex 1, 5, 7, 13
- LO2 (state and behavior): Ex 1, 5, 8, 9, 13
- LO3 (three-kinds-of-wrong): Ex 2, 3, 6, 7, 11
- LO4 (verification loop): Ex 4, 10, 12
