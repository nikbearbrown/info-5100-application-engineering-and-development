# Module 2 — Methods, Arrays, and File Objects: Exercises

---

## Tier 1 — Warm-Up (Recall, True/False, Definition)

**Exercise 1** (Tests: LO1 — explain stack vs heap memory model)

What is the difference between a **reference variable** and the **object it points to**?

Write your answer as a one-sentence analogy involving a physical address and a building.

---

**Exercise 2** (Tests: LO2 — trace references through shared-reference scenarios)

**True or False:** "When you write `Patron patronB = patronA;`, Java creates a second `Patron` object with the same field values as `patronA`."

State whether this is true or false, then explain your reasoning in two to three sentences.

---

**Exercise 3** (Tests: LO1 — explain stack vs heap memory model)

Where does a **reference variable** live in memory? Where does the **object itself** live?

Why does this distinction matter when two reference variables point to the same object?

---

**Exercise 4** (Tests: LO3 — construct objects with correct constructors)

What happens if you create a `Patron` object without defining a constructor in the `Patron` class?

Describe what Java does automatically and what the resulting field values will be for a `String` field and an `int` field.

---

**Exercise 5** (Tests: LO4 — implement toString())

**True or False:** "Implementing `toString()` in a class is optional if you already have a `display()` method that prints to the console."

State whether this is true or false, then explain your reasoning in two to three sentences.

---

## Tier 2 — Application (Scenarios, Error Analysis, AI Interaction)

**Exercise 6** (Tests: LO2 — trace references through shared-reference scenarios)

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

**Exercise 7 — Error Analysis** (Tests: LO3 — construct objects with correct constructors)

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

**Exercise 8** (Tests: LO1 — explain stack vs heap memory model; LO2 — trace references)

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

**Exercise 9 — AI Interaction** (Tests: LO2 — trace references through shared-reference scenarios)

A student asked an AI: "My two Patron objects are changing each other's data and I don't know why."

The AI responded:

> "This happens because Java uses pass-by-reference for objects. To fix it, use the `clone()` method to make a copy of your object before assigning it."

(a) Identify the strongest point in this response.
(b) Identify the error or oversimplification in the AI's explanation.
(c) Write a corrected explanation of why the student's two "objects" are actually one object with two reference variables pointing to it.

---

**Exercise 10** (Tests: LO4 — implement toString())

A student has a `Product` class with three fields: `name` (String), `price` (double), and `inStock` (boolean).

(a) Write a complete `toString()` method for `Product` that returns a properly formatted string. Include all three fields in the output.
(b) Explain why `toString()` is preferred over a separate `display()` method when working with collections and debuggers.

---

## Tier 3 — Synthesis

**Exercise 11** (Tests: LO2 — Ch 2 × Ch 1) (Connects: Module 2 reference/heap model + Module 1 object state and behavior ownership)

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

---

**Exercise 12** (Tests: LO1 — Ch 2 × Ch 0) (Connects: Module 2 verification + Module 0 three-layer model + Module 1 verification loop)

A student completes their object model, compiles it successfully in NetBeans, and tells you: "I've verified my program."

Using the **verification loop from Ch 1** and the **three-layer model from Ch 0**, explain:

(a) What has the student actually verified, and at which layer?
(b) What has the student *not* verified?
(c) Describe one specific test they should run at the **program layer** and what evidence it would produce.

> **What distinguishes a surface answer from a strong one:**
> - Correctly states that compilation is a project-layer or toolchain-layer verification step, not a program-layer one
> - Names specific evidence from the program layer — describes a concrete test, not just "run it"
> - Correctly applies the three-layer vocabulary from Ch 0

---

## Tier 4 — Challenge

**Exercise 13** (Tests: LO1, LO2 — reference model and design)

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

## Answer Key — Exercises 1–12

**Exercise 1**
A reference variable is like a physical address written on a piece of paper — it tells you *where* a building is, but it is not the building itself; the building (the object) exists independently on the heap, and multiple pieces of paper can all contain the same address.

---

**Exercise 2**
**False.** The assignment `Patron patronB = patronA;` copies the *reference* — the memory address — stored in `patronA` into `patronB`. It does not create a new `Patron` object. After this assignment, both `patronA` and `patronB` point to the same single object on the heap. Modifying a field through `patronB` will be visible through `patronA` and vice versa, because they refer to the same object.

---

**Exercise 3**
A **reference variable** lives on the **stack** — it is a local variable that holds a memory address. The **object itself** lives on the **heap** — it is allocated there when `new` is called.

This distinction matters when two references point to the same object because any modification made through one reference immediately affects what the other reference sees. There is no independent copy; both references are windows into the same piece of heap memory. Treating them as independent objects leads to unexpected mutations.

---

**Exercise 4**
If no constructor is defined, Java automatically provides a **default no-argument constructor** that initializes the object with default field values. The `Patron` object can still be created with `new Patron()`.

Default values by type:
- A `String` field will be initialized to `null` (not to an empty string)
- An `int` field will be initialized to `0`

This can be a source of bugs if the program later calls methods on the `String` field without checking for null first.

---

**Exercise 5**
**False.** `toString()` and `display()` serve different purposes. `display()` prints to `System.out` — it is only useful when you explicitly call it. `toString()` is called automatically by Java in many contexts: when you pass an object to `System.out.println()`, when you concatenate an object into a String, when a debugger displays an object's value, and when a collection's `toString()` iterates over its elements. A class with only `display()` will show a raw memory address in all of these contexts. `toString()` makes the object integrate correctly with the language and tooling.

---

**Exercise 6**
**Predicted output:**
```
Charlie
Bob
```

**Explanation:** The statement `Patron p3 = p1;` does not create a new `Patron` object. It copies the reference stored in `p1` into `p3`. After this assignment, `p1` and `p3` both point to the same `Patron` object on the heap — the one originally created with name "Alice". When `p3.name = "Charlie"` is executed, it modifies the `name` field of that single shared object. Since `p1` still holds the same reference, `p1.name` now reflects the change. `p2` is a completely separate object and is unaffected.

---

**Exercise 7**

(a) The output of `b.display()` will be:
```
Clean Code by null
```
The `author` field was never assigned a value, so it holds its default value of `null`. When concatenated into the string, `null` is converted to the text "null".

(b) The design problem is that the constructor only accepts a `title` parameter. A `Book` object cannot be created with both `title` and `author` at construction time. This forces the caller to either leave `author` as null or set it manually after construction, which is error-prone and leaves the object in an incomplete, inconsistent state.

(c) The constructor should accept both `title` and `author` as parameters:
```java
public Book(String t, String a) {
    title = t;
    author = a;
}
```
This ensures that every `Book` object is fully initialized at the moment it is created. An object should not exist in a partially constructed state — requiring all essential state to be provided at construction time prevents null field bugs downstream.

---

**Exercise 8**

(a) During the loop, each call to `new Student(...)` allocates a new `Student` object on the **heap**. The reference variable `temp` lives on the **stack** and is reassigned on every iteration — it points to the newly created object for the duration of that iteration. The 30 objects all exist simultaneously on the heap, but after each iteration, `temp` no longer points to any previous object. By the end of the loop, `temp` holds a reference only to the 30th object.

(b) Setting `temp = null` removes the reference stored in `temp` — it does not affect the objects on the heap. The 29 earlier `Student` objects that `temp` no longer references are eligible for garbage collection, but "deleting" `temp` has no effect on the last object either, since setting a reference variable to null only clears that one variable. The object on the heap persists until no references point to it.

(c) They should have used an **array** (or an `ArrayList`) of `Student` references:
```java
Student[] students = new Student[30];
for (int i = 0; i < 30; i++) {
    students[i] = new Student("Student" + i, i + 18);
}
```
This would have allowed them to retain references to all 30 objects after the loop and access any individual student by index.

---

**Exercise 9**

(a) Strongest point: The AI correctly identifies that the root cause is related to how Java handles objects — the student's intuition that they have "two separate objects" is wrong, and the AI is pointing in the right direction.

(b) Error or oversimplification: The AI's claim that "Java uses pass-by-reference for objects" is a common and significant misconception. Java is *always* pass-by-value — what is passed is the *value of the reference* (the memory address), not the object itself, and not a reference in the C++ sense. Additionally, `clone()` is not a straightforward fix — it requires implementing `Cloneable`, performs only a shallow copy by default, and is widely considered a problematic API.

(c) Corrected explanation: The student does not have two `Patron` objects — they have one `Patron` object on the heap and two reference variables that both store the same memory address. When the code wrote `Patron patronB = patronA;`, it copied the address, not the object, so any change made through `patronB` is visible through `patronA` because both variables are looking at the same place in memory.

---

**Exercise 10**

(a) `toString()` implementation for `Product`:

```java
@Override
public String toString() {
    return "Product{name='" + name + "', price=" + price + ", inStock=" + inStock + "}";
}
```

Or a more user-facing format:

```java
@Override
public String toString() {
    String availability = inStock ? "In Stock" : "Out of Stock";
    return name + " - $" + price + " (" + availability + ")";
}
```

(b) `toString()` is preferred over `display()` for two reasons:

First, `toString()` is called automatically by Java whenever an object needs to be represented as a string — including inside `System.out.println(product)`, string concatenation (`"Item: " + product`), and when a collection such as `ArrayList<Product>` is printed. A `display()` method requires an explicit call and produces no usable return value.

Second, debuggers (including the NetBeans debugger) call `toString()` to show the object's state in the variables window. A class without `toString()` will display a raw memory address (`Product@7852e922`), which provides no diagnostic information. Implementing `toString()` makes debugging significantly more efficient.

---

**Exercise 11**
Sample strong response:

**Scenario:** A library system has a `Checkout` screen and a `Patron Detail` screen. Both screens receive the same `Patron` object from a central `LibraryDatabase`. The `Checkout` screen initially displays the correct patron name and shows "no active checkouts."

**Initial correct output:** Both screens show "Alice Chen — No active checkouts."

**The bug appears:** A staff member uses the `Checkout` screen to check out a book. The checkout logic modifies the `Patron` object's `activeCheckouts` list directly — `patron.activeCheckouts.add(checkout)`. Because the `Patron Detail` screen holds a reference to the *same* object (not a copy), it immediately shows the updated checkout list without being explicitly refreshed. This seems convenient, but when the staff member then cancels the checkout on the `Checkout` screen (before saving), the patron detail screen still shows the book as checked out — because the intermediate state was written directly to the shared object, and the cancel operation only cleared the `Checkout` screen's local UI state, not the object's field.

**Why this is a reference consequence:** Both screens hold the same reference. Any mutation to the object is immediately visible to all references. The design assumed the object was a local copy for the `Checkout` screen to work with; it was not.

**Ch 1 violation:** The `Checkout` screen — which is a UI component, not a domain object — is directly modifying the state of a `Patron` object. The behavior of updating checkout state belongs inside `Patron` or a `CheckoutService`, not in the screen. Placing mutation behavior outside the object that owns the state caused the side effect to be uncontrolled.

---

**Exercise 12**

(a) The student has verified that their code satisfies the **compiler's type and syntax rules** — this is primarily a project-layer verification (the NetBeans project configuration is correct, the source compiled to bytecode). It does not verify what the program does when it runs.

(b) The student has not verified:
- That the program runs without a runtime error
- That the program produces the correct output for any given input
- That the program's behavior matches the business requirement (the verification loop's third question)
- That the compiled `.class` files exist and are accessible (a file-system / toolchain-layer check from Ch 0)

(c) One specific program-layer test: Create a `Patron` object and a `Book` object in a test `main` method, call the checkout method, then print the book's `isCheckedOut` field and the patron's `activeCheckouts` count directly.

Evidence it would produce: If the field reads `true` and the count reads `1`, the behavior matches the requirement. If the field still reads `false`, the checkout method compiled but does not correctly update state — which is a silent wrong behavior (Ch 1, three-kinds-of-wrong), invisible to compilation but observable at the program layer.

---

## Instructor Notes

**Pacing:** Exercise 6 (tracing) is highly effective as a live in-class exercise — ask students to write their prediction on paper *before* any discussion, then reveal the output. The gap between prediction and actual output creates a productive moment for explaining the reference model.

**Exercise 2 vs Exercise 6:** These exercises are deliberately sequenced. Exercise 2 tests the conceptual understanding (true/false); Exercise 6 tests whether students can apply that understanding to a concrete trace. Students who answer Exercise 2 correctly but get Exercise 6 wrong have the concept but cannot yet trace execution — address this gap explicitly.

**Exercise 7 (Error Analysis):** The most common incomplete answer is "add an author parameter." Push students to articulate *why* — what principle requires a fully initialized object at construction time? Connect this to the Ch 1 concept of state: an object whose state is partially null is not a valid domain object.

**Exercise 9 (AI Interaction):** The "pass-by-reference" misconception is extremely common and the AI response here reflects what many AI tools actually produce. The goal is not to dismiss the AI's response entirely but to train students to identify the precise error. The correction — "pass-by-value of a reference" — is a subtle but important distinction.

**Exercise 11 (Synthesis):** Students frequently describe a scenario where the bug is "two variables have the same value," which is not a reference bug. The target scenario requires mutation through a shared reference producing an unintended side effect visible in a different part of the program. If students struggle, ask: "Where else does this object appear? Who else can see the change?"

**Exercise 12 (Synthesis):** The most common error is conflating "it compiled" with "it runs correctly." The three-layer model from Ch 0 is useful here: compilation is a project-layer check; running the program and observing behavior is a program-layer check. Students should be able to name both layers and explain what each verifies.

**Exercise 13 (Tier 4):** Strong responses will separate the two scenarios clearly. A common weakness is describing a scenario where references are "good" because the program works, and a scenario where they are "bad" because it does not — without explaining the mechanism. Require students to explain specifically *what the reference does* in each case, not just what the outcome is.

**LO Coverage:**
- LO1 (stack vs heap): Ex 1, 3, 4, 8, 12
- LO2 (trace references): Ex 2, 3, 6, 8, 9, 11
- LO3 (constructors): Ex 4, 7
- LO4 (toString): Ex 5, 10
