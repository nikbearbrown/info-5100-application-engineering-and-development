# Worked Exercises: Event-Driven Programming with Scene Builder

*Chapter 10 of INFO 5100 Application Engineering and Development*

> These exercises follow a research-backed sequence: full worked example → matched practice → completion problem → error-recognition → transfer → interleaved review. Each section builds on the previous. Do not skip ahead.

This chapter is built on one distinction: the **model** holds business truth, the **view** displays it, and the **controller** mediates between them. The view in JavaFX is the **scene graph** — a tree of nodes inside a **stage** (window) — built from **panes** (`VBox`, `HBox`, `BorderPane`, `GridPane`) and **controls** (`Button`, `TextField`, `TableView`). The chapter's central artifact is the `TableView<Book>` whose columns each have a **cell value factory** — "the seam between the view and the model" — that calls a `Book`'s own method at render time. The module's single capability: a visual interface where every visible value is traceable to a model object and no display logic has migrated into the model.

---

## Prerequisites

- You completed the Chapter 9 model: a `List<Book>` catalog and a model search method that returns a filtered list.
- You can read JavaFX construction code (`new BorderPane()`, `new TableView<Book>()`, `setCenter(...)`).
- You understand that a `Book` exposes domain state through methods like `getTitle()`, `getAuthor()`, and `isAvailable()`.

---

## Part A — Full Worked Example: A TableColumn Whose Cell Value Factory Reads the Model

**What this demonstrates:** How a `TableView<Book>` column displays a model value by calling a `Book` method through a cell value factory at render time, rather than storing a copy of the data.

**The problem:** You have a `TableView<Book> bookTable` backed by the catalog's `Book` objects. Add a title column that shows each book's title. The displayed value must come from the model (`Book.getTitle()`), not from a string copied into the table.

```java
TableView<Book> bookTable = new TableView<>();
bookTable.setItems(catalog.getObservableBooks()); // real Book objects
TableColumn<Book, String> titleColumn = new TableColumn<>("Title");
// titleColumn must show each Book's title.
```

**The solution:**

**Step 1 — Decide who owns the displayed value.**
The title is **business state** owned by the model. The column's job is to display it, not to invent it.
*Why:* The model "holds business state"; the view "displays model state." Keeping the title a model concern means the table is a *view onto* the model, not a parallel copy. Two copies "will diverge."
*Check:* `getTitle()` lives on `Book`, in the model. Correct ownership.

**Step 2 — Wire the cell value factory to call the model method.**
```java
titleColumn.setCellValueFactory(cell ->
    new SimpleStringProperty(cell.getValue().getTitle()));
```
*Why:* The cell value factory is "a function that, given a `Book` object, returns the value to display." It "calls the model's own methods to extract what it needs," computing the displayed value from the model *at render time*.
*Check:* `cell.getValue()` is the row's `Book`; `.getTitle()` is a model call. No string was stored in the table.

**Step 3 — Attach the column to the table.**
```java
bookTable.getColumns().add(titleColumn);
```
*Why:* The table is the **control** in the **scene graph** that renders the column; the column is the view artifact that holds the factory. Layout and rendering are the view's business; the data is the model's business.
*Check:* `bookTable.getColumns()` now contains `titleColumn`.

**Step 4 — Trace one displayed value from screen to model.**

| layer | artifact | what it does |
| --- | --- | --- |
| view (control) | `bookTable`, row 0 | renders a row for a `Book` |
| view (column) | `titleColumn` | holds the cell value factory |
| seam | `setCellValueFactory(...)` | calls `getValue().getTitle()` at render time |
| model | `Book.getTitle()` | returns the business state |

*Why:* The verification the module requires is exactly this trace: "this string on screen came from this field on this object by way of this cell value factory." If you cannot trace it, the separation is violated.
*Check:* If a `Book`'s title changes in the model and the row re-renders, the cell shows the new title with no view code change.

**Final answer:**
```java
TableColumn<Book, String> titleColumn = new TableColumn<>("Title");
titleColumn.setCellValueFactory(cell ->
    new SimpleStringProperty(cell.getValue().getTitle()));
bookTable.getColumns().add(titleColumn);
```

**What made this work:** The central concept is the **cell value factory as the seam** between view and model. The naive approach copies model state into the table — extracting each title into a string and storing it in the cell. That creates two sources of truth: when the model's title changes, the stored copy does not, and the table silently shows stale data. Letting the factory call `getTitle()` at render time keeps the model authoritative.

**Self-explanation prompt:** Why does computing the cell value at render time (calling `getTitle()` each draw) keep the model and view in sync, while storing the title string in the cell once does not?

---

## Part B — Matched Practice Problem: An Availability Column

**Same structure, different surface.** Add an availability column to `bookTable` that shows `"Available"` when `book.isAvailable()` is true and `"Checked Out"` when it is false. The label text is a **display** representation; the boolean `isAvailable()` is the **business** state.

Work the same four steps:
1. Decide who owns the value — which part is model state, which part is the display string?
2. Wire the cell value factory so it calls `isAvailable()` and *maps* the boolean to a label.
3. Attach the column to the table.
4. Trace the displayed `"Checked Out"` string back to `Book.isAvailable()`.

**Stuck?** The model must return the boolean `isAvailable()`; the *view* decides the words. Do not add a `getAvailabilityLabel()` to `Book` — that would push display words into the model.

*Instructor note: No solution is provided for Part B. Build the column and the four-step trace yourself, and confirm the word "Available" never appears anywhere in the `Book` class.*

---

## Part C — Completion Problem: A Search Bar That Filters the Model

Goal: a `TextField searchField` and `bookTable`. When the user types a query and the controller runs, the table shows only matching books — by asking the **model**, not by deleting rows from the table.

**Step 1 — Identify the layers (complete).**
The `searchField` is a **control** in the view. The controller reads its text. The model owns the search.
*Why:* The controller "mediates between view events and model operations"; the model is "the single source of truth."

**Step 2 — Read the query in the controller (complete).**
```java
String query = searchField.getText();
List<Book> results = catalog.search(query); // the Module 9 model method
```
*Why:* The controller calls "the same method that existed before there was a GUI." The model returns the filtered list; the view did not decide which books exist.

**Step 3 — [BLANK] Update the table to show the model's result.**
*Your work here:*
_______________________________________________
*Why (your explanation):*
_______________________________________________

**Step 4 — [BLANK] Handle clearing the search (empty query).**
*Your work here:*
_______________________________________________
*Why (your explanation):*
_______________________________________________

**Step 5 — Verify (complete).**
Searching, then clearing, returns the full catalog with no rows lost — because the controller always re-asks the model rather than removing rows from the table. There is one list of books: the model's.

**Final answer:**
```java
String query = searchField.getText();
List<Book> results = query.isEmpty()
    ? catalog.getAllBooks()
    : catalog.search(query);
bookTable.setItems(FXCollections.observableArrayList(results));
```

**Self-explanation prompt:** Why does asking the model for results (and resetting the table's items) avoid the "two lists of books" problem that deleting rows from the table creates?

---

## Part D — Error-Recognition Problem

> **Use this section only after completing Parts A–C.**

Goal: show available books with green title text and checked-out books with red title text in the catalog table.

**Step 1 — Identify the layers (correct).**
Color is a **display** decision; availability is **business** state. The view should decide the color from the model's boolean.

**Step 2 — Read the model's availability (correct).**
`Book.isAvailable()` returns the boolean the view will use.

**Step 3 — ⚠ Add the color to the model.**
```java
public class Book {
    private boolean available;
    public String getTitleColor() {                  // ⚠ added to the model
        return available ? "green" : "red";
    }
}
// view:
titleColumn.setCellValueFactory(cell ->
    new SimpleStringProperty(cell.getValue().getTitleColor()));
```

**Step 4 — Confirm the colors appear (correct-looking).**
The table renders green and red titles. The demo looks right.

**Your tasks:**
1. **Identify and explain the error.** `getTitleColor()` puts a **display** decision — a color string — inside the **model**. The `Book` class now "knows about colors. It knows about the GUI." Run the app headlessly (a batch export, a web API, a test), and `Book` carries GUI concepts that serve no purpose and pull JavaFX-flavored dependencies into the domain model.
2. **Write the corrected Step 3.** Keep `Book` returning domain state; let the view decide the color with a custom `TableCell`:
```java
// Book stays pure: only isAvailable() — no colors.
titleColumn.setCellFactory(col -> new TableCell<>() {
    @Override protected void updateItem(String title, boolean empty) {
        super.updateItem(title, empty);
        if (empty || getTableRow() == null || getTableRow().getItem() == null) {
            setText(null); setStyle("");
        } else {
            Book b = (Book) getTableRow().getItem();
            setText(title);
            setStyle(b.isAvailable() ? "-fx-text-fill: green;"
                                     : "-fx-text-fill: red;");
        }
    }
});
```
3. **Name the principle violated.** "Model objects return domain state. View logic decides how to display that state." The color decision belongs in the view; the availability decision belongs in the model.
4. **Write a test that catches this class.** Compile or run the model in isolation with no JavaFX on the classpath. If `Book` references colors, fonts, or any `javafx.scene` type, the test fails — exposing display logic that migrated into the model.

**Why this error is common:** The `Book` already knows its availability, so returning the *display* of that state from the same class feels like a convenient shortcut — until the model has to run somewhere there is no screen.

---

## Part E — Transfer Problem: A Weather Station Dashboard

A weather dashboard has a `TableView<Reading>` of sensor `Reading` objects, each with `getCelsius()` and `isStale()` (a reading older than five minutes). A temperature column must show the value, and stale readings should appear dimmed. There is no chapter weather example; the model/view boundary is identical to the library's availability-color problem.

Design it: which value comes from `Reading` (the model), where does the "dimmed" decision live, and how do you write the column so `Reading` never learns the word "dimmed" or any color?

**Hint (use only if stuck after 10 minutes):** `Reading` should expose `getCelsius()` and `isStale()` only. The dimming is a custom `TableCell`/`cellFactory` decision in the view, mirroring the green/red title cell.

**Reflection prompt:**
1. Which method did you put on `Reading`, and which decision did you deliberately keep out of it?
2. If the dashboard later ran as a headless data export, what about your design guarantees `Reading` still works unchanged?

---

## Part F — Interleaved Review

**Problem F1.** For the catalog view, classify each item as model, view, or controller responsibility and justify in one sentence each: (a) storing the `List<Book>`; (b) rendering availability as green or red; (c) calling `patron.borrow(book)` on a button click; (d) deciding which column headers appear.
*Chapter this draws from: Chapter 10 (Event-Driven Programming with Scene Builder).*

**Problem F2.** A `Button checkoutButton` should set `statusLabel` to `"Checkout requested."` on click. Write the registration with `setOnAction`, and name the event source and the event class involved.
*Chapter this draws from: Chapter 9 (Event-Driven Programming) — the event source / event / handler structure.*

**Problem F3.** A detail panel must show the selected book's due date formatted as `"Due: Jun 18"`. Is computing that formatted string a *model* responsibility (it derives from the loan's date) or a *view* responsibility (it is presentation)? Defend your answer.
*Note to instructor: intentionally ambiguous — the due *date* is model state, but the *format* is presentation. A strong answer has the model expose the date and the view do the formatting.*

**Closing reflection:** Across F1–F3, which decisions were truly the model's truth and which were the view's presentation? The discipline of this chapter is holding that line under pressure.

---

## Instructor Notes

**Common errors to watch for:**
- Adding display methods (`getTitleColor()`, `getAvailabilityLabel()`) to model classes — display logic leaking into the model.
- Implementing search by deleting rows from the `TableView`, creating two lists of books (model and removed-rows store).
- Storing extracted strings in cells instead of letting the cell value factory call the model at render time, producing stale displays.

**Signs a student needs to return to the chapter:**
- The student cannot trace a displayed value from screen to a specific model method.
- The student puts business decisions (eligibility, the three-book limit) into the view or the cell factory.

**Scaffolding adjustments:** If a student struggles in Part A, have them write the trace table (Step 4) *before* writing the factory, so the seam is named first. If a student finishes Part F quickly, ask them to add a second column whose value is *derived* from two model fields and decide where the derivation belongs.

**Domain adaptation note:** Replace the `Book` catalog table with a `Product` inventory table (name, quantity, status) or an `Appointment` scheduling grid (patient, provider, time, status); the cell-value-factory seam and model/view boundary are identical.
