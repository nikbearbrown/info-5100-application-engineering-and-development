# Module 3 — Objects and Classes: Exercises
**Topic:** Multi-screen flows, CardLayout, state management
**Learning Objectives:**
1. Design multi-screen flows with state transitions
2. Implement CardLayout navigation
3. Trace object references through user flows
4. Diagnose lost-reference and premature-display failures

---

## Tier 1: Warm-up

**1. Recall** *(Tests: LO1 — setter-before-show contract)*

In a multi-screen application, what is the setter-before-show contract? Why does violating it cause a `NullPointerException`?

---

**2. True/False + Explain** *(Tests: LO3 — shared references vs. screen independence)*

> "Each screen in a CardLayout application should create its own copy of the Book object it needs to display, so screens are independent of each other."

State whether this is true or false. Explain your reasoning in two to three sentences.

---

**3. Vocabulary** *(Tests: LO1 — flow table)*

What is a flow table? What four columns does it contain, and why is specifying the "state change" column particularly important when designing multi-screen applications?

---

**4. CardLayout** *(Tests: LO2 — CardLayout navigation)*

What does the call `layout.show(container, "checkout")` do? What must be true before this call executes for the checkout screen to display correctly?

---

**5. True/False + Explain** *(Tests: LO1 — separation of concerns)*

> "Mixing navigation logic (which screen to show) with domain logic (how to process a checkout) inside the same method is acceptable if the class is small enough."

State whether this is true or false. Explain your reasoning in two to three sentences.

---

## Tier 2: Application

**6. Scenario** *(Tests: LO3 — object travel between screens)*

A hospital appointment app has three screens: `PatientSearch` → `AppointmentDetails` → `Confirmation`. A patient object is found on the search screen.

Describe:
- (a) How the patient object should travel to the `AppointmentDetails` screen
- (b) What method should be called before showing that screen
- (c) What happens if the screen is shown before the patient is set

---

**7. Error Analysis** *(Tests: LO4 — premature display and setter-before-show)*

A student's library checkout flow has this code on the checkout screen's "Confirm" button:

```java
confirmButton.addActionListener(e -> {
    Book book = catalog.findByIsbn(isbnField.getText());
    Patron patron = new Patron(nameField.getText(), idField.getText());
    checkout(book, patron);
    layout.show(container, "confirmation");
    confirmationScreen.setResult("Done");
});
```

Identify **two design problems**. For each problem:
- Name the problem
- Explain what will go wrong at runtime
- Describe the fix

---

**8. Flow Table** *(Tests: LO1 — flow table design)*

Design a flow table for a 3-screen student grade submission app with screens: `CourseList` → `GradeEntry` → `Submission`.

For each transition, specify:
- (a) The user action that triggers it
- (b) The object involved
- (c) The state change that must happen
- (d) Which screen "owns" that state

---

**9. AI Interaction** *(Tests: LO3 — shared references, separation of concerns)*

A student asked an AI: *"How do I pass data between screens in a Java Swing application?"*

The AI responded:

> "The easiest way is to use static variables. Make your data static and access it from any screen using the class name. For example: `Main.currentBook = selectedBook;`"

- Identify the **strongest point** in the AI's response.
- Identify the **design problem** with using static variables for screen-to-screen data.
- Write a **one-paragraph correction** explaining the proper approach.

---

**10. Diagnosis** *(Tests: LO4 — lost reference and premature display failures)*

A student's book detail screen shows `null` for all fields even though the search returned a valid book. The screen itself was written correctly.

Using the two failure modes from this chapter (lost reference and premature display), explain:
- The two most likely causes
- How you would diagnose which one is occurring

---

## Tier 3: Synthesis

**11. Synthesis (Ch 3 + Ch 2)** *(Tests: LO3 + Ch 2 reference semantics)*

In Ch 2, shared references allow two variables to point to the same object. In Ch 3, passing an object reference between screens is the correct design.

Explain:
- (a) How the same reference mechanism that caused bugs in Ch 2 is the feature that makes multi-screen data passing work correctly in Ch 3
- (b) What the difference is between a "shared reference bug" and "intentional reference passing"
- (c) What design principle prevents the former while enabling the latter

**What distinguishes a surface answer:**
- Distinguishes accidental vs. intentional sharing
- Names the specific design principle (screen ownership of state)
- Uses reference vocabulary from Ch 2 correctly

---

**12. Synthesis (Ch 3 + Ch 1)** *(Tests: LO1 + Ch 1 object model)*

The object model from Ch 1 says behavior belongs in the object that owns the relevant state. Apply this to a multi-screen application: which object should own the "navigate to next screen" behavior — the current screen, a separate navigator object, or the main application?

Defend your answer using both the object model principle from Ch 1 and the separation of concerns principle from Ch 3.

**What distinguishes a surface answer:**
- Names specific state that each candidate object owns
- Uses object model vocabulary from Ch 1
- Makes a defensible choice with reasoning, not just assertion

---

## Tier 4: Challenge

**13. Capstone — Lazy Screen Construction** *(No answer key — rubric only)*

`CardLayout` requires that all screens exist before the application starts. This means you must construct every screen object upfront, even if the user never visits some screens.

Design an alternative approach that constructs screens on demand (lazily). Describe:
- (a) The data structure you would use to manage screen instances
- (b) How the setter-before-show contract would still be enforced with lazy construction
- (c) What new failure modes you would introduce that do not exist in the eager-construction approach
- (d) Under what conditions lazy construction is worth the additional complexity

**Rubric — a strong response will:**
- Propose a concrete data structure (not vague)
- Correctly identify the setter-before-show enforcement challenge unique to lazy construction
- Name a specific new failure mode and how to prevent it
- Make a justified trade-off decision with reasoning

---

## Full Answer Key (Tiers 1–3)

### Tier 1 Answers

**1.** The setter-before-show contract requires that all data a screen needs must be set on the screen object before calling `layout.show(...)` to display it. Violating it causes a `NullPointerException` because the screen's display code (often in a listener or `paintComponent`) tries to call methods on a reference field that has never been assigned — it is still `null`.

**2. False.** Each screen creating its own copy defeats the purpose of reference passing and introduces data inconsistency. If the search screen finds a `Book` and the detail screen creates a different copy, changes made on the detail screen will not be reflected elsewhere. The correct design is to pass the same object reference to each screen that needs it.

**3.** A flow table is a design artifact that documents every screen-to-screen transition in an application. Its four columns are: (1) trigger (the user action), (2) object (the data involved), (3) state change (what must happen to that object before the transition), and (4) screen owner (which screen is responsible for that state). The "state change" column is important because it makes the setter-before-show contract explicit — it forces the designer to specify *what* must be done before `layout.show(...)` is called.

**4.** `layout.show(container, "checkout")` tells the `CardLayout` manager to make the component registered under the name `"checkout"` visible inside `container`, hiding all other components. Before this call executes, the checkout screen must have had its data set via its setter methods; otherwise the screen will display with `null` fields.

**5. False.** Separation of concerns is not a matter of class size. Mixing navigation logic (deciding which screen comes next) with domain logic (calculating or recording a checkout) makes both harder to test and maintain independently. A checkout method should not need to know anything about which screen the user sees next.

---

### Tier 2 Answers

**6.**
- (a) The `PatientSearch` screen should call a setter method on the `AppointmentDetails` screen, such as `appointmentDetailsScreen.setPatient(foundPatient)`, passing the reference to the found `Patient` object.
- (b) `appointmentDetailsScreen.setPatient(patient)` must be called before `layout.show(container, "appointmentDetails")`.
- (c) If the screen is shown before the patient is set, any code in the screen that reads the patient reference — such as populating name labels in a display-refresh method called on show — will throw a `NullPointerException` because the reference is still `null`.

**7.**
- **Problem 1: Premature display.** `layout.show(container, "confirmation")` is called before `confirmationScreen.setResult("Done")`. The confirmation screen is visible before its data is set. Fix: move `confirmationScreen.setResult("Done")` to before the `layout.show(...)` call.
- **Problem 2: Mixed concerns.** The button listener constructs a `Patron` object, performs a catalog lookup, executes the checkout transaction, drives navigation, and sets the result label — all in one lambda. Navigation logic and domain logic are tightly coupled. Fix: extract `checkout(book, patron)` to a service or controller class, and restrict the listener to calling the service and then triggering navigation.

**8.**

| Trigger | Object | State Change | Screen Owner |
|---|---|---|---|
| User selects a course | `Course` | Selected course reference set on `GradeEntry` screen | `CourseList` sets it before showing `GradeEntry` |
| User enters grade and clicks Submit | `GradeRecord` | New `GradeRecord` constructed with course + grade; set on `Submission` screen | `GradeEntry` sets it before showing `Submission` |

**9.**
- **Strongest point:** The AI correctly identified that data needs to travel between screens and provided a concrete, runnable example rather than an abstract answer.
- **Design problem:** Static variables introduce global mutable state. Any class in the application can read or overwrite `Main.currentBook` at any time, making it impossible to reason about which screen set the value or when. This causes subtle bugs when the user opens multiple flows or when refactoring moves classes.
- **Correction:** The proper approach is to pass object references explicitly between screens using setter methods. When the search screen selects a book, it calls `detailScreen.setBook(selectedBook)` before calling `layout.show(container, "detail")`. This keeps state local to the objects that need it, makes the data flow readable in code, and eliminates hidden dependencies on global fields.

**10.**
- **Lost reference:** The search screen may have stored the book in a local variable, then passed the wrong reference (or no reference) to the detail screen. Diagnose by setting a breakpoint on the setter call in the search screen and inspecting whether the book reference is non-null at that point.
- **Premature display:** The detail screen may have been shown before `setBook(...)` was called. Diagnose by checking the order of statements in the transition code: does `layout.show(...)` appear before or after the setter call?

---

### Tier 3 Answers

**11.**
In Ch 2, a shared reference bug occurs when two variables accidentally point to the same object and one modifies it unexpectedly — the sharing was unintended. In Ch 3, intentional reference passing works by *deliberately* giving two objects (two screens) a reference to the same data object, so they both see the same state without copying. The mechanism is identical: one reference, multiple holders. The difference is intent and ownership. The design principle that prevents accidental sharing while enabling intentional sharing is *screen ownership of state*: exactly one screen (or one controller object) is responsible for creating and setting the data object; other screens only read it through the reference they were given. This makes the flow explicit and auditable.

**12.**
The object model from Ch 1 says behavior belongs with the state it needs. Navigation behavior (deciding which screen comes next) requires knowing the current application state — which flow is in progress, what data has been collected — not the internal UI state of a single screen. A screen object owns only its own UI widgets; it does not own application flow state. Therefore navigation logic should live in the main application class or a dedicated navigator object, not in the screen. The separation of concerns principle from Ch 3 reinforces this: screens are responsible for displaying and collecting data; the navigator is responsible for sequencing screens. A screen that also drives navigation conflates two responsibilities, making it impossible to reuse the screen in a different flow or test the navigation logic independently.

---

## Instructor Notes

- **Exercise 7** is the highest-value error analysis item. The premature-display error is subtle because the code is almost correct; students who spot only the mixed-concerns problem have missed the primary failure mode. Award partial credit accordingly.
- **Exercise 9 (AI Interaction)** works best as a written response, not discussion. Students who accept the static-variable answer uncritically have not internalized the reference-passing model from Ch 3. Look for whether their correction uses setter vocabulary.
- **Exercise 11 (Synthesis)** surfaces whether students understand that reference semantics are neutral — not inherently a bug or a feature. Students who say "shared references are always bad" have missed the point of Ch 2.
- **Exercise 13 (Challenge)** has no single correct answer. Evaluate on the quality of reasoning about trade-offs, not on any specific data structure choice. Common strong answers mention a `HashMap<String, JPanel>` with null-check logic; common weak answers propose the same eager construction renamed.
- Recommended sequence for in-class use: assign Tier 1 as pre-class reading check, Tier 2 in pairs during lab, Tier 3 as written individual homework, Tier 4 as optional extension for students ahead of pace.
