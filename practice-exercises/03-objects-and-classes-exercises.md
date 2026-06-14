# Module 3 — Objects and Classes: Exercises
**Topic:** Multi-screen flows, CardLayout, state management

---

## Learning Objectives Covered

- Design multi-screen flows with explicit state transitions using flow tables
- Implement CardLayout navigation with correct screen registration and switching
- Trace object references through user flows across multiple screens
- Diagnose lost-reference and premature-display failures

*Every exercise below maps to at least one of these objectives. The `(Tests: ...)` tag on each exercise identifies which one(s).*

---

## Worked Example

*Study this example before attempting Tier 1. After reading it, close it and try to recall the key steps from memory before moving on.*

**Problem:** A library app has two screens: `BookSearch` and `BookDetail`. When a user selects a book, the app should navigate to `BookDetail` and display the book's title and author. A student writes this transition code:

```java
layout.show(container, "detail");
detailScreen.setBook(selectedBook);
```

The detail screen shows null for all fields. What went wrong and how should it be fixed?

**Approach:**
1. **Identify the contract.** The setter-before-show contract says: set all data on the target screen *before* calling `layout.show()`.
2. **Trace the execution order.** Line 1 calls `layout.show(...)` — the detail screen becomes visible. At this moment, `detailScreen.book` is still null (no setter has been called). Any code that runs when the screen appears (like a display-refresh method) reads a null reference.
3. **Line 2** then calls `setBook(selectedBook)` — but the screen is already visible and has already tried to display null data.
4. **Identify the failure mode.** This is a **premature display** failure — the screen was shown before its required data was set.
5. **Fix.** Reverse the two lines:

```java
detailScreen.setBook(selectedBook);
layout.show(container, "detail");
```

**Answer:** The screen was shown before its data was set, causing a null display. The fix is to always set data before showing the screen.

**What to notice:** The lines are almost correct — they're just in the wrong order. Premature display failures are easy to miss because the code looks nearly right. The setter-before-show contract is the rule that catches them.

---

## Tier 1 — Warm-Up

*(Tests: recall, CardLayout, setter-before-show, flow table, separation of concerns)*

**Exercise 1** *(Tests: setter-before-show contract — NullPointerException cause)*

In a multi-screen application, what is the setter-before-show contract? Why does violating it cause a `NullPointerException`?

---

**Exercise 2** *(Tests: reference passing — screen independence is a misconception)*

**True or False:** "Each screen in a CardLayout application should create its own copy of the Book object it needs to display, so screens are independent of each other."

State whether this is true or false. Explain your reasoning in two to three sentences.

---

**Exercise 3** *(Tests: flow table — four columns and purpose)*

What is a flow table? What four columns does it contain, and why is specifying the "state change" column particularly important when designing multi-screen applications?

---

**Exercise 4** *(Tests: premature display vs. lost reference — contrastive classification)*

Classify each of the following as a **premature display** failure, a **lost reference** failure, or **neither**. Write one sentence explaining your classification.

- (a) The detail screen shows null fields because `layout.show()` was called before `setBook()`.
- (b) The confirmation screen shows the previous patron's name because the patron reference was never updated between checkouts.
- (c) A `NullPointerException` is thrown at the line `book.getTitle()` inside the detail screen's display method.
- (d) The search screen successfully finds a book, but it calls `detailScreen.setBook(null)` accidentally.

*(Why this is tempting to get wrong: (a) and (c) both produce null-related errors but have different causes. The question is whether the reference is null because it was never set — premature display — or because it was actively set to null/lost — lost reference.)*

---

**Exercise 5** *(Tests: CardLayout navigation — show() requirements)*

What does the call `layout.show(container, "checkout")` do? What must be true before this call executes for the checkout screen to display correctly?

---

**Exercise 6** *(Tests: separation of concerns — navigation vs. domain logic)*

**True or False:** "Mixing navigation logic (which screen to show) with domain logic (how to process a checkout) inside the same method is acceptable if the class is small enough."

State whether this is true or false. Explain your reasoning in two to three sentences.

---

## Tier 2 — Application

*(Tests: setter-before-show, flow table design, diagnosing failures, AI evaluation)*

**Exercise 7** *(Tests: object travel between screens — setter-before-show)*

A hospital appointment app has three screens: `PatientSearch` → `AppointmentDetails` → `Confirmation`. A patient object is found on the search screen.

Describe:
- (a) How the patient object should travel to the `AppointmentDetails` screen
- (b) What method should be called before showing that screen
- (c) What happens if the screen is shown before the patient is set

---

**Exercise 8 — Error Analysis** *(Tests: premature display + separation of concerns)*

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

**Exercise 9** *(Tests: flow table design — state ownership per transition)*

Design a flow table for a 3-screen student grade submission app with screens: `CourseList` → `GradeEntry` → `Submission`.

For each transition, specify:
- (a) The user action that triggers it
- (b) The object involved
- (c) The state change that must happen
- (d) Which screen "owns" that state

---

**Exercise 10 — AI Interaction** *(Tests: reference passing — static variables vs. setter design)*

First, without consulting AI, write one sentence answering: what is the correct way to pass a `Book` object from one screen to another in a CardLayout application?

Then read this AI response to "How do I pass data between screens in a Java Swing application?":

> "The easiest way is to use static variables. Make your data static and access it from any screen using the class name. For example: `Main.currentBook = selectedBook;`"

- Identify the **strongest point** in the AI's response.
- Identify the **design problem** with using static variables for screen-to-screen data.
- Write a **one-paragraph correction** explaining the proper approach.
- State the **specific failure scenario** you would construct to demonstrate the problem with static variables to a skeptical classmate — describe what sequence of user actions would reveal the bug.

---

**Exercise 11 — Self-Explanation** *(Tests: setter-before-show — why order matters for NullPointerException)*

In this chapter, the setter-before-show contract requires setting data on a screen *before* calling `layout.show()`. Explain in 2–3 sentences why calling `layout.show()` before the setter causes a `NullPointerException` rather than simply displaying empty fields. Your explanation must use the term **"reference"** correctly — specifically, what the reference's value is at the moment the screen appears.

---

**Exercise 12 — Cumulative** *(Tests: reference passing across screens + reference semantics from Ch 2)*

In Ch 2, you learned that `patronB = patronA` copies the reference (the memory address), not the object. In this chapter, the correct way to pass data between screens is to call a setter method that stores the reference.

A library app's `PatientSearch` screen calls `appointmentScreen.setPatient(patient)` and navigates. The next time a different patient is searched, the same `setPatient()` call is made with a new patient.

(a) After the second `setPatient()` call, how many `Patient` objects exist on the heap?
(b) Who holds a reference to the first patient after the second call?
(c) Is the first patient object deleted? What determines when it will be removed from memory?

---

**Exercise 13** *(Tests: lost reference and premature display — diagnosis)*

A student's book detail screen shows `null` for all fields even though the search returned a valid book. The screen itself was written correctly.

Using the two failure modes from this chapter (lost reference and premature display), explain:
- The two most likely causes
- How you would diagnose which one is occurring

---

## Tier 3 — Synthesis

**Exercise 14** *(Connects: Module 3 reference passing + Module 2 reference semantics)*

In Ch 2, shared references allow two variables to point to the same object. In Ch 3, passing an object reference between screens is the correct design.

Explain:
- (a) How the same reference mechanism that caused bugs in Ch 2 is the feature that makes multi-screen data passing work correctly in Ch 3
- (b) What the difference is between a "shared reference bug" and "intentional reference passing"
- (c) What design principle prevents the former while enabling the latter

**What distinguishes a surface answer from a strong one:**
- Distinguishes accidental vs. intentional sharing using specific examples from each chapter
- Names the specific design principle (screen ownership of state, setter-before-show contract)
- Uses reference vocabulary from Ch 2 correctly

*Common error:* Students say "shared references are always bad." The answer must distinguish the mechanism (same in both cases) from the intent (accidental mutation vs. deliberate passing). A strong answer shows that the same property — one object, multiple reference holders — is a bug when unintended and a feature when controlled.

---

**Exercise 15** *(Connects: Module 3 screen design + Module 1 object model)*

The object model from Ch 1 says behavior belongs in the object that owns the relevant state. Apply this to a multi-screen application: which object should own the "navigate to next screen" behavior — the current screen, a separate navigator object, or the main application?

Defend your answer using both the object model principle from Ch 1 and the separation of concerns principle from Ch 3.

**What distinguishes a surface answer from a strong one:**
- Names specific state that each candidate object owns
- Uses object model vocabulary from Ch 1 (state, behavior, ownership)
- Makes a defensible choice with reasoning, not just assertion

*Common error:* Students say "the main application" because "it controls everything" — without using Ch 1 vocabulary to justify which object owns the relevant state. A strong answer identifies that navigation state (which screen is active, what data is in transit) belongs to the application or navigator, not to individual screens, because screens only own their own UI state.

---

## Tier 4 — Challenge

**Exercise 16 — Lazy Screen Construction** *(No answer key — rubric only)*

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

**Worked Example**
*No answer needed — the worked example is its own model.*

---

### Tier 1 Answers

**Exercise 1**
The setter-before-show contract requires that all data a screen needs must be set on the screen object before calling `layout.show(...)` to display it. Violating it causes a `NullPointerException` because the screen's display code tries to call methods on a reference field that has never been assigned — it is still `null`.

*Common error:* Students say "it throws an error because the screen can't find the data." The more precise answer: the screen's reference field was never set, so when the screen tries to call `book.getTitle()`, `book` is null — calling any method on null throws `NullPointerException`.

---

**Exercise 2**
**False.** Each screen creating its own copy defeats the purpose of reference passing and introduces data inconsistency. If the search screen finds a `Book` and the detail screen creates a different copy, changes made on the detail screen will not be reflected elsewhere. The correct design is to pass the same object reference to each screen that needs it.

*Common error:* Students answer True because "screens should be independent." Screens should have independent UI logic, not independent data objects. The data (the Book) is shared by reference; the UI is separate.

---

**Exercise 3**
A flow table is a design artifact that documents every screen-to-screen transition in an application. Its four columns are: (1) trigger (the user action), (2) object (the data involved), (3) state change (what must happen to that object before the transition), and (4) screen owner (which screen is responsible for that state). The "state change" column is important because it makes the setter-before-show contract explicit — it forces the designer to specify *what* must be done before `layout.show(...)` is called.

---

**Exercise 4**
- (a) **Premature display.** The screen was shown before its data was set. The null fields are a direct consequence of the screen being visible before `setBook()` was called.
- (b) **Lost reference.** The patron reference was not updated — the screen holds a stale reference to the previous patron rather than a null. This is a logic error in the transition code, not a timing issue.
- (c) **Neither / premature display consequence.** The `NullPointerException` in the display method is a *symptom* of premature display — it is not a separate failure mode. The root cause is (a).
- (d) **Lost reference.** The book reference was actively set to null rather than being left unset from construction time. `setBook(null)` is an explicit act; premature display is about calling `show()` too early.

*Common error:* Students classify (c) as a separate failure mode. `NullPointerException` is the symptom that both premature display and lost reference can produce. The failure mode is identified by cause, not by exception type.

*Why this is tempting:* (a) and (c) both involve null and both cause null-related errors. The distinction is in the cause: premature display = screen shown too early; (c) is merely what premature display looks like at runtime.

---

**Exercise 5**
`layout.show(container, "checkout")` tells the `CardLayout` manager to make the component registered under the name `"checkout"` visible inside `container`, hiding all other components. Before this call executes, the checkout screen must have had its data set via its setter methods; otherwise the screen will display with `null` fields.

---

**Exercise 6**
**False.** Separation of concerns is not a matter of class size. Mixing navigation logic (deciding which screen comes next) with domain logic (calculating or recording a checkout) makes both harder to test and maintain independently. A checkout method should not need to know anything about which screen the user sees next.

*Common error:* Students say "it's okay for a small class." Size does not change the coupling problem — a small class with mixed concerns is still hard to test and change independently.

---

### Tier 2 Answers

**Exercise 7**
- (a) The `PatientSearch` screen should call a setter method on the `AppointmentDetails` screen, such as `appointmentDetailsScreen.setPatient(foundPatient)`, passing the reference to the found `Patient` object.
- (b) `appointmentDetailsScreen.setPatient(patient)` must be called before `layout.show(container, "appointmentDetails")`.
- (c) If the screen is shown before the patient is set, any code in the screen that reads the patient reference will throw a `NullPointerException` because the reference is still `null`.

---

**Exercise 8**
- **Problem 1: Premature display.** `layout.show(container, "confirmation")` is called before `confirmationScreen.setResult("Done")`. The confirmation screen is visible before its data is set. Fix: move `confirmationScreen.setResult("Done")` to before the `layout.show(...)` call.
- **Problem 2: Mixed concerns.** The button listener constructs a `Patron`, performs a catalog lookup, executes the checkout, drives navigation, and sets the result label — all in one lambda. Fix: extract `checkout(book, patron)` to a service or controller class, and restrict the listener to calling the service and then triggering navigation.

---

**Exercise 9**

| Trigger | Object | State Change | Screen Owner |
|---|---|---|---|
| User selects a course | `Course` | Selected course reference set on `GradeEntry` screen | `CourseList` sets it before showing `GradeEntry` |
| User enters grade and clicks Submit | `GradeRecord` | New `GradeRecord` constructed with course + grade; set on `Submission` screen | `GradeEntry` sets it before showing `Submission` |

---

**Exercise 10**
- **Strongest point:** The AI correctly identified that data needs to travel between screens and provided a concrete, runnable example.
- **Design problem:** Static variables introduce global mutable state. Any class in the application can read or overwrite `Main.currentBook` at any time, making it impossible to reason about which screen set the value or when. This causes subtle bugs when the user opens multiple flows or when refactoring moves classes.
- **Correction:** The proper approach is to pass object references explicitly using setter methods. When the search screen selects a book, it calls `detailScreen.setBook(selectedBook)` before calling `layout.show(container, "detail")`. This keeps state local to the objects that need it and makes the data flow visible in code.
- **Demonstration scenario:** Open the app, search for Book A, begin navigating to the detail screen, then (without completing the flow) trigger a second search for Book B. With static variables, `Main.currentBook` is immediately overwritten to Book B. If the detail screen reads `Main.currentBook` when it becomes visible, it now shows Book B's data — even though the user was in the middle of viewing Book A. This race condition does not exist with setter-based passing because each screen holds its own reference.

---

**Exercise 11**
When `layout.show()` is called, the CardLayout makes the target screen visible and any display-refresh code that runs on show (such as updating labels from the stored reference) executes immediately. At that moment, the screen's **reference** field — the variable that will hold the `Book` — has never been assigned, so its value is `null` (Java's default for uninitialized reference variables). When the display code calls `book.getTitle()`, it is calling a method on a null reference, which the JVM cannot resolve and reports as `NullPointerException`. It does not show "empty fields" because there is no object to read empty values from — there is no object at all.

*Common error:* Students say the screen "can't find the data." The precise cause: the reference variable is null (holds no address), so any method call on it fails immediately. Empty fields would require an object with empty strings; null means no object exists yet.

---

**Exercise 12**
(a) After the second `setPatient()` call, **two** `Patient` objects still exist on the heap — the first patient and the second patient. The setter only changes which object `appointmentScreen.patient` points to; it does not delete the first patient.

(b) After the second call, only the code that originally created the first patient (the search result) might still hold a reference to it — or nobody does, if the search result variable was reassigned. `appointmentScreen.patient` now points to the second patient.

(c) The first patient object is **not deleted** by the setter call. Java's garbage collector removes objects from the heap only when no references point to them. If no variable anywhere holds the first patient's address, it becomes eligible for garbage collection and will eventually be removed. If the search screen still holds a reference to it (e.g., in a local variable or a `lastSearch` field), it remains on the heap.

---

**Exercise 13**
- **Lost reference:** The search screen may have stored the book in a local variable, then passed the wrong reference (or no reference) to the detail screen. Diagnose by setting a breakpoint on the setter call in the search screen and inspecting whether the book reference is non-null at that point.
- **Premature display:** The detail screen may have been shown before `setBook(...)` was called. Diagnose by checking the order of statements in the transition code: does `layout.show(...)` appear before or after the setter call?

---

### Tier 3 Answers

**Exercise 14**
In Ch 2, a shared reference bug occurs when two variables accidentally point to the same object and one modifies it unexpectedly — the sharing was unintended. In Ch 3, intentional reference passing works by *deliberately* giving two objects (two screens) a reference to the same data object, so they both see the same state without copying. The mechanism is identical: one reference, multiple holders. The difference is intent and ownership. The design principle that prevents accidental sharing while enabling intentional sharing is *screen ownership of state*: exactly one screen (or one controller) is responsible for creating and setting the data object; other screens only read it. This makes the flow explicit and auditable.

*Common error:* Students say "shared references are always bad" or "always good." The answer must distinguish the mechanism (same in both chapters) from the intent. Accidental sharing = bug. Deliberate passing with clear ownership = feature.

---

**Exercise 15**
The object model from Ch 1 says behavior belongs with the state it needs. Navigation behavior (deciding which screen comes next) requires knowing the current application state — which flow is in progress, what data has been collected — not the internal UI state of a single screen. A screen object owns only its own UI widgets; it does not own application flow state. Therefore navigation logic should live in the main application class or a dedicated navigator object, not in the screen. The separation of concerns principle from Ch 3 reinforces this: screens are responsible for displaying and collecting data; the navigator is responsible for sequencing screens. A screen that also drives navigation conflates two responsibilities, making it impossible to reuse the screen in a different flow or test the navigation logic independently.

*Common error:* Students say "the main application" as the answer but without using Ch 1 vocabulary. A strong answer explains *why* in terms of state ownership: navigation state belongs to the application because no single screen owns the whole flow.

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

**Worked example note:** The worked example targets the premature display failure — the most common error in this chapter. Ask students after reading it: "What is the one thing you must always do before calling layout.show()?" If they can answer without looking, they have the core contract.

**Exercise 4 (Contrastive Classification):** The key confusion is (a) vs. (c) — students classify (c) as a separate failure mode. Use the clarification: failure modes are identified by cause, not by symptom. `NullPointerException` is a symptom. Premature display is a cause. Multiple causes can produce the same symptom.

**Exercise 8 (Error Analysis):** The premature display error is the primary one — award partial credit if students identify only the mixed-concerns problem. The premature display is the runtime-visible failure; the mixed-concerns is a design flaw that makes the code hard to fix.

**Exercise 10 (AI Interaction):** The verification scenario (part 4) is the highest-value part. Students who can construct a concrete multi-step user scenario that breaks the static-variable design have genuinely understood the problem. Students who say "it will cause bugs" without a scenario have not.

**Exercise 11 (Self-Explanation):** Students must explain *why* null causes NullPointerException, not just that it does. The target explanation: a null reference holds no address, so calling any method on it fails because there is no object to dispatch to.

**Exercise 12 (Cumulative):** This connects Ch 2 reference semantics (assignment copies addresses, garbage collection) to Ch 3 screen design. Part (c) introduces garbage collection implicitly — students often think `setPatient(newPatient)` "deletes" the old patient. It does not.

**Common errors to watch for:**
- Classifying (c) in Exercise 4 as a separate failure mode
- Saying static variables are "fine for small apps" (Exercise 10)
- Saying `setPatient(newPatient)` deletes the old object (Exercise 12)

**DEI note:**
All scenarios use hospital appointment systems, library catalogs, and grade submission apps — domains accessible regardless of cultural background. No socioeconomic assumptions are embedded.
