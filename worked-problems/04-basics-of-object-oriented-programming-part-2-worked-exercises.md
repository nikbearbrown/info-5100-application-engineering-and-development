# Worked Exercises: Basics of Object-Oriented Programming Part 2

*Chapter 4 of INFO 5100 Application Engineering and Development*

> These exercises follow a research-backed sequence: full worked example → matched practice → completion problem → error-recognition → transfer → interleaved review. Each section builds on the previous. Do not skip ahead.

---

## Prerequisites

- You can write and run a Java class with fields, a constructor, and methods, and you understand that an object variable holds a *reference* to an object, not the object itself.
- You can set a breakpoint in the NetBeans debugger, pause execution, and read the variables panel; you know the difference between **step over** and **step into**.
- You can articulate the chapter's central distinction: a **symptom** is the observable wrong output, a **proximate cause** is the immediate line that produced it, and a **root cause** is the design or state error upstream that made the proximate cause possible.

---

## Part A — Full Worked Example

**What this demonstrates:** Moving from symptom to root cause on a sequence-dependent bug by forming a falsifiable **hypothesis**, using a **breakpoint** to **isolate** evidence, and confirming the root cause rather than patching the output.

**The problem:** The library checkout program assigns each checked-out book to a patron. When a patron checks out a single book, the output is correct. When two checkouts happen in succession, the second book is attached to the *first* patron's name. The program compiles, runs, and throws no exception. Here is the relevant code:

```java
public class Checkout {
    private String currentPatron;   // set before each checkout

    public void checkout(String patronName, Book book) {
        if (currentPatron == null) {
            currentPatron = patronName;
        }
        book.setBorrower(currentPatron);
        System.out.println(book.getTitle() + " -> " + book.getBorrower());
    }
}
```

Driver:

```java
Checkout desk = new Checkout();
desk.checkout("Alice", new Book("Effective Java"));
desk.checkout("Bob",   new Book("Clean Code"));
```

Observed output:

```
Effective Java -> Alice
Clean Code -> Alice      <-- should be Bob
```

**The solution:**

**Step 1 — Classify the symptom and refuse to patch it.** Name what you observe without changing code: the second line shows `Clean Code -> Alice` when it should show `Bob`. The first checkout is correct; only the second is wrong.
*Why:* This is the chapter's foundational move — distinguish the **symptom** (wrong output on the second checkout) from the cause. "Something is off with the checkout" is a restatement of the symptom, not a **hypothesis**.
*Check:* You have a concrete, sequence-dependent fact: correct on the first call, wrong on the second. That asymmetry is a hypothesis generator.

**Step 2 — Form a falsifiable hypothesis naming object, field, and moment.** Write: "At the start of the second `checkout`, the field `currentPatron` still holds `\"Alice\"` instead of being reset, so the second book is assigned the stale reference."
*Why:* A hypothesis must name *which field, in which object, at which point in execution* holds a wrong value. This claim is checkable — it can be confirmed or refuted, which is what makes it useful.
*Check:* The hypothesis points at exactly one location (`currentPatron` at entry to the second `checkout`) and predicts one value (`"Alice"`).

**Step 3 — Isolate with a breakpoint at the line the hypothesis names.** Set a breakpoint on the first line inside `checkout` (the `if (currentPatron == null)` test). Run the program. Let the first checkout complete; when execution pauses at the *second* call, inspect `currentPatron` in the variables panel.
*Why:* **Isolation** creates conditions under which the hypothesis can be confirmed or refuted. The breakpoint shows *actual* intermediate state, not what the code claims should happen.
*Check:* Trace the value of `currentPatron` at the breakpoint across both calls:

| Call | `patronName` arg | `currentPatron` at breakpoint | `if (== null)` taken? | `book.getBorrower()` after |
| --- | --- | --- | --- | --- |
| 1 (Alice) | "Alice" | null | yes → set to "Alice" | Alice (correct) |
| 2 (Bob) | "Bob" | "Alice" | no → stays "Alice" | Alice (WRONG) |

**Step 4 — Move from proximate cause to root cause.** The proximate cause is `book.setBorrower(currentPatron)` running with `currentPatron == "Alice"`. Step back: why did `currentPatron` hold `"Alice"` on entry to call 2? Because the only assignment is guarded by `if (currentPatron == null)`, which is false after the first checkout. The field is never reset, and the guard prevents reassignment.
*Why:* The proximate cause is closer to the bug but still not the **root cause**. The root cause is the *design decision* — making `currentPatron` a persistent field with a one-time, null-guarded assignment — that made the stale reference possible.
*Check:* Predict: if the root cause is the guard, removing it should fix call 2. Confirm before editing by reasoning, not by trial-and-error patching.

**Step 5 — Fix the root cause and verify state, not just output.** Replace the null-guarded assignment with an unconditional one (or pass the patron straight through without a field):

```java
public void checkout(String patronName, Book book) {
    currentPatron = patronName;       // always reset, no guard
    book.setBorrower(currentPatron);
    System.out.println(book.getTitle() + " -> " + book.getBorrower());
}
```

Re-run with the breakpoint still set. Confirm `currentPatron == "Bob"` at entry-after-assignment on call 2.
*Why:* The chapter's verification standard: confirm the state is now correct *at the point where it was wrong*, not merely that the symptom disappeared.

**Final answer:** Root cause — the `if (currentPatron == null)` guard makes the assignment a one-time event, so `currentPatron` retains its stale first-checkout value on every subsequent call. Fix — assign `currentPatron = patronName` unconditionally. Verified output:

```
Effective Java -> Alice
Clean Code -> Bob
```

**What made this work:** The central concept is **reading code as a causal system** — every method modifies state, and a bug is a place where actual state diverges from expected state. We named the divergence (`currentPatron` stale at call 2), isolated it with a breakpoint, and traced upstream from proximate cause (`setBorrower` with the wrong reference) to root cause (the null guard). The naive approach — changing the method-call order or "fixing" the print line until `Bob` appeared — fails because it patches the symptom without identifying *why* the state was wrong, leaving the stale-field design intact to resurface on a different call sequence.

**Self-explanation prompt:** In your own words, why does committing to a hypothesis *before* opening the debugger produce a better diagnosis than stepping through the program looking for anything suspicious?

---

## Part B — Matched Practice Problem

**The problem:** An inventory program decrements stock when an item is sold. Selling one item works. Selling two items in quick succession decrements the *first* item's stock twice and never touches the second item. No exception is thrown. The code:

```java
public class Register {
    private Product currentProduct;

    public void sell(Product p, int qty) {
        if (currentProduct == null) {
            currentProduct = p;
        }
        currentProduct.reduceStock(qty);
        System.out.println(currentProduct.getName() + " stock: " + currentProduct.getStock());
    }
}
```

Driver: `reg.sell(milk, 1); reg.sell(bread, 1);`

Produce: (1) the symptom classification, (2) a falsifiable hypothesis naming the object, field, and moment, (3) the breakpoint location and a trace table of `currentProduct` across both calls, (4) the proximate-vs-root-cause distinction, and (5) the corrected method plus the state you would verify at the breakpoint.

**Stuck?** Compare the asymmetry — correct on the first call, wrong on the second — to the library checkout. Ask which field is supposed to change between calls but does not, and what guards its assignment.

*Instructor note: No solution is provided for Part B. Work it fully before moving on; the matched structure to Part A is intentional.*

---

## Part C — Completion Problem

**The problem:** A scheduling program assigns each appointment to a provider. The first booking gets the right provider. On the second booking in the same session, the appointment is assigned to the first provider, who is already booked. No exception. Code:

```java
public class Scheduler {
    private Provider currentProvider;

    public void book(Provider prov, Appointment appt) {
        if (currentProvider == null) {
            currentProvider = prov;
        }
        appt.assignTo(currentProvider);
        System.out.println(appt.getId() + " -> " + appt.getProvider());
    }
}
```

Driver: `s.book(drLee, a1); s.book(drPark, a2);`

**Step 1 — Classify the symptom.** Booking `a1` correctly shows `drLee`; booking `a2` shows `drLee` when it should show `drPark`. Correct on the first call, wrong on the second.
*Why:* Separating the observable wrong output from its cause is the precondition for a hypothesis; the sequence-dependence is the clue.

**Step 2 — Form the hypothesis.** "At entry to the second `book` call, the field `currentProvider` still holds the `drLee` reference instead of being updated to `drPark`."
*Why:* The hypothesis names the object (`Scheduler` instance), the field (`currentProvider`), and the moment (entry to the second call) — making it falsifiable.

**Step 3 — [BLANK] Isolate with a breakpoint and trace the field.**
*Your work here:* ________________________________________________
(Name the exact line for the breakpoint, then fill the trace table below.)

| Call | `prov` arg | `currentProvider` at breakpoint | `if (== null)` taken? | `appt.getProvider()` after |
| --- | --- | --- | --- | --- |
| 1 (drLee) | | | | |
| 2 (drPark) | | | | |

*Why (your explanation):* ________________________________________________

**Step 4 — [BLANK] Move from proximate cause to root cause.**
*Your work here:* ________________________________________________
(Name the proximate cause line, then the root-cause design decision upstream.)

*Why (your explanation):* ________________________________________________

**Step 5 — Fix the root cause and verify state.** Replace the null-guarded assignment with `currentProvider = prov;` (unconditional). Re-run with the breakpoint and confirm `currentProvider == drPark` at entry-after-assignment on call 2.
*Why:* The fix addresses the design decision that made the stale reference possible; verification confirms the field is correct at the point it was previously wrong.

**Final answer:** Root cause — the `if (currentProvider == null)` guard makes assignment a one-time event, so `currentProvider` keeps its stale first-booking value. Fix — assign unconditionally. Verified output: `a1 -> drLee` and `a2 -> drPark`.

**Self-explanation prompt:** Explain why the *proximate* cause (`appt.assignTo(currentProvider)`) is a misleading place to apply the fix, even though it is the line where the wrong value enters the appointment.

---

## Part D — Error-Recognition Problem

> **Use this section only after completing Parts A–C.**

A student is diagnosing the library checkout bug from Part A. Their write-up:

**Step 1 (correct).** Symptom: second checkout shows `Clean Code -> Alice` instead of `Bob`. First checkout correct.

**Step 2 (correct).** Hypothesis: at entry to the second `checkout`, `currentPatron` holds the stale value `"Alice"`.

**Step 3 ⚠.** "Breakpoint set inside `checkout`. The variables panel shows `currentPatron == \"Alice\"` on call 2. So the bug is that `book` and the second `Book` object share the *same* `borrower` reference — both `Book` objects point to one shared `currentPatron` String, and modifying it for one modifies it for both. The fix is to give each `Book` its own copy of the patron name with `new String(currentPatron)`."

**Step 4 (correct-looking).** Student applies `book.setBorrower(new String(currentPatron))`. Re-runs. Output is still `Clean Code -> Alice` (a plausible-looking partial result — no exception, "shared reference" reasoning sounds sophisticated, and the change compiles).

**Your tasks:**

1. **Identify and explain the error in Step 3.** The student misread the evidence. The breakpoint *confirmed* `currentPatron == "Alice"` — that is the stale-field problem from Part A, not a shared-reference-across-Books problem. The two `Book` objects do not share a `borrower`; each `setBorrower` call stores whatever value `currentPatron` held *at that moment*. The defect is that `currentPatron` was never reset, not that the String is aliased between books.

2. **Write the corrected Step 3.** "The breakpoint confirms `currentPatron == \"Alice\"` at entry to call 2. The hypothesis is confirmed: the field holds a stale reference. The next question is upstream — why was `currentPatron` not updated to `\"Bob\"`? Inspect the `if (currentPatron == null)` guard: it is false on call 2, so the assignment is skipped."

3. **State the principle violated.** The chapter's rule that the diagnostic act is *reading what the tool shows against your hypothesis*. The student let the tool's output trigger a new, fancier theory (shared mutable reference) instead of confirming the hypothesis they already held. They moved from proximate evidence to a speculative root cause without tracing upstream.

4. **Design a test to catch this class of error.** Add a third checkout with a distinct patron (`desk.checkout("Carol", new Book("X"))`) *after* clearing the suspected shared-reference theory: if the "shared String" theory were true, fixing it should change call 2; since output is unchanged, the theory is refuted. More directly: set a breakpoint and watch whether `currentPatron` is *reassigned* between calls — if it never is, the root cause is the missing reset, conclusively.

**Why this error is common:** "Shared mutable reference" is a real and serious bug class in Java, so it is an attractive explanation — but here it is pattern-matched onto evidence that actually points at a much simpler stale-field-never-reset cause.

---

## Part E — Transfer Problem

**The problem (different domain — a vending-machine controller, not in this chapter):** A vending machine tracks the currently selected slot. The first purchase dispenses the right snack. The second purchase, in the same power cycle, dispenses the *first* snack again instead of the newly selected one. No crash.

```java
public class Vendor {
    private Slot selectedSlot;
    public void purchase(Slot s) {
        if (selectedSlot == null) {
            selectedSlot = s;
        }
        selectedSlot.dispense();
        System.out.println("Dispensed from " + selectedSlot.getCode());
    }
}
```

Apply the full hypothesize–isolate–test loop: classify the symptom, write a hypothesis naming the field and moment, name the breakpoint and predict the trace, identify proximate vs. root cause, and give the fix. Confirm the root cause is the same *class* of error as the library bug even though the domain is different.

**Hint (use only if stuck after 10 minutes):** The bug class is "a field that should be updated every call is updated only when null." Ask: what is the one field that is supposed to change between purchases, and what condition gates its assignment?

**Reflection prompt:** (1) What made it possible to transfer the library diagnosis to a vending machine with almost no new reasoning? (2) If you had only the wrong *output* and not the code, what single observation about the *sequence* of failures would still let you form the same hypothesis?

---

## Part F — Interleaved Review

**Problem F1.** Given the library checkout method, a teammate proposes "fixing" the second-checkout bug by reordering the driver so Bob checks out before Alice. Explain why this masks rather than fixes the root cause, and describe the breakpoint observation that would prove the field-reset defect still exists.
*Chapter this draws from: Chapter 4 (Basics of Object-Oriented Programming Part 2 — symptom vs. root cause; hypothesize, isolate, test).*

**Problem F2.** In a `Catalog` that holds `Book` objects in an array with a `count` field, `searchByTitle` returns an oversized array trimmed to `found` results. A `Book` references an `Author` entity shared across multiple books. Explain why storing a shared `Author` reference (rather than copying the author's name into each `Book`) lets you update a biography in one place — and why this is *supply-side modeling*, not a debugging concern.
*Chapter this draws from: Chapter 5 (Inheritance and Polymorphism — entity, relationship, transaction; the catalog as a first-class object).*

**Problem F3 (discrimination).** A program loads books into a `Catalog` at startup, then the first checkout works but the second attaches the wrong patron. A student says "this is a supply-side modeling problem — the catalog isn't a first-class object." Decide whether the defect is a supply-side modeling failure (Chapter 5) or a stale-field causal-diagnosis problem (Chapter 4), and justify which chapter's method you would apply first.
*Note to instructor: intentionally ambiguous — the preloaded catalog is correct supply-side modeling, so the surface cue ("catalog") points at Chapter 5, but the actual defect is a stale `currentPatron` field requiring Chapter 4's hypothesize-isolate-test. Students must resist the surface match.*

**After F1–F3:** Write two sentences on how you decided which chapter each problem belonged to, and what surface feature in F3 was designed to mislead you.

---

## Instructor Notes

**Common errors to watch for:**
- Writing a hypothesis that is actually a symptom restatement ("the checkout is broken") rather than naming a field, object, and moment.
- Stopping at the proximate cause (`setBorrower`/`assignTo` with the wrong value) and editing that line, leaving the stale-field root cause intact.
- Reading the variables panel and inventing a more sophisticated theory (shared mutable reference, aliasing) instead of confirming the hypothesis already held — the Part D failure mode.

**Signs a student needs to return to the chapter:**
- They change code before stating any hypothesis, or change multiple lines at once until the symptom disappears.
- They cannot distinguish, on a concrete example, which observation is the symptom, which is the proximate cause, and which is the root cause.

**Scaffolding adjustments:** If a student struggles with Part A, have them fill only the trace table first (Step 3) with the program paused — reading actual state against their prediction usually unlocks the hypothesis. If a student finishes Part F quickly, have them introduce a *new* sequence-dependent bug of their own (per Exercise 4 in the chapter) and write the full debugging session for a peer to solve blind.

**Domain adaptation note:** Swap the library checkout for the student's semester-project domain (inventory decrement, scheduling double-booking) — the stale-field-never-reset bug class and the hypothesize-isolate-test loop are identical; only the class, field, and method names change.
