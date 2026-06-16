# Module 10 — Event-Driven Programming with Scene Builder: Wonder Edition
## Companion Chapter

> **Wonder Edition:** Read this alongside the chapter, not instead of it.

---

## The Strange Question

A student completes nine modules of a library program. The console prints book titles, patron names, checkout records. Every method works. The model is correct.

Then the student adds a `TableView`. The window opens. The same catalog appears in rows and columns. The search bar filters by title. Everything still works — and looks completely different.

Here is the specific failure to observe. The student types in the search bar. Rows disappear from the table. The filtered results appear correctly. Then the student types a second search without clearing the first. The results are wrong. Some books that should appear do not.

What broke? And more precisely: where is the broken logic living?

---

## First Intuition

The first instinct is to look at the search method. The model's `search()` logic must have a bug. It is not returning the right books the second time.

That instinct comes from console programming experience. In a console program, if output is wrong, the method computing the output is wrong. The method is the only place the logic lives. Debugging means reading the method.

> **► Planning prompt:** Before continuing, write down your answer. Where do you expect the bug to be — in the model's search method, in the event handler, or somewhere else? What experience is driving that prediction? What would you check first, and in what order?

The instinct is not wrong about methods. It is wrong about where the logic is living. This program has two places where "which books are shown" could be decided. The model decides which books match a query. The table decides which rows are visible. When those two decisions are separate, a search can appear to work once and fail the second time — without any bug in the model at all.

---

## The Surprise

The model's search method is fine. It returns the correct books every time it is called.

The bug is in the table. The first search removed non-matching rows from the `TableView`'s items list. The table stored the removed rows nowhere. They are gone. When the second search runs, the model searches the full catalog and returns correct results — but the table's items list no longer contains the full catalog. It contains only the results of the first search. The model and the table now disagree about what the catalog is.

**But** — this creates an architectural puzzle that the bug alone does not resolve. If the table should not hold the authoritative book list, where does the list live? And if filtering means asking the model and then updating the table, how does the table "know" not to lose data it removed?

The answer is that the table should never remove rows in the first place. But that requires treating the table as a display surface — not as a data store. That distinction is the architecture this module is built on. It is not intuitive. It has to be named.

> **► Monitoring prompt:** Hold the contradiction. The table displays books. The model holds books. These seem like the same thing — just in two different places. What assumption made them feel equivalent? What fact about the bug contradicts that assumption? What is still unexplained about how the table and model stay synchronized?

---

## The Hidden Structure

The program has three layers, and the search bug is a symptom of collapsing two of them.

The model holds what is true about the library. The view displays what the model holds. The controller translates user actions into model calls and view updates. These three layers are the MVC architecture the chapter describes.

The search bug collapsed the model and the view. The table's items list became the authoritative catalog. The model's catalog and the table's rows became two separate sources of truth. One source of truth is an architectural principle, not a preference.

**Misconception Checkpoint**

> "It is tempting to think that MVC is a design pattern a programmer selects — an optional layer of organization that experienced developers add to complex projects. But the three responsibilities already exist in every GUI application. The correct model holds that any program with a user interface already has domain logic, display logic, and translation logic — whether or not those three are separated. The key distinction is that untangled responsibilities can be tested and changed independently; tangled responsibilities cannot be tested at all, because the test cannot reach one without activating the other."

**Code Trace**

The bad pattern treats the table as the data store:

```java
// BAD: view-modifies-model-data — table becomes the catalog
searchButton.setOnAction(e -> {
    String query = searchField.getText();
    tableView.getItems().removeIf(book ->
        !book.getTitle().toLowerCase().contains(query.toLowerCase()));
});
```

The correct pattern filters the model and updates the view:

```java
// CORRECT: controller calls model method, view reflects model result
searchButton.setOnAction(e -> {
    String query = searchField.getText();
    ObservableList<Book> results = FXCollections.observableArrayList(
        model.search(query)           // model owns the search logic
    );
    tableView.setItems(results);      // view displays whatever model provides
});
```

In the bad pattern, `tableView.getItems()` is the catalog. In the correct pattern, `model.search()` is the catalog. The table is a window onto the model, not a copy of it.

---

## Try Looking At It This Way

**Target:** The three-layer MVC split in a JavaFX library application, where the `TableView` displays model objects and the controller mediates user actions.

**Base:** A hospital with a records room, a patient display board, and a ward clerk.

**Features:**
- The records room stores patient files, diagnoses, and treatment histories. It applies medical rules. It does not know what the display board shows or what font it uses. It knows what is true about patients.
- The display board shows current patient status — room assignments, alert flags, scheduled procedures. It does not make medical decisions. It shows what it is given.
- The ward clerk receives requests from doctors and nurses, retrieves records from the records room, and updates the display board. The clerk translates between the two domains without being either one.

**Commonalities:**
- Records room does work according to rules, does not present — Model holds business state and logic, does not know about the GUI. Both exist to be correct, not to be visible.
- Display board shows current status, does not decide content — View renders model state, does not make domain decisions. Both are reactive surfaces, not decision-makers.
- Ward clerk translates in both directions, knows both domains — Controller receives user input, calls model methods, updates the view. Both are translators, not authorities.

**Boundaries:** The analogy holds for responsibility separation. It does not capture JavaFX's reactive rendering. A hospital display board does not automatically update when a patient file changes. A `TableView` cell value factory recomputes from the model object at render time — the view reaches into the model object directly, without the clerk carrying each value manually. The clerk (controller) triggers re-renders; it does not copy every field.

**Conclusions:** The hospital analogy makes the MVC split concrete. Each layer has one authority. When a layer absorbs another layer's authority — when the display board starts making triage decisions, or when the ward clerk starts practicing medicine — the system breaks in ways that cannot be tested at the point of failure.

---

## Where The Analogy Breaks

Unlike the hospital display board, the JavaFX `TableView` does not wait for the controller to carry each value from the model to the screen.

The cell value factory is a function the programmer defines. The `TableView` calls it at render time, passing each model object. The factory calls the model object's method directly — `book.getTitle()`, `book.isAvailable()`. The view reaches into the model without going through the controller.

This matters because it changes what the controller's job actually is. The controller does not copy data from model to view. It triggers state changes in the model and, when necessary, tells the view to re-render. A design that treats the controller as a data ferry — manually extracting every field from the model and pushing it into the view — misreads the architecture and produces controllers that are too large and too fragile.

Any argument built on the hospital analogy that treats the clerk as the only channel for patient data to reach the board will produce the wrong design in JavaFX.

---

## Small Discovery

Consider a supermarket with a paper shelf-tag system and a digital price display system.

In the paper system, every price change requires a store employee to walk to the shelf and replace the tag. A price change for 200 items means 200 physical trips. The tag holds the price. It is a copy.

In the digital system, each shelf display pulls the current price from the central inventory database when it renders. A price change in the database appears on every display the next time that display refreshes. No employee carries prices to shelves. The display does not store a copy — it reads from the source.

**Pattern search:** In the paper system, the store runs a "sale on all dairy" promotion. The manager updates the database. How many shelf tags still show the old price? How long does the error last? In the digital system, the manager updates the database. How many shelf displays show the old price after the next refresh?

**Prediction:** Write a number for each system before continuing. The paper system number depends on how fast employees walk. The digital system number depends on the refresh interval. One of these is structurally guaranteed to eventually become consistent. The other requires manual effort to reach consistency.

---

The revelation: the paper system has two sources of truth — the database and the tag. Whenever they diverge, the customer sees wrong information. The digital system has one source of truth — the database. The display is a live window onto it.

This is the cell value factory. The `TableView` does not store book titles or availability strings. It calls `book.getTitle()` and `book.isAvailable()` at render time. When the model changes — when a book is checked out — the next render reflects the new state. No manual copy, no divergence, no stale data.

The insight: a live view is not a copy. It is a function applied to the source at display time.

---

## What This Changes

**First:** The question of why the search bar bug occurred now has a precise answer. Removing rows from the `TableView` created a second source of truth. The model held the full catalog. The table held a reduced version. When the controller asked the model for search results the second time, the results were correct — but the table had forgotten half the books. The fix is not in the model. The fix is in not treating the table as a data store.

**Second:** The design of every event handler looks different. A handler that is forty lines long and contains conditions, calculations, and string formatting has absorbed model and view work it should not hold. A correct handler does four things: receives the event, extracts user input from the view, calls the model method, updates the view. Handlers that exceed that boundary are testable only by clicking buttons — which is not testing.

**Practice Bridge:** Refactor the search button handler — remove `tableView.getItems().removeIf(...)` or `tableView.getItems().clear()` followed by manual row re-insertion, and replace the entire body with `model.search(query)` followed by `tableView.setItems(FXCollections.observableArrayList(results))`. Verify that searching twice without clearing still returns correct results, and that clearing the search field and clicking again restores the full catalog from the model, not from a stored local variable.

**Open question:** The view displays model state correctly now. But when the user clicks "Check Out" and the model rejects the action — the patron is at their limit, the book is already gone — how does the view surface that failure? The model throws an exception or returns an error state. The controller catches it. The view must show a message without crashing. That feedback loop is Module 11's subject. The clean separation built here is the precondition for that loop to work.

---

## Wonder Questions

1. The cell value factory recomputes a book's title and availability every time the `TableView` renders that cell. If one hundred books are in the table and the table renders thirty frames per second, how many model method calls happen per second just for rendering? Does the answer change how a programmer should design the model's accessor methods?

2. The chapter says the model "does not know whether it is being displayed in a console or a GUI or a web browser." But a model method like `search()` returns a `List<Book>`. A JavaFX `TableView` works better with an `ObservableList<Book>`. Does wrapping the result in `FXCollections.observableArrayList()` belong in the controller, or does it violate the model-view boundary? Where exactly is the line?

3. A student adds a `getAvailabilityLabel()` method to `Book` that returns `"Available"` or `"Checked Out"`. The chapter calls this a violation. But `Book` already has `toString()`, which returns a string representation. What is the structural difference between `getAvailabilityLabel()` and `toString()`? Is the violation in the method or in how it is used?

4. The chapter says an event handler should be "no more than a dozen lines." A checkout handler that extracts the selected book, extracts the logged-in patron, calls `model.checkout(patron, book)`, and calls `tableView.refresh()` is eight lines. A handler that does the same thing but also disables the checkout button when no row is selected and re-enables it after checkout is fourteen lines. Is the second handler a violation? What is the actual criterion — and when does line count mislead?

5. The MVC split ensures the model can be tested without a GUI. But the controller cannot easily be tested without both a model and a view. Does MVC make controllers untestable? Or is there a design decision that makes controllers testable in isolation? What would that design look like?

---

**Precision Summary**

**What the concept is:** MVC is a three-layer architecture assigning domain truth to the model, rendering to the view, and mediation to the controller. In JavaFX, the cell value factory is the seam where the view pulls display values directly from model objects at render time — not through the controller.

**What it explains:** Why filtering by removing `TableView` rows creates two sources of truth and breaks on the second search; why `Book.getColor()` is a violation even if it is convenient; why a forty-line event handler almost certainly contains model logic that should be extracted; and why a testable system requires each layer to be reachable independently.

**What it does NOT mean:** MVC does not mean the controller manually ferries every field from model to view. It does not mean the view never touches the model — the cell value factory calls model methods directly. It does not mean more layers are always better, or that MVC is a pattern a programmer opts into rather than a structure that already exists in any GUI application.

**What comes next:** The model enforces rules. It will reject actions — a patron at their limit, a book already checked out. The controller must catch these rejections. The view must surface them to the user without crashing. Module 11 addresses the feedback loop between model errors and view state, and it depends entirely on the clean separation built here.
