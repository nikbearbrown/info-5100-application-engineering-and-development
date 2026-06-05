# Worked Exercises: Event-Driven Programming

*Chapter 9 of INFO 5100 Application Engineering and Development*

> These exercises follow a research-backed sequence: full worked example → matched practice → completion problem → error-recognition → transfer → interleaved review. Each section builds on the previous. Do not skip ahead.

This chapter establishes event-driven programming: the inversion where the framework calls your code when an event occurs, rather than your code controlling the sequence. The three-part structure is always the same — an **event source** (a UI control that can fire, such as a `Button` or `TextField`), an **event** (the object carrying information about what happened, such as an `ActionEvent` or a `KeyEvent`), and a **handler** (the code you register in advance to respond). Registration connects a handler to a source with calls like `setOnAction`. The chapter's worked domain is the library semester project: a catalog of `Book` objects, a checkout button, a status label, and keyboard interaction using `KeyEvent` and `KeyCode` constants.

---

## Prerequisites

- You can write a Java class and call methods on objects (`button.setOnAction(...)`, `label.setText(...)`).
- You understand that a `Book` object in the library project exposes domain state through methods like `getTitle()` and `isAvailable()`.
- You can read a lambda expression `event -> { ... }` as "when this event fires, run this body."

---

## Part A — Full Worked Example: Registering a Handler That Responds to a Checkout Click

**What this demonstrates:** How to register a single handler on an event source so the framework calls your code when the `ActionEvent` fires, reading the event's source and updating the view.

**The problem:** In the library catalog window there is a `Button checkoutButton` and a `Label statusLabel`. When the user clicks the button, the status label must read `"Checkout requested."`. Write the registration so the framework runs your code on the click, and nothing runs before the click.

```java
Button checkoutButton = new Button("Check Out");
Label statusLabel = new Label("Ready.");
// We must make a click on checkoutButton update statusLabel.
```

**The solution:**

**Step 1 — Identify the event source and the event class.**
The source is `checkoutButton`. A button click produces an `ActionEvent`. The handler we register must be an `EventHandler<ActionEvent>`.
*Why:* Every event-driven interaction has three parts — source, event, handler. Naming the source and the event class first tells you which registration method (`setOnAction`) and which event type the handler receives. The button "does not know what will happen when it fires; it just fires."
*Check:* `setOnAction` accepts an `EventHandler<ActionEvent>`. The event class matches. Good.

**Step 2 — Register the handler in advance, do not call it yourself.**
```java
checkoutButton.setOnAction(event -> {
    statusLabel.setText("Checkout requested.");
});
```
*Why:* Event-driven programs invert control. "You do not call the handler. The framework calls it for you, when the event occurs." Registration happens once, at build time; execution happens later, on the click.
*Check:* The lambda is never invoked in our own code. We never write `handler.handle(...)`. We only register it. Correct.

**Step 3 — Confirm the handler reads from the event/source, not from a copy.**
The label update is a view action triggered by the source that fired. If we needed to know which control fired, `event.getSource()` would return `checkoutButton`.
*Why:* The **event** object carries "which source fired, when, and what the user did." Reading state from the event keeps the handler honest about what actually happened, instead of assuming.
*Check:* `event.getSource() == checkoutButton` would be `true` here. The handler responds to the real source.

**Step 4 — Trace one click end to end.**

| moment | what happens | who acts |
| --- | --- | --- |
| build time | `setOnAction(...)` stores the handler on the button | your code |
| user clicks | framework creates an `ActionEvent` | framework |
| dispatch | framework finds the registered handler and calls `handle(event)` | framework |
| handler body | `statusLabel.setText("Checkout requested.")` runs | your code |

*Why:* Tracing the chain proves the inversion: your registration runs once; the framework drives the rest. If the label never changes, you check whether the handler was actually registered on this source.
*Check:* Before any click, the label reads `"Ready."`. After one click, it reads `"Checkout requested."`.

**Final answer:**
```java
checkoutButton.setOnAction(event -> statusLabel.setText("Checkout requested."));
```

**What made this work:** The central concept is **registration**: connecting a handler to an event source so the framework calls it when the event fires. The naive approach is to write the label-update code in `main` in sequence — but in an event-driven program there is no point in `main` where "the user has clicked" is true. The flow is in the user's control. Only a registered handler runs at the right moment. Sequential code would set the label once at startup and never again.

**Self-explanation prompt:** In your own words, why does `setOnAction` take a handler *object* (a lambda) instead of you simply writing the label update on the next line after constructing the button?

---

## Part B — Matched Practice Problem: Responding to a Key Press with KeyCode

**Same structure, different surface.** In the catalog window there is a `TextField searchField` and a `Label statusLabel`. When the user presses the **Enter** key inside the search field, the status label must read `"Searching..."`. Key presses fire a `KeyEvent`, registered with `setOnKeyPressed`, and you compare against a `KeyCode` constant.

Work the same four steps:
1. Identify the event source and the event class (which `KeyEvent` registration method? which `KeyCode` constant for Enter?).
2. Register the handler in advance on `searchField`.
3. Read the key from the event (`event.getCode()`) and act only when it equals `KeyCode.ENTER`.
4. Trace one Enter keystroke end to end in a table.

**Stuck?** A `KeyEvent` handler runs for *every* key, so the first line of your handler body must filter: act only when `event.getCode() == KeyCode.ENTER`.

*Instructor note: No solution is provided for Part B. Produce the registration, the filter, and the trace table yourself, then verify against the four-step structure in Part A.*

---

## Part C — Completion Problem: A Single Handler Wired to Two Controls

Goal: when the user clicks `clearButton`, both `searchField` is emptied and `statusLabel` reads `"Cleared."`.

**Step 1 — Identify the source and event (complete).**
The source is `clearButton`; a click fires an `ActionEvent`; the handler is an `EventHandler<ActionEvent>`.
*Why:* Source + event + handler is the fixed three-part structure of every event-driven interaction.

**Step 2 — Register the handler in advance (complete).**
```java
clearButton.setOnAction(event -> {
    // body to complete
});
```
*Why:* Registration stores the handler so the framework calls it on the click; we never call it ourselves.

**Step 3 — [BLANK] Update the first view control.**
*Your work here:*
_______________________________________________
*Why (your explanation):*
_______________________________________________

**Step 4 — [BLANK] Update the second view control.**
*Your work here:*
_______________________________________________
*Why (your explanation):*
_______________________________________________

**Step 5 — Verify the trace (complete).**
After one click on `clearButton`: the framework creates an `ActionEvent`, finds the registered handler, and runs the body. Both `searchField.getText()` returns `""` and `statusLabel.getText()` returns `"Cleared."`.

**Final answer:**
```java
clearButton.setOnAction(event -> {
    searchField.setText("");
    statusLabel.setText("Cleared.");
});
```

**Self-explanation prompt:** One handler updated two controls. Why is it fine for a single handler to touch multiple view controls, but a problem for it to also contain the *business* decision of what "clear" means to the model?

---

## Part D — Error-Recognition Problem

> **Use this section only after completing Parts A–C.**

Goal: the catalog window has a `Button refreshButton`. Clicking it should re-read the catalog and set `statusLabel` to `"Catalog refreshed."`. Refreshing the catalog reads tens of thousands of `Book` records from disk and re-sorts them.

**Step 1 — Identify the source and event (correct).**
Source is `refreshButton`; a click fires an `ActionEvent`.

**Step 2 — Register the handler in advance (correct).**
```java
refreshButton.setOnAction(event -> handleRefresh(event));
```

**Step 3 — ⚠ Do the full reload inside the handler body.**
```java
private void handleRefresh(ActionEvent event) {
    List<Book> books = catalog.reloadFromDisk();   // reads 80,000 records, re-sorts
    rebuildEntireTable(books);                       // long, blocking work
    statusLabel.setText("Catalog refreshed.");
}
```

**Step 4 — Confirm the label updates (correct).**
After the handler returns, `statusLabel` reads `"Catalog refreshed."`, and the table shows the reloaded books.

**Your tasks:**
1. **Identify and explain the error.** Step 3 runs long, blocking work directly in the handler body. The handler is called by the framework on its UI/event thread, so while `reloadFromDisk()` and `rebuildEntireTable()` run, the framework cannot dispatch any other event. The window freezes — clicks, scrolls, and key presses are ignored until the handler returns.
2. **Write the corrected Step 3.** Keep the handler as a fast translator. Move the long work off the event thread and hop back to update the view when done:
```java
private void handleRefresh(ActionEvent event) {
    statusLabel.setText("Refreshing...");
    Task<List<Book>> task = new Task<>() {
        protected List<Book> call() { return catalog.reloadFromDisk(); }
    };
    task.setOnSucceeded(e -> {        // runs back on the UI thread
        rebuildEntireTable(task.getValue());
        statusLabel.setText("Catalog refreshed.");
    });
    new Thread(task).start();
}
```
3. **Name the principle violated.** The handler is the *translator*, not the worker — it should register/dispatch quickly and never block the thread the framework uses to deliver events. Long work belongs off the event thread; view updates happen back on it.
4. **Write a test that catches this class of error.** Trigger the handler, then immediately fire a second event (e.g., a click on another button) and assert it is handled within a small time bound. A frozen UI thread fails this because the second event is not dispatched until the reload finishes.

**Why this error is common:** The handler already has access to everything it needs, so the fastest path is to do the work right there — and the freeze is invisible in a demo with fifty books but appears the moment the catalog is large.

---

## Part E — Transfer Problem: A Thermostat Control Panel

A home thermostat has a physical `upButton` and a `currentTempLabel`. Each press of `upButton` should raise the setpoint by one degree and display the new setpoint. The setpoint must accumulate across presses (press three times from 68 → it shows 71). There is no chapter "thermostat" example; the principle is identical to registering a handler on an event source and updating a view from the fired event.

Design it: name the source, the event, the registration, and where the setpoint value lives so that successive presses accumulate rather than resetting.

**Hint (use only if stuck after 10 minutes):** A handler registered with a lambda runs fresh on each press; the *setpoint* cannot live as a local variable inside the handler body, or it resets every time. It must persist outside the handler (a field) so each firing reads and updates the same state.

**Reflection prompt:**
1. Where did you store the setpoint, and why could it not live inside the handler body?
2. What is the thermostat's "event source," "event," and "handler," and how does each map onto the library's `checkoutButton` example?

---

## Part F — Interleaved Review

**Problem F1.** A `Button` named `helpButton` should display `"Help is on the way."` in `statusLabel` when clicked. Write the registration call, then state which line creates the `ActionEvent` and who runs it.
*Chapter this draws from: Chapter 9 (Event-Driven Programming).*

**Problem F2.** The library catalog is a `List<Book>`. Write a `Comparator<Book>` named `byTitle` that sorts books alphabetically by title, then the single line that sorts `List<Book> books` with it. Explain why a named `Comparator` object is preferable to a tangle of inline string comparisons.
*Chapter this draws from: Chapter 9's collections-and-Comparator material (Comparator, Comparable, streams).*

**Problem F3.** A search bar must show, on each keystroke, the count of catalog books whose title starts with what the user has typed. Is the core difficulty here a *filtering* problem (reducing a collection by a predicate) or an *event-driven* problem (responding to a key press)? Defend your answer, then explain how a correct solution needs both.
*Note to instructor: intentionally ambiguous — it sits on the seam between event handling (the keystroke that triggers the work) and stream filtering (the predicate that selects matching books). A strong answer separates the trigger from the computation.*

**Closing reflection:** Across F1–F3, which problems were about *when* code runs (events) versus *what* the code computes (collections)? Naming that split is the chapter's central organizing idea.

---

## Instructor Notes

**Common errors to watch for:**
- Doing long or blocking work inside a handler body, freezing the UI thread (Part D).
- Registering the same handler twice (e.g., re-running setup code), so one click fires the action twice — watch for duplicate registration in initialization paths.
- Forgetting that a `KeyEvent` handler fires for every key, omitting the `event.getCode() == KeyCode.ENTER` filter and acting on the wrong keystroke.

**Signs a student needs to return to the chapter:**
- The student calls the handler method directly in `main` instead of registering it — they have not internalized control inversion.
- The student cannot name the event source and event class for a given interaction.

**Scaffolding adjustments:** If a student struggles in Part A, have them physically annotate which lines run at *build time* versus *click time* before writing any code. If a student finishes Part F quickly, ask them to add a second event source (a keyboard shortcut) that reuses the *same* delegated method without duplicating handler logic.

**Domain adaptation note:** Swap the library `checkoutButton`/`Book` catalog for an inventory "reorder" button over a `Product` list or a scheduling "book slot" button over an `Appointment` list; the source/event/handler structure is unchanged.
