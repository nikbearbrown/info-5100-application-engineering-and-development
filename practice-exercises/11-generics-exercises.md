# Module 11 — Generics: Event Handlers and Responsibility
## Exercise Set

> **Content note:** Despite the module title "Generics," this chapter's exercises cover **event handlers, lambda expressions, handler decomposition, and the handler responsibility rule**. Generics are not the primary topic here.

**Learning Objectives**
1. Register handlers using lambda, anonymous class, and named inner class forms
2. Decompose handler responsibility into delegated methods
3. Maintain the model-view boundary under extension
4. Trace the full click-to-view-update chain

**Core Concepts:** event/handler/registration triad, handler as translation not implementation, lambda vs. anonymous vs. named inner class, closet handler (too much responsibility), responsibility rule (single reason to change), handler decomposition, model update + view update as separate methods, dependency injection in handlers

---

## Worked Example

*Study this example before attempting Tier 1. After reading it, close it and try to recall the key steps from memory before moving on.*

**Problem:** A student's checkout button handler is 45 lines long. It validates the ISBN, finds the book, checks availability, finds the patron, creates the checkout record, saves to file, clears the form, and shows a confirmation. A reviewer says it violates the handler responsibility rule. Diagnose why and sketch the fix.

**Approach:**
1. **State the handler responsibility rule.** A handler's only job is to translate a user event into a model operation and update the view. It should not contain business logic itself.
2. **Identify what is wrong.** This handler has multiple distinct reasons to change: validation rules could change, the checkout business logic could change, the save format could change, and the confirmation display could change. Each change requires editing the handler.
3. **Apply decomposition.** Group the steps by reason to change:
   - `validateInput()`: ISBN and patron ID validation → reason to change: validation rules
   - `performCheckout()` → called on the Model: availability check, record creation, status update → reason to change: business logic
   - `persistChanges()` → Model's save method → reason to change: storage format
   - `updateView()`: clear form, show confirmation → reason to change: screen layout
4. **Write the decomposed handler:**
```java
checkoutButton.setOnAction(e -> {
    if (validateInput()) {
        model.checkout(isbnField.getText(), patronField.getText());
        updateView();
    }
});
```

**Answer:** The handler was a "closet handler" — it stuffed unrelated responsibilities into one method. After decomposition, the handler itself is 3–4 lines. Business logic lives in the Model. View updates live in a dedicated method.

**What to notice:** The handler does not need to shrink — it needs to *delegate*. Three lines in the handler can represent work that happens across four well-named methods.

---

## Tier 1 — Warm-Up

*(Tests: recall, conceptual identification, true/false with explanation)*

**Exercise 1.** (Tests: recall — handler responsibility rule)
What is the handler responsibility rule? State it in one sentence. Then give one example of a handler that follows it and one that violates it. Use a library or hospital app as your context — not an abstract example.

**Exercise 2.** (Tests: true/false — business logic in handler)
True or False — then explain your answer in 2–3 sentences:

> "A button click handler is the appropriate place to write the business logic for a checkout operation, because it is triggered directly by the user action."

**Exercise 3.** (Tests: vocabulary — handler registration)
What does it mean to "register" a handler? Write the lambda form of registering a handler for a "Checkout" button click in JavaFX. Your lambda should call a method named `handleCheckout()` rather than contain inline logic.

**Exercise 4.** (Tests: recall — three handler forms)
What are the three ways to register an event handler in Java? For each, give a one-line description of when you would choose it over the others.

**Exercise 5.** (Tests: true/false — long handler acceptability)
True or False — then explain your answer in 2–3 sentences:

> "A handler that is 50 lines long and handles validation, model update, view update, and persistence is acceptable if it passes all tests."

---

**Exercise 5b.** (Tests: handler responsibility — contrastive classification)

Classify each step below as belonging in the **handler** (translation only), the **Model** (business logic), or the **View** (display update). Write one sentence justifying each classification.

- (a) `isbnField.getText()` — read the ISBN from the input field
- (b) Check whether the book is currently available for checkout
- (c) `statusLabel.setText("Checkout complete!")` — update the label after checkout
- (d) Determine whether a patron has exceeded their borrow limit
- (e) Call `model.checkout(isbn, patronId)` from inside the handler

*(Why this is tempting to get wrong: (e) is tempting to classify as "Model" because it calls a model method. But the call itself lives in the handler — the handler is doing the translation. The business logic is inside `model.checkout()`, not inside the call that invokes it.)*

---

## Tier 2 — Application

*(Tests: decomposition, error analysis, AI interaction, tracing)*

**Exercise 6.** (Tests: handler decomposition — responsibility rule applied)
A student's checkout button handler (collapsed to pseudocode) does all of this:

```
handleCheckout():
  get isbn from field
  validate isbn not empty
  validate isbn format
  find book in catalog
  check book availability
  get patron from field
  validate patron id
  find patron in catalog
  create checkout record
  update book status
  update patron record
  save to file
  clear form fields
  show confirmation screen
  update status label
```

Apply the responsibility rule. Group these steps into at most four methods with clear names. For each method: name it, list which steps belong to it, and explain in one sentence why those steps belong together.

**Exercise 7.** (Tests: error analysis — named inner class with mixed concerns)
A student writes a named inner class handler:

```java
class CheckoutHandler implements ActionListener {
    public void actionPerformed(ActionEvent e) {
        String isbn = isbnField.getText();
        Book book = new Book(isbn, titleField.getText(), authorField.getText());
        catalog.add(book);
        checkoutLabel.setText("Checked out: " + book.getTitle());
    }
}
```

Identify two distinct problems. For each problem: name it, explain what principle it violates, and describe the correction.

**Exercise 8.** (Tests: lambda vs. named inner class — justified choice)
You are writing a handler for a "Save" button that needs to: (a) call `model.save()`, (b) show a confirmation dialog, and (c) disable the save button until new changes are made.

Should you use a lambda or a named inner class? Justify your choice using the criteria from this chapter. Then write the handler skeleton in whichever form you chose — show the structure, not just the choice.

**Exercise 9.** (Tests: AI interaction — handler decomposition, model-view boundary)
A student asks an AI: *"My checkout button handler is getting too long. How should I fix it?"*

The AI responds:

> "Break it into smaller private methods inside the handler class. Extract helper methods like `validateInput()`, `processCheckout()`, and `updateDisplay()`. Keep everything inside the handler class for simplicity."

- Identify the strongest point in the AI's response.
- Identify what the AI missed about the model-view boundary.
- Write a correction that specifies where each of the three extracted methods should actually live, and why.
- **(d)** State the specific test you would run to verify that `processCheckout()` — now in the Model — is tested correctly. Describe what the test asserts and why that assertion cannot be made through the handler directly.

**Exercise 9b — Self-Explanation** (Tests: handler responsibility rule — why "single reason to change" matters)

In this chapter, the handler responsibility rule is defined as: a handler has one reason to change — the event wiring changes. Explain in 2–3 sentences why "single reason to change" is a useful test for whether a method belongs in the handler or elsewhere. Your explanation must use the term **"reason to change"** correctly and name one specific reason that would require editing the handler if business logic were left inside it.

**Exercise 9c — Cumulative** (Tests: handler decomposition + MVC from Ch 10)

In Ch 10, the Controller translates user events into model operations. In Ch 11, handlers are the code that responds to a specific event. A student's `handleCheckout()` method calls `catalog.findByIsbn()`, validates availability, creates a `CheckoutRecord`, and updates the status label — all inline.

(a) Which of these steps violate the handler responsibility rule from Ch 11?
(b) Which MVC layer should own the availability check and record creation? Why?
(c) Rewrite `handleCheckout()` as it should appear after decomposition — three to five lines maximum. The handler should only contain what the responsibility rule allows.

**Exercise 10.** (Tests: click-to-view trace — responsibility rule applied end to end)
A user clicks the "Return Book" button in a library app. Trace the complete flow:

- (a) What event fires?
- (b) What does the handler do — following the responsibility rule?
- (c) Which model method is called, and what does it return?
- (d) Which view update method is called?
- (e) What does the user see change on screen?

Write this as a numbered sequence with one sentence per step. The handler itself should be no more than 2–3 lines.

---

## Tier 3 — Synthesis

*(Tests: cross-chapter integration, named prior chapters explicitly)*

**Exercise 11.** (Tests: synthesis — Ch 11 + Ch 10, handler position in MVC)
In Ch 10, controllers mediate between view events and model operations. In Ch 11, handlers are the code that responds to events.

Explain the relationship between handlers and controllers: Is a handler the same as a controller, a part of a controller, or a separate concept? Use a concrete "checkout button" example to show where the handler lives in the MVC architecture, what it calls, and what it does not do.

A surface answer says "handlers are part of the controller." A strong answer uses MVC vocabulary from Ch 10 and handler vocabulary from Ch 11 to show the handler calling a model method and a view-update method — not doing business logic itself.

**Exercise 12.** (Tests: synthesis — Ch 11 + Ch 3, setter-before-show in handler chain)
In Ch 3, the setter-before-show contract requires setting state on a screen before navigating to it. In Ch 11, handlers chain together model update and view update.

Design the complete handler chain for a "Checkout Complete → Show Confirmation" flow. Show:
- (a) The handler pseudocode
- (b) Where the model update happens
- (c) Where the setter-before-show call happens
- (d) Where the navigation happens

Explain why each step must happen in this specific order. What breaks if you navigate before calling the setter?

A surface answer sequences the steps. A strong answer uses setter-before-show vocabulary from Ch 3, applies the handler responsibility rule from Ch 11, and explains the failure mode for each wrong ordering.

---

## Tier 4 — Challenge

*(No answer key. Rubric only. Open-ended design.)*

**Exercise 13.** (Tests: handler architecture — shared model/view, five-button system)
A library app has five buttons: Checkout, Return, Search, Save, and Clear. Each button's handler currently contains mixed validation, model, view, and persistence logic. You are refactoring to enforce the responsibility rule.

Design a handler architecture that:
- (a) Defines which classes exist and what each class owns
- (b) Describes how handlers for all five buttons share the model and view without duplicating code
- (c) Handles the case where both Save and Checkout need to call persistence

Then describe the trade-off between creating one `CheckoutController` class with five inner handler classes vs. five separate top-level handler classes.

**Rubric — what distinguishes a strong response:**
- Proposes a concrete class structure with actual class names and responsibilities (not vague categories)
- Shows how model and view are passed in (dependency injection) rather than accessed globally
- Addresses the persistence-sharing problem specifically — names a solution
- Makes an explicit, reasoned judgment on the one-controller-with-inner-classes vs. five-separate-classes trade-off
- Does not conflate "handler" with "method"

---

## Full Answer Key — Tiers 1–3

### Exercise 1
**Handler responsibility rule:** A handler's only job is to translate a user event into a model operation and update the view — it should not contain business logic itself.

**Follows the rule:** A checkout button handler that calls `model.checkout(isbn, patronId)` and then calls `view.showConfirmation()`.

**Violates the rule:** A checkout button handler that validates the ISBN format, checks book availability, creates a checkout record, and saves to disk — all inline.

### Exercise 2
**False.** The handler is triggered by the user action, but "triggered by" does not mean "responsible for." Business logic in a handler cannot be tested without simulating a button click. If the checkout rules change (e.g., a new late-fee policy), the handler changes — but the handler should only change when the event-wiring changes, not when business rules change. Business logic belongs in the Model.

### Exercise 3
"Registering" a handler means associating a piece of code with a specific event source so that the code executes whenever that event occurs.

Lambda registration for a checkout button:
```java
checkoutButton.setOnAction(e -> handleCheckout());
```
The lambda contains only the delegation call, not the logic.

### Exercise 4
1. **Lambda expression** — use when the handler is short (1–3 lines) and does not need to be reused or tested independently.
2. **Anonymous inner class** — use when the handler needs to implement an interface with multiple methods or when lambdas are not supported (older Java).
3. **Named inner class** — use when the handler is complex enough to warrant a name, needs to be tested independently, or is reused by more than one event source.

### Exercise 5
**False.** Passing tests verifies behavior but does not validate design. A 50-line handler with mixed responsibilities has multiple reasons to change: the validation rules may change, the model API may change, the view layout may change, or the persistence format may change. The responsibility rule is violated regardless of test outcomes. Long handlers also cannot be tested in isolation — you cannot test the validation step without triggering the persistence step.

### Exercise 6
```
validateInput():
  - get isbn from field
  - validate isbn not empty
  - validate isbn format
  - get patron from field
  - validate patron id
  Reason: all input checks, one reason to change: validation rules change

performCheckout():
  - find book in catalog
  - check book availability
  - find patron in catalog
  - create checkout record
  - update book status
  - update patron record
  Reason: all model operations, one reason to change: checkout business logic changes

persistChanges():
  - save to file
  Reason: all persistence, one reason to change: storage format changes

updateView():
  - clear form fields
  - show confirmation screen
  - update status label
  Reason: all view updates, one reason to change: screen layout or messaging changes
```

### Exercise 7
**Problem 1 — Creating a new Book instead of finding one:**
The handler calls `new Book(isbn, ...)`, constructing a new `Book` from field values instead of looking up the existing book in the catalog. This violates the Model-owns-truth principle — the catalog already has authoritative `Book` objects. The correction: call `catalog.findByIsbn(isbn)` and use the returned `Book` object.

**Problem 2 — Mixed model update and view update in the handler:**
The handler both modifies the catalog (`catalog.add(book)`) and updates the label (`checkoutLabel.setText(...)`). This is two separate responsibilities in one method. The correction: extract `catalog.add(book)` into a model method call and `checkoutLabel.setText(...)` into a separate view-update method, both called from the handler.

### Exercise 8
**Choice: Named inner class** (or a separate method in the controller, not a lambda)

**Justification:** The handler has three distinct responsibilities: calling the model, showing a dialog, and updating the button state. A lambda would force all three into one inline expression, making it hard to read, test, and extend. A named inner class (or a controller method registered with a short lambda) gives the logic a name and allows it to be tested without triggering a button click.

**Handler skeleton:**
```java
class SaveHandler implements EventHandler<ActionEvent> {
    @Override
    public void handle(ActionEvent e) {
        model.save();
        showSaveConfirmation();
        saveButton.setDisable(true);
    }
}
// Registration:
saveButton.setOnAction(new SaveHandler());
```

### Exercise 9
**Strongest point:** Extracting `validateInput()`, `processCheckout()`, and `updateDisplay()` is correct — the AI identified that decomposition is the right technique.

**What the AI missed:** Keeping all three methods inside the handler class keeps them in the View/event layer. `processCheckout()` contains model logic and belongs in a `LibraryModel` (or `CheckoutService`) class. `validateInput()` may also belong in the Model if it enforces business rules (not just input format). The model-view boundary requires that model operations live in model classes, not in handler helper methods.

**Corrected placement:**
- `validateInput()` — format checks stay in the handler/controller; business-rule checks (e.g., is the patron suspended?) move to the Model
- `processCheckout()` → `model.checkout(isbn, patronId)` — lives in the Model
- `updateDisplay()` — stays in the View/controller, called after the model operation completes

### Exercise 10
1. The user clicks the "Return Book" button; a JavaFX `ActionEvent` fires on the button.
2. The registered handler calls `handleReturn()` — two lines: one model call, one view call.
3. The handler calls `model.returnBook(isbn)`, which removes the active checkout record and marks the book available; the model returns the updated `Book`.
4. The handler calls `view.showReturnConfirmation(book.getTitle())`.
5. The status label updates to "Returned: [title]" and the book reappears as available in the TableView.

### Exercise 11
A handler is a part of the Controller layer, not a separate concept and not the same as the full controller. In MVC (Ch 10), the Controller mediates between view events and model operations. In Ch 11, a handler is the specific code that executes when one event fires — it is one unit of controller behavior.

For the checkout button: the handler lives in the Controller class (or is registered by it). The handler calls `model.checkout(isbn, patronId)` (a model operation), then calls `checkoutView.showConfirmation()` (a view update). The handler does not perform the checkout logic itself — that would put business logic in the Controller layer, which Ch 10 prohibits.

> **Common error:** A surface answer says "handlers are part of the controller." A strong answer uses both Ch 10 and Ch 11 vocabulary: the handler is one unit of controller behavior — it calls a model method, then calls a view-update method, and contains no business logic itself.

### Exercise 12
Handler pseudocode:
```
handleCheckoutComplete():
  (a) model.finalizeCheckout(checkoutRecord)    // model update first
  (b) confirmationScreen.setCheckoutRecord(...)  // setter before show (Ch 3)
  (c) sceneManager.navigateTo(confirmationScreen) // navigate after setter
```

**Why this order:**
- Model update must happen first: the confirmation screen needs accurate data from the model.
- The setter (Ch 3) must be called before navigation: if you navigate first and then call the setter, the confirmation screen's `initialize()` has already run without the data — the screen renders empty or throws a NullPointerException.
- Navigation must happen last: it triggers the screen transition, which fires `initialize()` on the new screen. All data must be in place before that runs.

**Failure mode:** Navigating before calling the setter causes the confirmation screen to initialize with null data, which either shows empty fields or crashes.

> **Common error:** A surface answer sequences the steps correctly but doesn't explain why. A strong answer names the specific failure: calling `initialize()` on the confirmation screen before the setter means the screen runs its setup code against a null `checkoutRecord`, throwing `NullPointerException` when any field is accessed.

---

## Instructor Notes

**Common student errors in this module:**

1. **Business logic in handlers:** The most frequent error. Students write `handleCheckout()` as a 30-line method because "it starts when the button is clicked." The corrective framing from Exercise 1: ask "if the checkout rules changed, would you need to edit the handler?" If yes, the logic is in the wrong place.

2. **Lambda for everything:** Some students use lambdas for all handlers, including complex ones. Exercise 8 targets this. The criterion is not syntax preference — it is whether the logic is complex enough to deserve a name and independent testability.

3. **Decomposition inside the handler:** Exercise 9's AI response deliberately gives the most common student "fix" — extracting helpers within the handler class. This feels correct but does not cross the model-view boundary. Use Exercise 9 as a discussion prompt: "Is this better than before? Is it done?"

**Sequencing recommendation:** Run Exercise 10 (click trace) on the board with students narrating each step before they write. Students who cannot narrate "the handler calls model, not implements logic" will produce handlers with business logic no matter how many exercises they do.

**Tier 3 notes:** Exercise 11 requires Ch 10 MVC vocabulary. Exercise 12 requires Ch 3 setter-before-show vocabulary. Students who skipped Ch 3 will sequence the handler steps incorrectly — they will navigate first. Use the failure mode as the teaching moment.

**Point distribution:** T1 = 5 pts each · T2 = 10 pts each · T3 = 15 pts each · T4 = 20 pts (rubric-graded)

**Bloom's distribution:**

| Tier | Bloom's Level | % of exercises |
|------|--------------|----------------|
| Tier 1 | Remember / Understand | ~25% |
| Tier 2 | Apply / Analyze | ~55% |
| Tier 3 | Analyze / Evaluate | ~12% |
| Tier 4 | Evaluate / Create | ~8% |

**Tier 4 note:** The strongest responses to Exercise 13 will name dependency injection explicitly — the model and view are passed into the controller (or handler class) rather than accessed via static references or globals. Accept any mechanism (constructor injection, setter injection) as long as it is named and the reason is given.
