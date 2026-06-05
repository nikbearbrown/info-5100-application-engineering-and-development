# Worked Exercises: Fundamental Themes
*Chapter 97 of INFO 5100 Application Engineering and Development*

> These exercises follow a research-backed sequence: full worked example → matched practice → completion problem → error-recognition → transfer → interleaved review. Each section builds on the previous. Do not skip ahead.

*Bridge chapter — Parts D, E, and F omitted.*

## Prerequisites
- You can name the seven themes — *you cannot verify what you do not understand*, *objects model responsibilities*, *debugging is causal reasoning*, *AI use requires phase gates*, *the project is one system*, *tests are evidence not magic*, *the final defense is the point* — and recognize them as habits of mind, not rules.
- You can connect a theme to a concrete artifact in the library semester project (`Book`, `Patron`, `Catalog`, `CheckoutTransaction`).
- You hold the Feynman test: being able to say "here is what I still do not fully understand," with specificity, is the mark of real understanding.

---

## Part A — Full Worked Example: Applying "Objects Model Responsibilities" to a misplaced display method

**What this demonstrates:** How the *objects model responsibilities* theme — and its "must nots" — diagnoses and fixes a class that absorbed a responsibility it should never hold.

**The problem:** A student's `Book` class compiles, runs, and displays correctly in the JavaFX demo. But `Book` contains this:

```java
public class Book {
    private String title;
    private boolean available;
    public Label renderTitleLabel() {
        Label label = new Label(title);
        label.setTextFill(available ? Color.GREEN : Color.RED);
        return label;   // Book builds a JavaFX Label
    }
}
```

Apply the theme to decide whether this design is sound and, if not, to relocate the responsibility correctly.

**The solution:**

**Step 1 — Ask the theme's central question: whose responsibility is this?** The method builds a JavaFX `Label` and chooses a display color. The question is not "where is it convenient?" but "what object owns this knowledge and behavior?"
*Why:* The theme states a class is "a statement about what one kind of thing knows, what one kind of thing can do, and what one kind of thing must never be asked to do." Color and `Label` construction are *view* knowledge; a `Book` is a supply-side entity that models the world, not the screen.
*Check:* Recall the theme's own example: "A `Book` knows its title and availability... It must not know about the GUI." `renderTitleLabel()` violates that "must not" exactly.

**Step 2 — Name the specific degradation this "must not" violation causes.** Because `Book` now depends on JavaFX (`Label`, `Color`), it cannot be used in a headless context, and it cannot be unit-tested without a JavaFX toolkit running.
*Why:* The theme: "A `Book` that knows what color to display its title in cannot be used in a headless context." The responsibility that should live in the view is now "locked inside an object that will have to be modified every time those external concerns change."
*Check:* Try to write a plain `@Test` that constructs a `Book` and checks `isAvailable()` — it now risks dragging in JavaFX initialization. That difficulty is the symptom.

**Step 3 — Relocate the responsibility to the layer that owns it.** Keep state and domain behavior in `Book`; move rendering to the view/handler.
```java
public class Book {
    private String title;
    private boolean available;
    public String getTitle() { return title; }
    public boolean isAvailable() { return available; }   // Book knows; Book does not render
}

// in the view/handler layer:
Label label = new Label(book.getTitle());
label.setTextFill(book.isAvailable() ? Color.GREEN : Color.RED);
```
*Why:* The view now reads model state (`getTitle()`, `isAvailable()`) and decides presentation; `Book` no longer knows about the GUI. Each layer has "a defined responsibility, a defined boundary."
*Check:* `Book` no longer imports any JavaFX type; a unit test can construct it and assert `isAvailable()` with no toolkit.

**Step 4 — Confirm the fix against "the project is one system."** This is not a local cleanup; a `Book` free of view dependencies wires up cleanly in persistence (Module 8) and GUI (Module 10) because good design compounds.
*Why:* The themes interlock: respecting the responsibility boundary now prevents the compounding degradation the *one system* theme describes — where a Module-2 shortcut surfaces as pain in Modules 4, 8, and 10.
*Check:* You can state one future module that this fix makes easier (e.g., headless persistence tests), which is evidence the boundary, not just the demo, improved.

**Final answer:** `Book.renderTitleLabel()` violates the responsibility boundary by giving a domain entity view knowledge; relocate rendering to the view layer so `Book` only knows its state and domain behavior, which also makes it testable and lets the design compound cleanly across modules.

**What made this work:** The central theme is *objects model responsibilities*, whose "must nots" are as load-bearing as its "cans." The naive approach — "it displays correctly, so the design is fine" — fails because a working demo is "local evidence" while the misplaced responsibility "travels through every subsequent module"; the demo cannot reveal that the entity is now untestable and view-coupled.

**Self-explanation prompt:** In your own words, why is "it works in the demo" the wrong test for whether a responsibility lives in the right class, and what is the right test?

---

## Part B — Matched Practice Problem: Applying "Debugging Is Causal Reasoning" to an out-of-sync list

**What this demonstrates:** Replacing change-and-rerun guessing with a falsifiable hypothesis that names an object, a field, a moment, and a mechanism.

**The problem:** After a patron returns a book, the GUI still shows the book in the patron's borrowed list, but the catalog correctly shows it as available. A classmate has been changing lines near the return handler and rerunning, with no progress. Using the *debugging is causal reasoning* theme, produce a disciplined diagnosis.

Produce a worked solution with the same deep structure as Part A:

**Step 1 — State why change-and-rerun is not debugging.** (Use the theme's claim that it is "search with worse odds than a coin flip," driven by the same wrong mental model that produced the bug.)
**Step 2 — Form one falsifiable hypothesis.** (It must name an object, a field, a moment in execution, and a mechanism — e.g., something about whether `Patron.borrowedBooks` holds `Book` references or title strings, and whether `return` updates the same object the catalog updated.)
**Step 3 — State the inspection that would confirm or refute it.** (What breakpoint, on which field, checked when?)
**Step 4 — Distinguish proximate cause from root cause.** (If confirmed, what upstream design decision made this divergence possible? Tie it to the *one system* theme's `Book`-reference-vs-title-string example.)
**Step 5 — State what AI can and cannot contribute here.** (Per the theme: AI can explain errors and suggest categories of root cause; it cannot hold *your* program's causal model.)

**Stuck?** Recall the theme's worked hypothesis form: not "something is wrong with the return" but "the borrowed list and the catalog refer to *different* objects representing the same book, so updating one does not update the other." Make your hypothesis that specific.

> Instructor note: No solution is provided for Part B. Work it fully before moving on.

---

## Part C — Completion Problem: Applying "Tests Are Evidence, Not Magic" to an overconfident claim

**What this demonstrates:** Stating precisely what a passing test does and does not prove, and identifying the regression value tests provide over time.

**The problem:** A teammate has one passing test for `Catalog.searchByTitle` and concludes "search is correct." Using the *tests are evidence, not magic* theme, write the precise account of what their test establishes.

**Step 1 — State the exact claim a passing test makes.** A passing test proves "on this specific setup, with these specific inputs, the method produced output that matched the stated requirement, at the time the test was run."
*Why:* The theme insists this is "a real claim... not a small claim" — it externalizes a previously internal, ephemeral judgment — but it is bounded to the inputs supplied.

**Step 2 — Name the three specific limits the theme lists.** It does not prove all inputs are handled (only the supplied ones); not that behavior survives surrounding-code changes (only at write time); not that behavior is correct in the full system (only in the isolated setup).
*Why:* These limits "are not arguments against testing... they are arguments for thinking carefully about what you are testing and what you are leaving untested."

**Step 3 — [BLANK] Apply the five-case taxonomy to show what the single test leaves uncovered.**
*Your work here:*

*Why (your explanation):*

**Step 4 — [BLANK] State the more durable value of the test suite that the teammate is overlooking.**
*Your work here:*

*Why (your explanation):*

**Step 5 — Write the corrected conclusion the teammate should make.** Replace "search is correct" with a bounded, evidence-honest claim and name what would have to be added to strengthen it.
*Why:* "No finite set of tests can be" a proof that all cases are covered; the honest claim names its scope and its regression value rather than overclaiming correctness.

**Final answer:** One passing test proves search met its requirement only for that one input at write time; it is silent on other inputs, on future code changes, and on full-system behavior — and the suite's more durable value is the regression barrier each prior test creates, not a proof of correctness.

**Self-explanation prompt:** Why is "the tested behaviors are correct" a fundamentally different claim from "the system is correct," and which one did the teammate actually have evidence for?

---

## Instructor Notes

**Common errors:**
- Treating "it works in the demo" as evidence a responsibility lives in the right class, missing that good or bad design compounds across modules (the *one system* theme).
- Debugging by change-and-rerun instead of forming a falsifiable hypothesis that names an object, field, moment, and mechanism.
- Overclaiming from a passing test ("the system is correct") instead of stating the bounded claim a test actually supports.

**Signs a student needs to return:**
- They cannot connect a theme to a concrete artifact in their own project — the theme stays abstract.
- They cannot state "here is what I still do not fully understand" with specificity, defaulting to vague confidence (the Feynman test the defense probes).

**Scaffolding adjustments:** If a student struggles with Part A, give them only the theme's two sentences about what a `Book` "knows" and "must not know" and have them classify each line of the class against them before refactoring. If a student finishes Part C quickly, have them take a second theme (e.g., *AI use requires phase gates*) and write their own three-step worked example connecting it to a specific module's boundary.

**Domain adaptation note:** Substitute inventory or scheduling entities for the library `Book`/`Patron`/`Catalog`; the themes are domain-independent habits of mind, so the responsibility boundaries, causal-reasoning discipline, and evidence-not-magic limits transfer unchanged.
