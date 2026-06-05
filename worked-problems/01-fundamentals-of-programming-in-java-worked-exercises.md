# Worked Exercises: Fundamentals of Programming in Java

*Chapter 1 of INFO 5100 Application Engineering and Development*

> These exercises follow a research-backed sequence: full worked example → matched practice → completion problem → error-recognition → transfer → interleaved review. Each section builds on the previous. Do not skip ahead.

---

## Prerequisites

- You can read code as a **business model**, not as syntax: a `Book` class is a *claim about what a book is* in the library's world (it has a title, an availability state, and can transition between available and checked-out), and the `checkOut()` method is a *business process*, not just a Java construct.
- You understand the chapter's core distinction — **state** (the data an object holds about itself) versus **behavior** (the operations an object can perform) — and the central principle that *state and behavior belong together* so a rule like "no more than three books" can live in exactly one place.
- You can distinguish the **three kinds of wrong**: a *compilation error* (Java rejects grammatically illegal code before running), a *runtime error* (legal code that fails during execution, e.g. `NullPointerException`), and *silent wrong behavior* (the program runs, produces output, and the output is incorrect with no exception and no red text).

---

## Part A — Full Worked Example

**What this demonstrates:** That the most dangerous of the three kinds of wrong — silent wrong behavior — is invisible to the compiler and must be caught by reading code *against the requirement*, because compilation checks form while the requirement checks meaning.

**The problem:** In the library checkout program, a patron borrows a book. The intended business behavior is: the borrowed book becomes unavailable *and* the book is recorded in that patron's borrowed list. Here is a checkout method that compiles cleanly and produces output. Read it against the requirement and decide whether it is correct.

```java
public void checkOut(Book book, Patron patron) {
    book.setAvailable(false);
    // record the loan
    patron.getBorrowedBooks().add(book);
}
```
Now consider this variant a teammate committed, which also compiles and runs:
```java
public void checkOut(Book book, Patron patron) {
    book.setAvailable(false);
    // record the loan
    // (line that adds the book to the patron's list was deleted)
}
```

**The solution:**

**Step 1 — Recover the requirement before reading the code**
Write the business behavior in plain terms first: after checkout, (1) the book is unavailable, and (2) the patron's borrowed list contains the book.
*Why:* The chapter's skill is "reading code as a business model" — you must hold *what the business needs* in your head before you can judge whether the code provides it. AI cannot do this step for you; it does not know your requirement.
*Check:* You have two concrete, checkable conditions, not a vague sense of "checkout works."

**Step 2 — Classify the failure mode of the variant before running it**
The variant marks the book unavailable but never adds it to the patron's list. It has no missing semicolon and calls no method on `null`, so it is neither a compilation error nor a `NullPointerException`. Predict: this is **silent wrong behavior**.
*Why:* Compilation checks form; the variant is grammatically legal, so Java accepts it. The requirement checks meaning, and condition (2) is unmet. "The distance between them is where most real bugs live."
*Check:* If your classification depends on the program crashing, re-read — silent wrong behavior produces no exception and no red text.

**Step 3 — Trace the state to expose the divergence**
Trace one checkout call against both conditions:

| condition (requirement) | correct version | teammate's variant |
| --- | --- | --- |
| book is unavailable | true | true |
| patron's list contains the book | true | **false** |

*Why:* This is the chapter's verification loop — change/read the code, predict the effect on state, compare to the requirement. The book's availability matches; the patron's record does not. The right book is touched, but the loan is not recorded under the patron.
*Check:* Run the program and print both `book.isAvailable()` and `patron.getBorrowedBooks().contains(book)`. The first prints `false` (correct); the second prints `false` (wrong) in the variant.

**Step 4 — Name the evidence that would prove correctness**
"It compiled" and "it ran" are not evidence. The evidence is a trace or test asserting *both* conditions after checkout: the book is unavailable AND the patron's list contains exactly that book.
*Why:* The module's standard is reading code against a requirement and verifying that what runs is what was specified. Only the engineer's judgment closes the gap between "looks right" and "is correct."
*Check:* Your evidence must fail on the variant and pass on the correct version. If a test passes on both, it is not testing condition (2).

**Final answer:** The variant is **silently wrong**. Expected output for the correct version after `checkOut(book, patron)`:
```
book.isAvailable()                       -> false
patron.getBorrowedBooks().contains(book) -> true
```
The variant prints `false` for the second line — the book is unavailable but attached to no patron's record. No exception fires; the bug is visible only by reading the code against the two-part requirement.

**What made this work:** The central concept is **the three kinds of wrong**, and specifically that silent wrong behavior cannot be caught by the compiler. A naive approach — "it compiles and the output looks right on the first test" — fails because compilation checks form, not meaning, and a single happy-path glance never exercises condition (2). Only recovering the requirement first and tracing state against it surfaces the divergence.

**Self-explanation prompt:** Close the page and write one sentence: what principle did Step 2 rely on when it ruled out compilation error and runtime error, and when would that classification be wrong (i.e., what small change to the variant would turn the silent bug into a `NullPointerException` instead)?

---

## Part B — Matched Practice Problem

**Same structure, different surface.** In the library program, the business requirement for *return* is: returning a book makes it available again AND removes it from the patron's borrowed list. A teammate writes a `returnBook` method that compiles and runs:
```java
public void returnBook(Book book, Patron patron) {
    patron.getBorrowedBooks().remove(book);
    // mark the book available
    book.setAvailable(true);
    book.setAvailable(false);   // teammate added this "just to reset"
}
```
Recover the two-part requirement, classify the failure mode (compilation error, runtime error, or silent wrong behavior) *before* running, trace the state against both conditions, and state the evidence that would prove the method correct. Produce a Final answer with expected output.

**Stuck?** Return to Part A and map each step to your obstacle — especially Step 2, where the failure mode was classified by checking whether the code was grammatically legal and whether anything was called on `null`, before any trace.

*Instructor note: No worked solution provided for Part B — the point is production, not verification.*

---

## Part C — Completion Problem

**What's missing:** Steps 3 and 4 are removed.

**The problem:** The library requires that a patron may not hold more than three books. A teammate's `borrow` method compiles and runs and works fine in a quick demo where a patron borrows two books. Decide whether it satisfies the requirement.
```java
public void borrow(Book book) {
    // intended: refuse if the patron already holds 3 books
    this.borrowedBooks.add(book);
    book.setAvailable(false);
}
```

**Step 1 — Recover the requirement (complete)**
The business rule: a patron with three books already checked out must be refused a fourth; the book stays available and the list stays at three.
*Why:* The chapter places this rule "inside the patron" precisely because state (the borrowed list) and behavior (the borrow decision) belong together. The requirement, not the code, defines correctness.

**Step 2 — Classify how this could be wrong (complete)**
The method has no syntax error and calls nothing on `null` in the demo, so it is not a compilation or runtime error. The risk is **silent wrong behavior**: it always adds, even on the fourth book.
*Why:* Compilation checks form; the rule is about meaning. A two-book demo never exercises the limit, so "looks right on the first test" hides the divergence.

**Step 3 — [BLANK] Trace the state for a patron borrowing a FOURTH book and show the divergence**
*Your work here:*
_______________________________________________
_______________________________________________
*Why (your explanation):*
_______________________________________________

**Step 4 — [BLANK] State the evidence (a specific test) that would prove correctness, and what output the buggy version produces on it**
*Your work here:*
_______________________________________________
_______________________________________________
*Why (your explanation):*
_______________________________________________

**Step 5 — Locate the rule in exactly one place (complete)**
The fix adds a guard at the top of `borrow` so the limit lives inside the `Patron`:
```java
public void borrow(Book book) {
    if (this.borrowedBooks.size() >= 3) {
        return; // refuse: limit reached
    }
    this.borrowedBooks.add(book);
    book.setAvailable(false);
}
```
*Why:* This is the chapter's payoff — because state and behavior belong together, the "no more than three" rule can live in exactly one place, inside the patron, rather than being draped across the program.

**Final answer:** The original method is silently wrong: it adds a fourth book without refusal. A test that borrows four books and asserts `borrowedBooks.size() == 3` fails on the original (it returns 4) and passes on the guarded version.

**Self-explanation prompt:** Compare your Steps 3–4 to Part A's Steps 3–4. In Part A the missing condition was "book added to list"; here it is "limit enforced." What is the same about *how* you exposed each — and why did a happy-path demo hide both?

---

## Part D — Error-Recognition Problem

> **Use this section only after completing Parts A–C.**

**What's wrong:** one error, marked ⚠.

**The problem:** A method checks whether a returned book is the specific copy a patron has on record before removing it. The patron's record stores the book's title for the matching step.
```java
public void returnIfHeld(String returnedTitle, Patron patron) {
    String heldTitle = patron.getHeldTitle();
    // ... decide whether this is the patron's book ...
}
```

**Step 1 — (correct) Recover the requirement**
The book should be removed from the patron's record only if the returned title matches the title the patron actually holds.
*Why correct:* States the business condition before reading code, as the chapter requires.

**Step 2 — (correct) Identify the comparison this needs**
Two `String` values — `returnedTitle` and `heldTitle` — must be compared for *equal content* (same characters), since a returned title and a stored title are separate String objects built at different times.
*Why correct:* The business meaning is content equality of two strings, not identity of one.

**Step 3 ⚠ — Compare the two Strings**
```java
if (returnedTitle == heldTitle) {
    patron.getBorrowedBooks().removeIf(b -> b.getTitle() == heldTitle);
}
```
The student uses `==` to compare the title strings.
*Why it looks fine:* In quick tests it may even print the right result — when both strings come from the same string literal, Java may intern them so `==` happens to be `true`, producing a plausible-looking pass.

**Step 4 — (correct, and that is what makes it dangerous) Observe a passing demo**
The student runs a demo where the returned title was typed as the same literal used to populate the record, sees the book correctly removed, and concludes the method is right.
*Why this is a trap:* The demo's success is an accident of string interning. With a title read from a file or built from user input, `==` compares object identity, returns `false`, and the book is silently *not* removed — silent wrong behavior, no exception.

**Your tasks:**
1. **Identify and explain the error.** Step 3 compares `String` content with `==`, which tests reference identity (whether the two variables point at the same object), not whether they contain the same characters. This is the classic Java misconception of comparing Strings with `==` instead of `.equals()`.
2. **Write the corrected Step 3.**
```java
if (returnedTitle.equals(heldTitle)) {
    patron.getBorrowedBooks().removeIf(b -> b.getTitle().equals(heldTitle));
}
```
3. **Name the principle violated.** Content equality of objects must use `.equals()`; `==` tests reference identity. Conflating the two produces silent wrong behavior — the third and most dangerous kind of wrong.
4. **Describe a test to catch this class of error.** Run the method with a `returnedTitle` that is built at runtime (e.g., read from input or concatenated) rather than written as the same literal, so the two strings are distinct objects with identical content. Assert the book is removed. The `==` version fails this test; the `.equals()` version passes.

**Why this error is common:** `==` compiles and frequently appears to work because Java interns identical string literals, so the bug hides behind plausible-looking output until the strings come from different sources — exactly the silent wrong behavior the chapter warns is invisible without reading code against the requirement.

---

## Part E — Transfer Problem

**Same principle, new context.** Leave the library entirely. A grade-tracking program stores each student's letter grade. The requirement: a student is on the honor roll only if their recorded grade equals `"A"`. A method takes a grade the registrar typed in and decides honor-roll status, then also must decide between a *compilation*, *runtime*, or *silent* failure if the grade field for a brand-new student was never set. Without writing the full program, (1) describe how you would compare the typed grade to `"A"` correctly and why a naive comparison could be silently wrong, and (2) classify what happens if the unset grade field is `null` and the code calls a method on it — which of the three kinds of wrong is that, and how would you detect it?

**Hint (use only if stuck after 10 minutes):** The chapter's three-kinds-of-wrong framework is domain-independent. One of your two sub-questions is about content-vs-reference comparison; the other is about calling behavior on something that holds nothing. Name each by its kind before solving.

**Reflection prompt:** (1) Which chapter concept did you apply, and how did you recognize it applied even though grades are not books? (2) What was different about the grade domain compared to the library domain — and what stayed identical about the *reasoning*?

---

## Part F — Interleaved Review

**Mixed problem set.** Decide which concept applies before solving — that selection is the point.

**Problem F1:** A teammate argues: "If the checkout program compiles and the output looks right on the first test, the implementation is correct." Give one specific scenario from the library domain where this reasoning fails, name which of the three kinds of wrong it is, and state the minimum evidence you would require before accepting the implementation as correct. *Chapter this draws from: Chapter 1 (Fundamentals of Programming in Java).*

**Problem F2:** Your `checkOut` method throws `error: package does not exist` when you run the project, before any of your checkout logic executes. Decide which *layer* of the diagnostic model this lives in, and explain why this is not a problem with your checkout code at all. *Chapter this draws from: Chapter 0 (Welcome) — the three-layer diagnostic model.*

**Problem F3:** The `Patron` class enforces the three-book limit inside its `borrow()` method. A teammate proposes moving that check to a `Library` class instead, "so the library decides what patrons may do." This *looks* like a pure design-style debate, but it is really about where state and behavior belong (this chapter) — and it can be confused with a question about how many objects the system manages (the next module). Argue both sides, then commit: where should the limit live, and what is the deciding factor? *Note to instructor: intentionally ambiguous; commit to an approach, then reflect.*

**After F1–F3:** State which concept you reached for first in each — especially F3, where the "where does behavior live?" principle (state and behavior belong together) is the right reach, not a collections question that belongs to a later module.

---

## Instructor Notes

**Common errors to watch for:**
- Students accept "it compiles and printed the right thing once" as correctness, missing silent wrong behavior because their single test only exercises the happy path (Parts A, C, F1).
- Students compare `String` content with `==` and are fooled by string interning into thinking it works (Part D) — surface this with runtime-built strings.
- Students ask AI to *write* new checkout code rather than restricting AI to *explaining* code and errors they already have, skipping the requirement-understanding the module teaches.

**Signs a student needs to return to the chapter:**
- They cannot state, for a given bug, which of the three kinds of wrong it is, or they assume every bug eventually throws an exception.
- They describe what a method *does in Java* but cannot say what *business behavior* it implements or what evidence would prove it correct.

**Scaffolding adjustments:** *For students who struggle with Part A:* give them the two-condition requirement written out and have them only fill the trace table, deferring the failure-mode vocabulary until the divergence is visible. *For students who finish Part F quickly:* have them attempt the chapter's design exercise — write the argument for enforcing the three-book limit in `Patron` versus `Library`, then carry it forward as the bridge question into managing many objects.

**Domain adaptation note:** Swapping the library for inventory or healthcare scheduling changes the object names and rules but not the three-kinds-of-wrong reasoning or the requirement-first verification loop — the deep structure is identical across all three paths.
