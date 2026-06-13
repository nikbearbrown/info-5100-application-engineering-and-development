# Module 10 — Scene Builder: MVC Architecture and TableView
## Exercise Set

**Learning Objectives**
1. Design MVC architectures with clean layer separation
2. Implement TableView with cell value factories
3. Build search that filters the model, not the view
4. Trace values from GUI controls back to model fields

**Core Concepts:** MVC (Model/View/Controller), scene graph, TableView, cell value factories, model owns truth and business logic, view displays model state, controller mediates, search filters model not table, display logic vs. business logic

---

## Tier 1 — Warm-Up

*(Tests: recall, conceptual identification, true/false with explanation)*

**Exercise 1.** (Tests: recall — MVC layer responsibilities)
In MVC, which layer owns business state and logic? Which layer should never contain business logic? What is the controller's specific responsibility? Answer each question in one sentence.

**Exercise 2.** (Tests: true/false — search-on-view anti-pattern)
True or False — then explain your answer in 2–3 sentences:

> "To implement a search filter in a TableView, you should loop through the table rows and remove rows that don't match the search term."

**Exercise 3.** (Tests: vocabulary — cell value factory)
What is a cell value factory in a TableView? What does it connect, and why is it required? Answer in 3–4 sentences.

**Exercise 4.** (Tests: recall — scene graph structure)
What is the scene graph in JavaFX? What is the relationship between a scene, a root node, and child nodes? Draw or describe the hierarchy using a login screen as your example.

**Exercise 5.** (Tests: true/false — display logic placement)
True or False — then explain your answer in 2–3 sentences:

> "A method that formats a date for display (e.g., `formatDisplayDate()`) belongs in the Model class because it operates on model data."

---

## Tier 2 — Application

*(Tests: design, error analysis, AI interaction, tracing)*

**Exercise 6.** (Tests: MVC layer assignment with justification)
A hospital appointment system has a screen showing a table of appointments with a search bar. Assign each of the following responsibilities to the correct MVC layer and justify each assignment in one sentence:

- (a) Stores the list of `Appointment` objects
- (b) Filters appointments by doctor name
- (c) Calls `model.search()` when the user types in the search bar
- (d) Formats appointment dates for table display
- (e) Removes an appointment from the system

**Exercise 7.** (Tests: error analysis — search-on-view, data loss on clear)
A student implements search in their library catalog view:

```java
searchField.textProperty().addListener((obs, old, newVal) -> {
    for (int i = tableView.getItems().size() - 1; i >= 0; i--) {
        Book book = tableView.getItems().get(i);
        if (!book.getTitle().contains(newVal)) {
            tableView.getItems().remove(i);
        }
    }
});
```

(a) Identify the architectural violation — name the MVC principle being broken.
(b) Explain what breaks when the user clears the search bar (types, then deletes back to empty).
(c) Rewrite the handler using the correct MVC approach. Your rewrite should call a model method and update the TableView from the model's return value.

**Exercise 8.** (Tests: TableView setup — cell value factories)
Design the TableView setup for a Student enrollment screen with columns: `studentId`, `lastName`, `firstName`, `major`, and `gpa`.

Write:
- (a) The `TableView` declaration with the correct generic type
- (b) Three cell value factory examples using `PropertyValueFactory`
- (c) One cell value factory using a lambda for a computed display value — specifically, a "Last, First" combined name column

**Exercise 9.** (Tests: AI interaction — MVC misplacement of logic)
A student asks an AI: *"Where should I put the logic that calculates a student's GPA from their grades?"*

The AI responds:

> "Put it in the Controller class since that's where you have access to both the model data and the UI to display the result. This keeps your logic centralized."

- Identify the strongest point in the AI's response.
- Identify the MVC violation.
- Write a corrected answer that specifies exactly which class should own GPA calculation and why.

**Exercise 10.** (Tests: layer tracing — full GUI-to-model round trip)
A user types "Smith" in the doctor search bar of a hospital scheduling app and the table updates to show only Dr. Smith's appointments. Trace this interaction from start to finish through all three MVC layers:

- (a) What event fires and where does it fire?
- (b) What does the controller do in response?
- (c) What does the model do and what does it return?
- (d) How does the view update?

Write this as a numbered sequence with one sentence per step.

---

## Tier 3 — Synthesis

*(Tests: cross-chapter integration, named prior chapters explicitly)*

**Exercise 11.** (Tests: synthesis — Ch 10 + Ch 5, Catalog as Model-layer concern)
In Ch 5, the `Catalog` holds supply-side entities and answers queries. In Ch 10, the Model layer holds business state and logic.

Explain how these two concepts map onto each other:
- (a) Is the `Catalog` a Model-layer concern or a supply-side concern? Explain.
- (b) What does `search()` in the Model call on the `Catalog`?
- (c) Can the Controller ever call the `Catalog` directly? Why or why not?

A surface answer names the layers. A strong answer shows `search()` as delegation from Model to Catalog and applies the MVC boundary: Controller calls Model, not Catalog directly.

**Exercise 12.** (Tests: synthesis — Ch 10 + Ch 9, collection design within Model)
In Ch 9, you learned to choose collections based on operation profiles. In Ch 10, the Model holds collections of domain objects.

The library catalog Model needs to: support O(1) lookup by ISBN, display books in alphabetical order in a `TableView`, and quickly check whether a book is available.

Apply the collection design reasoning from Ch 9 to the Model layer in Ch 10:
- What fields does the `Model` need, and of what types?
- How does a `getAllSorted()` method connect to `TableView.setItems()`?
- Why does one Model legitimately hold two different collection fields?

A surface answer lists data structures. A strong answer applies operation-profile reasoning to field design, correctly connects the sorted list to `TableView.setItems()`, and shows a `Map` for O(1) lookup inside the same Model.

---

## Tier 4 — Challenge

*(No answer key. Rubric only. Open-ended design.)*

**Exercise 13.** (Tests: architectural reasoning — display formatting diversity across views)
MVC works cleanly when the View only displays what the Model provides. Design a scenario where a single field in the Model needs to be displayed differently in three different Views — for example, an appointment date shown as `"MM/DD/YYYY"` in a table, `"Monday, June 13"` in a detail panel, and `"June 13 at 2:00 PM"` in a confirmation dialog.

Propose three different architectural approaches for handling this formatting diversity. For each approach:
- Describe where the formatting logic lives
- State the trade-off
- Identify which MVC principle it respects or violates

**Rubric — what distinguishes a strong response:**
- Proposes three genuinely distinct approaches (not three variations of one idea)
- Correctly identifies which approaches violate Model-layer purity
- Makes an explicit recommendation with a stated trade-off
- Uses MVC vocabulary consistently (model, view, controller — not "class" or "place")

---

## Full Answer Key — Tiers 1–3

### Exercise 1
The **Model** owns business state and logic. The **View** should never contain business logic. The **Controller's** specific responsibility is to receive user events and translate them into model operations, then update the view with the result.

### Exercise 2
**False.** Removing rows from `tableView.getItems()` mutates the data the TableView is displaying, not a separate filter. When the user clears the search bar, the removed rows are gone permanently and cannot be restored. The correct approach is to filter the model's underlying list and reassign it to the TableView.

### Exercise 3
A cell value factory is a callback assigned to each `TableColumn` that tells the column how to extract the display value for each row object. It connects a column in the TableView to a specific property of the row's model object. It is required because `TableView<T>` does not know which field of `T` to show in which column — the factory provides that mapping explicitly.

### Exercise 4
The scene graph is JavaFX's hierarchical tree of all visual elements. A `Scene` holds a single root node (typically a layout container like `VBox` or `BorderPane`). The root node contains child nodes, which may themselves contain children, forming a tree. For a login screen: `Scene → VBox (root) → [Label, TextField, PasswordField, Button]`.

### Exercise 5
**False.** `formatDisplayDate()` is display logic, not business logic. It exists to serve a particular view's presentation requirement, not to enforce a domain rule. Moving it into the Model creates a dependency on view concerns inside the Model layer, violating the separation of concerns. Display formatting belongs in the View or in a utility class used only by the View.

### Exercise 6
| Responsibility | Layer | Justification |
|---|---|---|
| (a) Stores the list of Appointment objects | Model | The Model owns all business state |
| (b) Filters appointments by doctor name | Model | Search is a business operation on business data |
| (c) Calls model.search() when user types | Controller | Controller translates GUI events into model calls |
| (d) Formats appointment dates for display | View | Formatting is a display concern, not a domain rule |
| (e) Removes an appointment from the system | Model | Deletion is a state change — business logic |

### Exercise 7
(a) **Architectural violation:** The handler is mutating `tableView.getItems()` directly, operating on the View layer instead of delegating to the Model. This is the "search-on-view" anti-pattern — the View is being used as the source of truth for filtering, not the Model.

(b) **What breaks on clear:** When the user deletes all typed characters, `newVal` is an empty string, which matches nothing using the remove logic — but the removed rows were already deleted from `tableView.getItems()` in prior keystrokes. There is no way to restore them because the original list was modified in place.

(c) **Corrected handler:**
```java
searchField.textProperty().addListener((obs, old, newVal) -> {
    List<Book> results = model.search(newVal);
    tableView.setItems(FXCollections.observableArrayList(results));
});
```
The model holds the original list and returns a filtered subset. The view is always set from the model's return value, never mutated directly.

### Exercise 8
(a) `TableView<Student> studentTable = new TableView<>();`

(b) Three `PropertyValueFactory` examples:
```java
TableColumn<Student, String> idCol = new TableColumn<>("Student ID");
idCol.setCellValueFactory(new PropertyValueFactory<>("studentId"));

TableColumn<Student, String> lastCol = new TableColumn<>("Last Name");
lastCol.setCellValueFactory(new PropertyValueFactory<>("lastName"));

TableColumn<Student, Double> gpaCol = new TableColumn<>("GPA");
gpaCol.setCellValueFactory(new PropertyValueFactory<>("gpa"));
```

(c) Lambda for computed "Last, First" column:
```java
TableColumn<Student, String> nameCol = new TableColumn<>("Name");
nameCol.setCellValueFactory(cellData -> {
    Student s = cellData.getValue();
    return new SimpleStringProperty(s.getLastName() + ", " + s.getFirstName());
});
```

### Exercise 9
**Strongest point:** The AI is correct that GPA calculation needs to be centralized somewhere rather than scattered.

**MVC violation:** Placing business logic in the Controller is an MVC violation. The Controller's job is to translate events, not to compute domain values. If GPA calculation lives in the Controller, it cannot be tested without a GUI and cannot be reused by other screens.

**Corrected answer:** GPA calculation belongs in the `Student` model class (or a `GradeCalculator` service called by the Model). The Model owns business logic. The Controller should call `student.calculateGpa()` and then pass the result to the View for display — the Controller never performs the calculation itself.

### Exercise 10
1. The user's keystroke fires a `textProperty` change event on the `searchField` in the View.
2. The Controller's registered listener receives the new text value.
3. The Controller calls `model.searchByDoctor(newVal)`, delegating the filtering operation to the Model.
4. The Model iterates its internal list of `Appointment` objects, returning all whose doctor name matches the query.
5. The Controller calls `tableView.setItems(FXCollections.observableArrayList(results))`, handing the filtered list to the View.
6. The TableView re-renders, displaying only Dr. Smith's appointments.

### Exercise 11
(a) The `Catalog` is a supply-side concern that lives within the Model layer. It is the data store for supply-side entities (books, appointments, etc.), but it is accessed through the Model — the Controller never reaches past the Model to the Catalog directly.

(b) `search()` in the Model calls `catalog.findByDoctorName(query)` (or an equivalent Catalog method) and returns the result. The Model delegates the query to the Catalog rather than duplicating storage logic.

(c) The Controller cannot call the Catalog directly. MVC requires that the Controller only call the Model. Allowing the Controller to bypass the Model and call the Catalog directly breaks the layer boundary — the Controller would then be responsible for assembling results that are the Model's job to assemble.

### Exercise 12
**Model fields needed:**
```java
private Map<String, Book> booksByIsbn;        // O(1) lookup by ISBN
private List<Book> booksSortedByTitle;        // sorted for display
```

The `Map` supports O(1) ISBN lookup and availability checks. The `List` (kept sorted) is handed to `tableView.setItems()` directly.

**`getAllSorted()` → `setItems()` connection:**
```java
tableView.setItems(FXCollections.observableArrayList(model.getAllSorted()));
```
`getAllSorted()` returns a `List<Book>` sorted alphabetically. `setItems()` accepts an `ObservableList`, so the Controller wraps the result in `FXCollections.observableArrayList()`.

**Why two fields:** Different operations have different performance requirements. The Map serves O(1) lookup; the sorted List serves ordered display. Maintaining both is a deliberate design choice from Ch 9's operation-profile analysis — no single collection structure serves all three operations efficiently.

---

## Instructor Notes

**Common student errors in this module:**

1. **Search-on-view:** The most frequent error is Exercise 7's pattern — students mutate `tableView.getItems()` because it "works" for a single search but breaks on clear. Use Exercise 7 as a live debugging exercise: run the broken code, demonstrate the clear-bar failure, then trace the fix.

2. **Display logic in the Model:** Students frequently put `formatDisplayDate()` in the Model because it "touches model data." The corrective framing: ask "would this method need to change if we changed the screen layout?" If yes, it belongs in the View.

3. **Controller doing too much:** Students who have not internalized MVC place all logic in the Controller because it has references to both the model and the UI. Exercise 9's AI interaction is designed to surface and correct this.

**Sequencing recommendation:** Run Exercise 10 (layer tracing) as a full-class whiteboard exercise before assigning the written exercises. Students who can narrate the trace fluently answer Exercises 6, 7, and 11 correctly. Students who cannot narrate it will misassign responsibilities even after reading the chapter.

**Tier 3 notes:** Exercise 11 requires Ch 5 vocabulary (`Catalog`, supply-side). If students did not complete Ch 5, substitute: "A `BookRepository` holds all books. How does it relate to the Model?" Exercise 12 requires Ch 9 operation-profile reasoning. Students who chose collections without analysis in Ch 9 will give flat answers here.

**Tier 4 note:** Accept any three genuinely distinct approaches to Exercise 13. Common weak responses propose "put formatting in the Model," "put it in the Controller," and "put it in the View" as if these are three different approaches to the same problem rather than three distinct architectural stances. Push students to name the trade-off, not just the location.
