# Module 2 — Methods, Arrays, and File Objects: Exercises

---

## Learning Objectives Covered

- Explain the stack vs. heap memory model and where reference variables and objects live
- Trace references through shared-reference scenarios to predict program behavior
- Construct objects with correct constructors that fully initialize all required state
- Implement `toString()` so objects integrate with Java's language features and debuggers

*Every exercise below maps to at least one of these objectives. The `(Tests: ...)` tag on each exercise identifies which one(s).*

---

## Worked Example

*Study this example before attempting Tier 1. After reading it, close it and try to recall the key steps from memory before moving on.*

**Problem:** Trace the following code and predict the output:

```java
Patron p1 = new Patron("Alice", 25);
Patron p2 = p1;
p2.name = "Bob";
System.out.println(p1.name);
System.out.println(p2.name);
```

**Approach:**
1. **Line 1:** `new Patron("Alice", 25)` allocates a `Patron` object on the **heap** with `name = "Alice"`. The reference variable `p1` lives on the **stack** and stores the memory address of that heap object.
2. **Line 2:** `Patron p2 = p1;` copies the **reference** — the memory address — stored in `p1` into `p2`. No new object is created. Both `p1` and `p2` now point to the same heap object.
3. **Line 3:** `p2.name = "Bob"` follows `p2`'s reference to the heap object and modifies its `name` field. Since `p1` points to the same heap object, `p1.name` is now also "Bob".
4. **Lines 4–5:** Both print "Bob" — because there is only one object, and both variables refer to it.

**Answer:** Both lines print `Bob`.

**What to notice:** `p2 = p1` looks like it creates a copy, but it copies the address, not the object. The assignment `Patron p2 = p1` is the key moment — after it, there is still only one `Patron` on the heap.

---

## Tier 1 — Warm-Up

*(Tests: recall, stack vs. heap, reference semantics, constructors, toString)*

**Exercise 1** *(Tests: reference variable vs. object — stack vs. heap)*

What is the difference between a **reference variable** and the **object it points to**?

Write your answer as a one-sentence analogy involving a physical address and a building.

---

**Exercise 2** *(Tests: reference assignment — copies address, not object)*

**True or False:** "When you write `Patron patronB = patronA;`, Java creates a second `Patron` object with the same field values as `patronA`."

State whether this is true or false, then explain your reasoning in two to three sentences.

---

**Exercise 3** *(Tests: stack vs. heap — where variables and objects live)*

Where does a **reference variable** live in memory? Where does the **object itself** live?

Why does this distinction matter when two reference variables point to the same object?

---

**Exercise 4** *(Tests: stack vs. heap vs. reference — contrastive classification)*

Classify each of the following as living on the **stack**, the **heap**, or **both** (in the case of something that exists in both places). Write one sentence explaining each classification.

- (a) A reference variable declared inside a method
- (b) A `Patron` object created with `new Patron("Alice", 25)`
- (c) A local `int` variable inside a loop
- (d) An `ArrayList<Book>` created with `new ArrayList<>()`
- (e) The memory address stored in a reference variable

*(Why this is tempting to get wrong: students often say "the ArrayList lives on the stack" because the variable declaration appears inside a method. The variable lives on the stack; the ArrayList object it points to lives on the heap.)*

---

**Exercise 5** *(Tests: constructors — default values and incomplete initialization)*

What happens if you create a `Patron` object without defining a constructor in the `Patron` class?

Describe what Java does automatically and what the resulting field values will be for a `String` field and an `int` field.

---

**Exercise 6** *(Tests: toString() — automatic invocation vs. explicit display())*

**True or False:** "Implementing `toString()` in a class is optional if you already have a `display()` method that prints to the console."

State whether this is true or false, then explain your reasoning in two to three sentences.

---

## Tier 2 — Application

*(Tests: tracing references, constructor design, toString(), shared-reference debugging)*

**Exercise 7** *(Tests: trace references — shared reference mutation)*

Given this code:

```java
Patron p1 = new Patron("Alice", 25);
Patron p2 = new Patron("Bob", 30);
Patron p3 = p1;
p3.name = "Charlie";
System.out.println(p1.name);
System.out.println(p2.name);
```

**Before running:** predict the exact output of both print statements. Then explain why `p1.name` changed even though the code only assigned to `p3.name`.

---

**Exercise 8 — Error Analysis** *(Tests: constructors — incomplete initialization causes null fields)*

A student writes the following class:

```java
public class Book {
    String title;
    String author;

    public Book(String t) {
        title = t;
    }

    public void display() {
        System.out.println(title + " by " + author);
    }
}
```

They then create an object and call display:

```java
Book b = new Book("Clean Code");
b.display();
```

(a) What will the output of `b.display()` be? Write the exact output.
(b) Identify the design problem in this class.
(c) What should the constructor do differently, and why?

---

**Exercise 9** *(Tests: stack vs. heap — loop reference reassignment and null)*

A student management system creates 30 `Student` objects in a loop:

```java
Student temp;
for (int i = 0; i < 30; i++) {
    temp = new Student("Student" + i, i + 18);
}
```

After the loop, the student accesses `temp.name` and gets the last student's name. Then they set `temp = null`, expecting to "delete" that student from the system.

Explain:

(a) What happened in memory during the loop — where were the 30 objects created, and what happened to the reference `temp` with each iteration?
(b) Why did setting `temp = null` not delete any `Student` object?
(c) What data structure should they have used instead, and what would it have allowed them to do?

---

**Exercise 10 — AI Interaction** *(Tests: reference semantics — pass-by-value of a reference)*

First, without consulting AI, write one sentence answering: when Java passes an object to a method, does the method receive the object itself or something else?

Then read this AI response to "My two Patron objects are changing each other's data and I don't know why":

> "This happens because Java uses pass-by-reference for objects. To fix it, use the `clone()` method to make a copy of your object before assigning it."

(a) Identify the strongest point in this response.
(b) Identify the error or oversimplification in the AI's explanation.
(c) Write a corrected explanation of why the student's two "objects" are actually one object with two reference variables pointing to it.
(d) State the specific test you would run in the student's code to confirm whether they have one object or two — what would you inspect, and what result would tell you which case it is?

---

**Exercise 11 — Self-Explanation** *(Tests: constructors — fully initialized objects)*

In this chapter, the recommendation is to initialize all required fields in the constructor rather than leaving fields to be set with setter methods after construction. Explain in 2–3 sentences why constructing a fully initialized object is preferable to constructing an empty object and calling setters later. Your explanation must use the term **"null"** correctly, showing what risk it names.

---

**Exercise 12 — Cumulative** *(Tests: reference semantics + state ownership from Ch 1)*

In Ch 1, you learned that behavior belongs in the object that owns the relevant state. In this chapter, you have learned that reference assignment (`patronB = patronA`) copies the address, not the object.

A library system has a `CheckoutScreen` that retrieves a `Patron` from the database and calls `confirmationScreen.setPatron(patron)` before navigating. The `setPatron()` method stores the reference: `this.patron = patron`.

(a) After `setPatron()` is called, how many `Patron` objects exist on the heap?
(b) If `CheckoutScreen` later modifies `patron.name` to correct a typo, what does `confirmationScreen.patron.name` show?
(c) Using Ch 1 vocabulary, explain whether this is an intended design or a state ownership violation — and what would make it one vs. the other.

---

**Exercise 13** *(Tests: toString() — implementation and use in collections)*

A student has a `Product` class with three fields: `name` (String), `price` (double), and `inStock` (boolean).

(a) Write a complete `toString()` method for `Product` that returns a properly formatted string. Include all three fields in the output.
(b) Explain why `toString()` is preferred over a separate `display()` method when working with collections and debuggers.

---

## Tier 3 — Synthesis

**Exercise 14** *(Connects: Module 2 reference/heap model + Module 1 object state and behavior ownership)*

A classmate argues: "I can build any object model I want as long as it compiles and produces correct output. Internal memory structure doesn't matter to the user."

Using the **object model principles from Ch 1** (state and behavior ownership) and the **reference and heap model from Ch 2**, construct a scenario where this argument fails — where the internal memory structure directly causes a visible bug, even though the program compiled and initially produced correct output.

Describe:
- The concrete scenario and the initial "correct" output
- The moment the bug appears and what the user sees
- Why the bug is a direct consequence of how references work
- Which object model principle from Ch 1 the design violated

> **What distinguishes a surface answer from a strong one:**
> - The scenario is concrete — names real objects, not "Object A and Object B"
> - Shows specifically how a shared reference breaks state ownership from Ch 1
> - The bug is something the user can observe (wrong output, wrong data) — not a compiler warning

*Common error:* Students describe a scenario where the bug is "two variables have the same value," which is not a reference bug. The target scenario requires mutation through a shared reference producing an unintended side effect visible in a different part of the program.

---

**Exercise 15** *(Connects: Module 2 verification + Module 0 three-layer model + Module 1 verification loop)*

A student completes their object model, compiles it successfully in NetBeans, and tells you: "I've verified my program."

Using the **verification loop from Ch 1** and the **three-layer model from Ch 0**, explain:

(a) What has the student actually verified, and at which layer?
(b) What has the student *not* verified?
(c) Describe one specific test they should run at the **program layer** and what evidence it would produce.

> **What distinguishes a surface answer from a strong one:**
> - Correctly states that compilation is a project-layer or toolchain-layer verification step, not a program-layer one
> - Names specific evidence from the program layer — describes a concrete test, not just "run it"
> - Correctly applies the three-layer vocabulary from Ch 0

*Common error:* Students conflate "it compiled" with "it runs correctly." The three-layer model from Ch 0 is useful here: compilation is a project-layer check; running the program and observing behavior is a program-layer check. Students should be able to name both layers and explain what each verifies.

---

## Tier 4 — Challenge

**Exercise 16** *(Tests: reference model and design)*

Java's reference model means that passing an object to a method gives the method access to the same object in memory — not a copy of it.

Design **two distinct scenarios** in a multi-screen application (for example, a student enrollment system with a search screen, a detail screen, and a registration screen):

1. A scenario where shared references make the design **elegant** — where passing the same object to multiple parts of the program is a feature that simplifies the design.
2. A scenario where this same property causes a **subtle bug** — where a method modifies an object it received, producing an unintended side effect visible elsewhere in the application.

For each scenario:
- Describe the design concretely (name the classes and what they do)
- Explain why references help or hurt in that specific context
- State what a developer must understand about references to use them correctly in that design

**Rubric (no answer key provided for Tier 4):**

| Criterion | Strong Response |
|---|---|
| Scenario distinctness | Two genuinely different scenarios — not two variations of the same situation |
| Mechanism | Explains *why* the reference model helps or hurts — not just that it does |
| Concreteness | Names specific classes and operations — not "object A is passed to method B" |
| Design principle | Connects each scenario to a design principle, not just to "being careful" |
| Reference accuracy | Correctly describes what a reference is and what shared access means at the memory level |

---

## Answer Key — Exercises 1–15

**Worked Example**
*No answer needed — the worked example is its own model.*

---

**Exercise 1**
A reference variable is like a physical address written on a piece of paper — it tells you *where* a building is, but it is not the building itself; the building (the object) exists independently on the heap, and multiple pieces of paper can all contain the same address.

---

**Exercise 2**
**False.** The assignment `Patron patronB = patronA;` copies the *reference* — the memory address — stored in `patronA` into `patronB`. It does not create a new `Patron` object. After this assignment, both `patronA` and `patronB` point to the same single object on the heap. Modifying a field through `patronB` will be visible through `patronA` and vice versa, because they refer to the same object.

*Common error:* Students answer True because `=` in most everyday contexts means "make a copy." In Java, `=` on a reference type copies the address, not the object. The confusion is understandable and this exercise is designed to surface it directly.

---

**Exercise 3**
A **reference variable** lives on the **stack** — it is a local variable that holds a memory address. The **object itself** lives on the **heap** — it is allocated there when `new` is called.

This distinction matters when two references point to the same object because any modification made through one reference immediately affects what the other reference sees. There is no independent copy; both references are windows into the same piece of heap memory.

*Common error:* Students say "the object lives on the stack" because it was declared inside a method. Declarations of reference variables live on the stack; the objects they point to always live on the heap.

---

**Exercise 4**
- (a) **Stack.** Reference variables declared inside methods are local variables — they live on the stack and are discarded when the method returns.
- (b) **Heap.** `new Patron(...)` allocates the object on the heap. The reference variable that holds its address is on the stack, but the object itself is on the heap.
- (c) **Stack.** Local `int` variables are primitives; they live directly on the stack, not as references to heap objects.
- (d) **Both.** The reference variable for the `ArrayList` lives on the stack; the `ArrayList` object (and the array it uses internally) lives on the heap.
- (e) **Stack.** A memory address is a value stored inside a reference variable, which lives on the stack.

*Common error:* Classifying `ArrayList` as stack-only because "it's declared in the method." Students must distinguish the variable (stack) from the object the variable points to (heap).

*Why this is tempting:* All of these look like "just things in the method." The stack/heap distinction cuts across that intuition: primitives and reference variables go on the stack; any object created with `new` goes on the heap.

---

**Exercise 5**
If no constructor is defined, Java automatically provides a **default no-argument constructor** that initializes the object with default field values. The `Patron` object can still be created with `new Patron()`.

Default values by type:
- A `String` field will be initialized to `null` (not to an empty string)
- An `int` field will be initialized to `0`

This can be a source of bugs if the program later calls methods on the `String` field without checking for null first.

---

**Exercise 6**
**False.** `toString()` and `display()` serve different purposes. `display()` prints to `System.out` — it is only useful when you explicitly call it. `toString()` is called automatically by Java in many contexts: when you pass an object to `System.out.println()`, when you concatenate an object into a String, and when a debugger displays an object's value. A class with only `display()` will show a raw memory address (`Patron@7852e922`) in all of these contexts.

*Common error:* Students answer True because "both let you see the object's data." The difference is that `toString()` is invoked by the language automatically; `display()` requires an explicit call. If you forget to call `display()`, you see a memory address. `toString()` is always available.

---

**Exercise 7**
**Predicted output:**
```
Charlie
Bob
```

**Explanation:** The statement `Patron p3 = p1;` does not create a new `Patron` object. It copies the reference stored in `p1` into `p3`. After this assignment, `p1` and `p3` both point to the same `Patron` object on the heap — the one originally created with name "Alice". When `p3.name = "Charlie"` is executed, it modifies the `name` field of that single shared object. Since `p1` still holds the same reference, `p1.name` now reflects the change. `p2` is a completely separate object and is unaffected.

---

**Exercise 8**

(a) The output of `b.display()` will be:
```
Clean Code by null
```
The `author` field was never assigned a value, so it holds its default value of `null`. When concatenated into the string, `null` is converted to the text "null".

(b) The design problem is that the constructor only accepts a `title` parameter. A `Book` object cannot be created with both `title` and `author` at construction time.

(c) The constructor should accept both parameters:
```java
public Book(String t, String a) {
    title = t;
    author = a;
}
```
This ensures every `Book` object is fully initialized at the moment it is created. An object should not exist in a partially constructed state.

---

**Exercise 9**

(a) During the loop, each call to `new Student(...)` allocates a new `Student` object on the **heap**. The reference variable `temp` lives on the **stack** and is reassigned on every iteration. By the end of the loop, `temp` holds a reference only to the 30th object.

(b) Setting `temp = null` removes the reference stored in `temp` — it does not affect the objects on the heap. The 29 earlier `Student` objects that `temp` no longer references are eligible for garbage collection, but `temp = null` does not delete any object; it only clears that one stack variable.

(c) They should have used an **array** (or an `ArrayList`) of `Student` references:
```java
Student[] students = new Student[30];
for (int i = 0; i < 30; i++) {
    students[i] = new Student("Student" + i, i + 18);
}
```
This retains references to all 30 objects after the loop and allows access by index.

---

**Exercise 10**

(a) Strongest point: The AI correctly identifies that the root cause is related to how Java handles objects — the student's intuition that they have "two separate objects" is wrong, and the AI is pointing in the right direction.

(b) Error: The AI's claim that "Java uses pass-by-reference for objects" is a common and significant misconception. Java is *always* pass-by-value — what is passed is the *value of the reference* (the memory address). Additionally, `clone()` is not a straightforward fix — it requires implementing `Cloneable`, performs only a shallow copy by default, and is widely considered problematic.

(c) Corrected explanation: The student does not have two `Patron` objects — they have one `Patron` object on the heap and two reference variables that both store the same memory address. When the code wrote `Patron patronB = patronA;`, it copied the address, not the object. Any change made through `patronB` is visible through `patronA` because both variables are looking at the same place in memory.

(d) Verification test: Add the line `System.out.println(patronA == patronB);` immediately after the assignment. If it prints `true`, both variables refer to the same object (one object on the heap). If it prints `false`, they are two separate objects. In this bug scenario, it will print `true`.

*Common error:* Students accept "pass-by-reference" as correct because it sounds precise. The correction — "pass-by-value of a reference" — is subtle but important. Java never passes the object itself; it passes a copy of the address.

---

**Exercise 11**
Constructing a fully initialized object is preferable because it prevents the object from ever existing in a state where a required field is **null**. If a constructor accepts all required fields as parameters, it is impossible to create a `Book` without a title and author — the compiler enforces this. If fields are left uninitialized and set later with setters, the object can be used before the setters are called, causing `NullPointerException` at the moment any code tries to read or operate on the null field. Full initialization at construction time means the object is valid as soon as it exists.

*Common error:* Students say "it's cleaner" without naming null or explaining the specific risk. The answer must connect incomplete construction to the null default and to the NullPointerException consequence.

---

**Exercise 12**

(a) After `setPatron()` is called, **one** `Patron` object exists on the heap. Both `CheckoutScreen` and `confirmationScreen` hold a reference to the same object.

(b) `confirmationScreen.patron.name` shows the corrected name — because both references point to the same heap object. The change through one reference is immediately visible through the other.

(c) Whether this is intended or a violation depends on ownership. If `CheckoutScreen` is the canonical owner of the patron data and `confirmationScreen` is only displaying it, then both holding the same reference is acceptable — the confirmation screen should reflect the current state. But if `confirmationScreen` is supposed to display a snapshot of the patron data at the time of confirmation (e.g., the name before the typo was corrected), then sharing the reference violates state ownership — the screen is showing live data it does not control. The Ch 1 principle: the object that owns the state should manage changes to it. Uncontrolled mutation through a shared reference means neither screen is fully in control.

---

**Exercise 13**

(a) `toString()` implementation for `Product`:
```java
@Override
public String toString() {
    String availability = inStock ? "In Stock" : "Out of Stock";
    return name + " - $" + price + " (" + availability + ")";
}
```

(b) `toString()` is preferred because Java calls it automatically whenever an object appears in a context requiring a String — including `System.out.println(product)`, string concatenation, and printing any collection containing `Product` objects. A `display()` method requires an explicit call and returns nothing. Debuggers also call `toString()` to show object state in the variables panel; without it, the debugger shows a raw memory address.

---

**Exercise 14**
Sample strong response:

A library system has a `Checkout` screen and a `Patron Detail` screen. Both screens receive the same `Patron` object from a central `LibraryDatabase`. Initially both show "Alice Chen — No active checkouts."

The bug appears when the `Checkout` screen's logic calls `patron.activeCheckouts.add(checkout)` to stage an in-progress checkout before saving. Because the `Patron Detail` screen holds a reference to the *same* object, it immediately reflects the staged (unsaved) checkout. When the checkout is cancelled before saving, the checkout screen clears its local state — but the patron detail screen still shows the staged checkout because the object was mutated and the cancel only cleared the UI.

This is a direct consequence of references: both screens point to the same heap object. Any mutation is immediately visible to all holders. The Ch 1 violation: the `Checkout` screen — a UI component — directly modified the state of a `Patron` object. Behavior that changes `Patron` state belongs inside `Patron` or a `CheckoutService`, not in the screen.

*Common error:* Students describe a scenario where "two variables have the same name" — that's a shadowing issue, not a reference issue. The target scenario requires mutation through a shared reference producing an observable side effect in a different screen.

---

**Exercise 15**

(a) The student has verified that their code satisfies the **compiler's type and syntax rules** — a project-layer verification. Compilation confirms the source translated to bytecode without errors, not that the program behaves correctly.

(b) The student has not verified:
- That the program runs without a runtime error
- That the program produces the correct output for any given input
- That the program's behavior matches the business requirement (verification loop's third question)

(c) One specific program-layer test: Create a `Patron` object and a `Book` object in a test `main` method, call the checkout method, then print `book.isCheckedOut` and `patron.getActiveCheckouts().size()` directly. If `book.isCheckedOut` is `true` and the patron's checkout count increased by 1, the behavior matches the requirement. If either is wrong, there is silent wrong behavior — invisible to compilation, visible only at the program layer.

*Common error:* Students say compilation is a "program layer" check. Compilation is a toolchain/project-layer event — it confirms the code is structurally valid, not that it behaves correctly.

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

**Worked example note:** The worked example shows the reference copy in 4 steps. If students struggle with Exercise 7 after reading it, ask them to draw the heap and stack for each line before attempting the prediction. The visual model is often what's missing.

**Exercise 4 (Contrastive Classification):** The most common error is classifying `ArrayList` as stack-only. Use a diagram: draw the stack holding a reference arrow pointing to a heap box labeled "ArrayList object." Emphasize: the variable is on the stack; the object is always on the heap.

**Exercise 10 (AI Interaction):** The verification step (part d) — `System.out.println(patronA == patronB)` — is the key insight. Students who discover `==` tests reference equality (not value equality) are making a connection that will pay off throughout the course.

**Exercise 11 (Self-Explanation):** Students who write "because it's better practice" without naming null have not made the causal connection. Require them to name the specific failure: `NullPointerException` when an uninitialized field is accessed.

**Exercise 12 (Cumulative):** This bridges Ch 1 (state ownership) and Ch 2 (reference semantics). Part (c) is the synthesis question: when is shared reference intentional design vs. a state ownership violation? Students often say "it's always a violation." Push them toward the nuance: ownership matters more than sharing.

**Common errors to watch for:**
- Classifying ArrayList as stack-only (Exercise 4)
- Saying "Java uses pass-by-reference" (Exercise 10)
- Answering True to Exercise 6 (toString vs. display)

**DEI note:**
All scenarios use library catalogs, student management, and product inventory — domains universally accessible regardless of background.
