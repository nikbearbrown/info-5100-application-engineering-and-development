# Worked Exercises: Objects and Classes

*Chapter 3 of INFO 5100 Application Engineering and Development*

> These exercises follow a research-backed sequence: full worked example → matched practice → completion problem → error-recognition → transfer → interleaved review. Each section builds on the previous. Do not skip ahead.

---

## Prerequisites

- You understand that a **user flow is a path through the state space**, not a sequence of screens: the screens are how the user sees and changes state, but the *state* — the objects, their fields, their relationships — exists independently of what is displayed.
- You know the **CardLayout** mechanics: a `CardLayout` holds multiple `JPanel`s in a container and shows exactly one at a time; hidden panels "are dormant, not dead" — they remain in memory with their objects' values intact; navigation is a `layout.show(container, "name")` call, and the **setter-before-show contract** requires `panel.setBook(...)` to run *before* `layout.show(...)`.
- You understand **separation of concerns**: visibility belongs to `CardLayout`, display belongs to the panels, and state belongs to the domain objects — three responsibilities deliberately kept in distinct layers so a change in one does not force a change in another.

---

## Part A — Full Worked Example

**What this demonstrates:** Why the same `Book` *reference* — not a copy, not a fresh instance — must travel through a flow, and why the setter-before-show order is a contract: violating either produces the chapter's two signature failures (Lost Reference and Premature Display).

**The problem:** In the library flow, the user selects "Dune" on the result panel and proceeds to checkout. The checkout panel must display the selected book and later mark it checked out, and the confirmation panel must show that the book is now checked out. Here is a navigation handler. Decide whether it correctly carries the object through the flow.
```java
// inside ResultPanel's "Select" handler
Book selectedBook = getSelectedBookFromList();
layout.show(container, "checkout");          // show first
checkoutPanel.setBook(new Book(selectedBook.getTitle()));  // then "set" a fresh Book
```

**The solution:**

**Step 1 — Frame the flow as a state path, not a screen swap**
Ask the chapter's questions: which object travels (a `Book`), who owns it, what each screen reads and writes. The result panel produces a selected `Book`; checkout reads it and later writes its checked-out state; confirmation reads that state.
*Why:* "A user flow is not a sequence of screens. It is a path through the state space." Thinking in screens is exactly the mistake that produces edge-case failures.
*Check:* You can write one row per step naming the object and its read/write role. If you can only name panels, you are still thinking in screens.

**Step 2 — Test the setter-before-show contract on the given order**
The handler calls `layout.show(container, "checkout")` *before* `checkoutPanel.setBook(...)`. That is backwards.
*Why:* "If you show the panel first, the panel's display methods may run before the object is set — and you get the failure from the opening: the right screen, the wrong state." Set state first, then show.
*Check:* This is **Premature Display**: the checkout panel may read a null/unset book on becoming visible, throwing `NullPointerException` or showing empty fields.

**Step 3 — Test reference identity: is the SAME Book traveling?**
The handler passes `new Book(selectedBook.getTitle())` — a brand-new object built from the title string — instead of `selectedBook` itself.
*Why:* "Java passes object references, not object values." Passing a `new` instance means the checkout panel holds a *different* `Book` than the one selected. Any update checkout makes (marking it checked out) lands on this throwaway object, invisible to anything holding the real one.
*Check:* This is the **Lost Reference** failure: "they look identical … because they were both built from the same database row. But they are different objects." Confirmation will show the pre-checkout state.

**Step 4 — Rewrite to honor both: same reference, set before show**
```java
Book selectedBook = getSelectedBookFromList();
checkoutPanel.setBook(selectedBook);   // SET the real reference first
layout.show(container, "checkout");     // THEN show
```
*Why:* This passes the same `Book` reference forward (so mutations persist to every screen holding it) and obeys the setter-before-show contract (so the panel never displays before its state is set). The reference carries forward; no re-query is needed.
*Check:* Trace the reference, not the visual output: confirm `setBook` runs before `show`, and confirm the argument is `selectedBook`, not a `new Book(...)`.

**Final answer:** The original handler has two defects. Corrected:
```java
Book selectedBook = getSelectedBookFromList();
checkoutPanel.setBook(selectedBook);   // same reference, set first
layout.show(container, "checkout");     // show second
```
Evidence of correctness is a reference trace: the *same* `Book` object selected on the result panel is the object checkout mutates and the object confirmation reads — verified by identity, not by the title looking right on screen.

**What made this work:** The central concepts are **reference identity across a flow** and the **setter-before-show contract**. A naive approach swaps panels and rebuilds the `Book` on each screen from the same database row; it compiles, runs, and demos fine forward-once, but it fails the actual requirement — that a loan modification made in checkout persists to confirmation — because each screen holds a *different* object. The fix is not more code; it is passing one reference and ordering two lines correctly.

**Self-explanation prompt:** Close the page and write one sentence: what principle did Step 3 rely on, and when would passing a copy instead of the reference *not* cause a bug (i.e., under what read-only condition would a fresh `Book` per screen be harmless)?

---

## Part B — Matched Practice Problem

**Same structure, different surface.** In the library flow, after checkout the user confirms a loan. The checkout panel's confirm handler must create a `Loan`, attach the *same* `Book` reference to it, and pass the `Loan` to the confirmation panel — in the correct order. A teammate writes:
```java
// inside CheckoutPanel's "Confirm" handler
layout.show(container, "confirmation");
Loan newLoan = new Loan();
newLoan.setBook(new Book(this.book.getTitle()));
newLoan.setBorrower(currentBorrower);
confirmationPanel.setLoan(newLoan);
```
Apply the same analysis: check the setter-before-show contract, check reference identity (is the *same* `Book` attached to the `Loan`?), name which of the two common failures each defect is, and write the corrected handler. Produce a reference trace as your evidence.

**Stuck?** Return to Part A and map each step to your obstacle — especially Step 2 (ordering) and Step 3 (the `new Book(...)` that breaks reference identity).

*Instructor note: No worked solution provided for Part B — the point is production, not verification.*

---

## Part C — Completion Problem

**What's missing:** Steps 3 and 4 are removed.

**The problem:** Design and partially trace a two-screen flow: ResultPanel → CheckoutPanel, where the user selects a `Book` and the checkout screen later marks it unavailable. Decide which object travels, who may modify it, and whether the implementation is correct.

**Step 1 — Build the flow table (state path) (complete)**

| screen | user action | object involved | field(s) read | field(s) written |
| --- | --- | --- | --- | --- |
| ResultPanel | select a book | `Book` | title, author | (none) |
| CheckoutPanel | confirm checkout | `Book` | title, author | `available` |

*Why:* The chapter's phase gate: "write the flow in a table … screen, user action, object involved, state change" before any code. The table is the spec.

**Step 2 — Assign ownership (complete)**
ResultPanel owns nothing — it produces a selected `Book`. CheckoutPanel is the *only* screen permitted to write `available`. Both read the same `Book` reference.
*Why:* "Decide explicitly which screen owns each piece of state and which screens only read it." Explicit roles make bugs visible instead of requiring every panel's code to be read at once.

**Step 3 — [BLANK] Write the two navigation lines (setter and show) in the correct order, passing the SAME reference**
*Your work here:*
_______________________________________________
_______________________________________________
*Why (your explanation):*
_______________________________________________

**Step 4 — [BLANK] State the evidence (a reference trace) that proves the correct object — not a copy — traveled**
*Your work here:*
_______________________________________________
_______________________________________________
*Why (your explanation):*
_______________________________________________

**Step 5 — Verify by tracing the reference, not the output (complete)**
After implementing, trace the `Book` reference from selection through checkout: confirm the same object (not a copy) is passed, and confirm `setBook` runs before `show`. "That trace is the evidence the lab asks for. Not 'it ran.' Not 'it compiled.' The trace."
*Why:* The two common failures (Lost Reference, Premature Display) are both caught by this single reference-trace practice.

**Final answer:** Correct navigation:
```java
checkoutPanel.setBook(selectedBook);   // same reference, set first
layout.show(container, "checkout");
```
Evidence: a reference trace showing the `Book` selected on ResultPanel is identical (same object) to the `Book` CheckoutPanel reads and writes, with the setter called before the show.

**Self-explanation prompt:** Compare your Steps 3–4 to Part A's Steps 3–4. Part A diagnosed a broken handler; here you wrote a correct one. What single property of your two lines guarantees you avoided *both* Lost Reference and Premature Display at once?

---

## Part D — Error-Recognition Problem

> **Use this section only after completing Parts A–C.**

**What's wrong:** one error, marked ⚠.

**The problem:** A teammate wants every panel to reach "the current book" without passing references through setters, so they store it in a shared static field on a utility class.

**Step 1 — (correct) Identify what travels through the flow**
The object that must be consistent across ResultPanel, CheckoutPanel, and ConfirmationPanel is a single `Book`.
*Why correct:* Names the traveling object, the first question of the chapter's flow design.

**Step 2 — (correct) Recognize that copies break the flow**
If each panel held its own copy, an update in checkout would be invisible to confirmation; the panels must see the *same* book.
*Why correct:* Matches the chapter's reason for passing references, not copies.

**Step 3 ⚠ — Share the book via a global static field**
```java
public class Selection {
    public static Book currentBook;   // every panel reads/writes this
}
// any panel:
Selection.currentBook = selectedBook;
// elsewhere:
display(Selection.currentBook);
```
Now every panel reaches the same `Book` through one global static field, "so every panel can access the current selection without passing references."
*Why it looks fine:* It does keep one shared `Book`, the demo runs forward correctly, and it removes the need for setter calls — which feels like a simplification.

**Step 4 — (correct, and that is what makes it dangerous) Observe a passing forward-once demo**
The student runs the flow once, sees the same book on every screen, and concludes the shared static field works.
*Why this is a trap:* It works in the happy path while silently destroying separation of concerns: now *any* screen can modify the current book at *any* time, so a backward navigation or a second concurrent flow corrupts state, and "tracing the failure requires reading every panel's code simultaneously."

**Your tasks:**
1. **Identify and explain the error.** Step 3 replaces explicit state ownership with a global mutable static field. That collapses the state layer into a shared global, violating separation of concerns: visibility (CardLayout), display (panels), and state (domain objects) are no longer separable, and no screen "owns" the book.
2. **Write the corrected Step 3.** Keep the reference travelling through setters under the setter-before-show contract, with one owner per field:
```java
checkoutPanel.setBook(selectedBook);
layout.show(container, "checkout");
```
3. **Name the principle violated.** Separation of concerns / explicit state ownership — "decide explicitly which screen owns each piece of state." A global static makes every screen a potential writer, which the chapter forbids by design constraint even though Java allows it.
4. **Describe a test to catch this class of error.** Add a backward navigation (Checkout → Result → re-select a different book) or run the flow twice; assert each confirmation shows *its own* flow's book. The static-field version leaks the prior/last selection across navigations and fails; the setter-passed reference does not.

**Why this error is common:** A global static field "optimizes" for not having to pass references and passes a forward-once demo, so the design-level cost — destroyed separation of concerns and unowned, any-screen-writable state — stays invisible until a backward navigation or second flow corrupts the shared object.

---

## Part E — Transfer Problem

**Same principle, new context.** Leave the library. You are building a checkout *wizard* for an e-commerce app with three screens: Cart → Shipping → Review. A single `Order` object is assembled across the screens — the Cart screen creates it with the items, the Shipping screen adds the address, and the Review screen displays the full order and must not change anything. Using only this chapter's concepts (state path, the traveling object, setter-before-show, ownership rules, and the staging-object idea where an object is "partially constructed … and progressively completed"), specify: which screen creates the `Order`, which fields each screen is permitted to set, what the object's state looks like at the end of each transition, and why the Review screen must be read-only. You do not need to write the Swing code — produce the ownership specification.

**Hint (use only if stuck after 10 minutes):** This is the chapter's staging-object pattern from the scheduling domain, where an `Appointment` "starts partially constructed and gains fields at each step." The key constraint is identical: the engineer decides which screen may set which field, and the final read-only screen must write nothing — "if the confirmation screen is allowed to write … a display bug becomes a data corruption bug."

**Reflection prompt:** (1) Which chapter concept did you apply, and how did you recognize the `Order` was a staging object rather than a fully-formed traveling object like the library `Book`? (2) What was structurally different about the e-commerce flow versus the library flow — and what stayed identical about the ownership reasoning?

---

## Part F — Interleaved Review

**Mixed problem set.** Decide which concept applies before solving — that selection is the point.

**Problem F1:** Draw the *state path* (not the screen sequence) for a two-screen library flow, naming for each step the object involved and the fields it reads versus writes. Then write the two navigation lines in the correct order and explain in one sentence why the order is a contract, not a preference. *Chapter this draws from: Chapter 3 (Objects and Classes).*

**Problem F2:** A teammate's checkout panel builds a `new Book` by reading the title string off a label on the result panel, then re-queries the database for a matching record. The confirmation panel shows the right title, yet a checkout update made in the checkout panel does not appear on confirmation. Using only the *reference-versus-object* model — copies versus shared references on the heap — explain why this fails. *Chapter this draws from: Chapter 2 (Methods, Arrays, and File Objects) — references vs. copies.*

**Problem F3:** A confirmation screen displays empty fields on first navigation. It *looks* like a Premature Display ordering bug (this chapter's setter-before-show contract), but it could instead be that the panel is reading from a `Book` that was never the traveling reference at all (a Lost Reference / reference-identity issue rooted in the prior chapter). Decide which you will investigate first, justify it, and name the single trace that would distinguish the two causes. *Note to instructor: intentionally ambiguous; commit to an approach, then reflect.*

**After F1–F3:** State which concept you reached for first in each — especially F3, where two failures share a surface symptom (empty fields) but one is an ordering-contract violation (this chapter) and the other is a reference-identity violation (prior chapter), and only a reference trace tells them apart.

---

## Instructor Notes

**Common errors to watch for:**
- Students rebuild a `new Book` on each screen from the same database row, producing the Lost Reference failure that passes a forward-once demo but fails when an update must persist across screens.
- Students call `layout.show(...)` before the destination panel's setter, producing Premature Display (NullPointerException or empty fields) on navigation.
- Students reach for a shared static field to avoid passing references (Part D), trading away separation of concerns and explicit state ownership.

**Signs a student needs to return to the chapter:**
- They describe their flow only as a screen sequence and cannot produce the four-column flow table (screen, user action, object involved, state change).
- Their verification evidence is "it ran / it compiled / the title looked right" rather than a *reference trace* proving the same object — not a copy — traveled.

**Scaffolding adjustments:** *For students who struggle with Part A:* give them the corrected two lines and ask only "which line sets state and which shows the panel, and what breaks if you swap them?" — isolate the setter-before-show contract before adding reference identity. *For students who finish Part F quickly:* have them attempt the chapter's Challenge — design the three-screen staging-object flow (Patient → Provider → Time Slot) for the scheduling domain, specifying which screen creates the `Appointment`, which fields each may set, the state at each transition, and what happens if the user skips the middle screen.

**Domain adaptation note:** The traveling-object discipline is identical across domains — a `Book`, an inventory `Item`, or a staged `Appointment` all require the same answers to "what travels, who owns it, what may each step change?" — only the object name and whether it arrives fully formed or is staged across screens changes.
