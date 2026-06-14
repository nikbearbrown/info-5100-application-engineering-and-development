# Module 12 — Recursion: FXML, Scene Builder, and @FXML Injection
## Exercise Set

> **Content note:** Despite the module title "Recursion," this chapter's exercises cover **FXML, Scene Builder layout, `@FXML` field injection, `fx:id`, and the `initialize()` lifecycle**. Recursion is not the topic of this chapter.

**Learning Objectives**
1. Design FXML layouts in Scene Builder and explain their structure
2. Write FXML-controller mapping tables as a verification discipline
3. Implement controllers with correct `@FXML` injection
4. Diagnose and fix injection failures including silent null failures

**Core Concepts:** FXML as serialized JavaFX object graph, `fx:id` as component identifier, `@FXML` annotation for injection, `FXMLLoader` injection mechanism, `initialize()` method as configuration point, constructor vs. `initialize()` lifecycle, silent null failure from `fx:id` mismatch, mapping table as verification discipline

---

## Worked Example

*Study this example before attempting Tier 1. After reading it, close it and try to recall the key steps from memory before moving on.*

**Problem:** A student has a `TableView` in their FXML file with `fx:id="appointmentTable"`. Their controller has:

```java
@FXML private TableView<Appointment> appointmentTable;
```

They run the app. It starts without errors, but the table is always empty and none of the `initialize()` setup takes effect — as if the method was never called.

Apply the `@FXML` injection lifecycle to diagnose what went wrong.

**Approach:**
1. **Check the `fx:id` value.** The FXML has `fx:id="appointmentTable"`. The controller field is named `appointmentTable`. These match — this is not the problem.
2. **Check whether the controller is set.** `FXMLLoader` only injects into a controller that is declared in the FXML file (`fx:controller="com.example.AppointmentController"`) or set programmatically. If no controller is set, `@FXML` injection never runs and `initialize()` is never called.
3. **Check the injection lifecycle.** The order is: (1) constructor, (2) `@FXML` injection, (3) `initialize()`. If `initialize()` appears to not run, either the controller is not connected to the FXML, or the setup code is in the constructor (running before injection).
4. **Apply the fix.** Verify that `fx:controller` is set in the FXML Document pane in Scene Builder. Confirm that all setup code is in `initialize()`, not the constructor.

**Answer:** The controller was not declared in the FXML file. `FXMLLoader` did not know which class to inject into, so injection and `initialize()` never ran. The fix: set `fx:controller` in Scene Builder's Document pane.

**What to notice:** Two completely different bugs produce the same symptom — table is empty and `initialize()` seems to not run. One is a missing `fx:controller`; the other is setup code in the constructor. The mapping table (Exercise 6) catches both: if you fill it out and then check the FXML, you will find the mismatch.

---

## Tier 1 — Warm-Up

*(Tests: recall, conceptual identification, true/false with explanation)*

**Exercise 1.** (Tests: recall — purpose of FXML)
What is FXML and why is it used instead of writing all JavaFX layout code in Java? Answer in 3–4 sentences. Include one concrete advantage it provides for projects using Scene Builder.

**Exercise 2.** (Tests: true/false — constructor timing)
True or False — then explain your answer in 2–3 sentences:

> "You can put UI setup code (like setting cell value factories) in the controller's constructor, as long as `@FXML` fields are declared."

**Exercise 3.** (Tests: vocabulary — fx:id and @FXML relationship)
What is `fx:id`? What is its relationship to the `@FXML`-annotated field in the controller class? What must be true about the `fx:id` value and the field name for injection to succeed?

**Exercise 4.** (Tests: recall — initialize() lifecycle)
What is the `initialize()` method? When does `FXMLLoader` call it relative to the constructor? Why does this ordering matter for UI setup code?

**Exercise 5.** (Tests: true/false — silent failure from fx:id mismatch)
True or False — then explain your answer in 2–3 sentences:

> "If you rename an `fx:id` in Scene Builder but forget to update the corresponding field name in the controller, you will get a compilation error."

---

**Exercise 5b.** (Tests: `fx:id` vs. `@FXML` vs. `initialize()` — contrastive classification)

Classify each item below as belonging to the **FXML file**, the **controller field declaration** (`@FXML`), or the **`initialize()` method**. Write one sentence justifying each classification.

- (a) `fx:id="searchField"` on a `TextField`
- (b) `@FXML private TextField searchField;`
- (c) `searchField.textProperty().addListener(...)`
- (d) `onAction="#handleSearch"` on a `Button`
- (e) `enrollButton.setDisable(true);`

*(Why this is tempting to get wrong: (d) is in the FXML file — but students often think handler wiring happens in Java. Both wiring locations exist, but FXML `onAction` is a declarative wiring in the file, while `setOnAction()` is an imperative wiring in `initialize()`.)*

---

## Tier 2 — Application

*(Tests: mapping table, error analysis, scenario diagnosis, AI interaction, initialize() implementation)*

**Exercise 6.** (Tests: mapping table — hospital appointment screen)
A hospital appointment screen has these FXML components:
- A `TableView<Appointment>` with `fx:id="appointmentTable"`
- A `TextField` with `fx:id="searchField"`
- A `Button` with `fx:id="bookButton"`
- A `Label` with `fx:id="statusLabel"`

Write the complete FXML-controller mapping table. Use these four columns:

| fx:id | Java type | Controller field name | Handler method (if applicable) |
|---|---|---|---|

Fill in all four rows. For the Button row, include a handler method name.

**Exercise 7.** (Tests: error analysis — constructor vs. initialize() NullPointerException)
A student's controller has this structure:

```java
public class AppointmentController {
    @FXML private TableView<Appointment> appointmentTable;
    @FXML private TextField searchField;

    public AppointmentController() {
        appointmentTable.setItems(model.getAppointments()); // setup in constructor
    }

    @FXML
    public void initialize() {
        searchField.textProperty().addListener(...);
    }
}
```

The application throws a `NullPointerException` on startup.

- (a) Identify the cause. Be specific: what is null, and why?
- (b) Explain why the constructor runs before injection.
- (c) Move the setup code to the correct location. Write the corrected `initialize()` method and explain why `initialize()` is the right place for this code.

**Exercise 8.** (Tests: fx:id rename scenario — silent failure diagnosis)
A student edits their library checkout screen in Scene Builder and renames the component `fx:id` from `"checkoutButton"` to `"confirmButton"` for clarity. They run the application and see no compilation error, but clicking the button does nothing.

- (a) Explain exactly what happened to the `fx:id` mapping. Where is the mismatch?
- (b) Explain why there is no compilation error despite the broken connection.
- (c) Describe the two specific places the student must update to fix this, and what each update does.

**Exercise 9.** (Tests: AI interaction — Scene Builder controller connection, missing fx:id step)
A student asks an AI: *"How do I connect a button in Scene Builder to my Java controller?"*

The AI responds:

> "In Scene Builder, select the button and in the Code section, type the method name in the 'On Action' field. Then in your controller, add the method with `@FXML public void handleButton(ActionEvent e)`. Make sure your controller class is set in the Document > Controller field."

- Identify the strongest point in the AI's response.
- Identify what the AI omitted that would cause a silent failure.
- Write the missing step in one clear sentence.
- **(d)** State the specific check you would perform after wiring the button to verify it is correctly connected — describe what action you would take in the running application and what specific result would confirm the wiring worked.

**Exercise 9b — Self-Explanation** (Tests: constructor vs. `initialize()` — why lifecycle ordering matters)

In this chapter, `@FXML` fields must be accessed in `initialize()`, not the constructor. Explain in 2–3 sentences why the ordering matters. Your explanation must use the term **"injection"** correctly and describe what value an `@FXML` field holds when the constructor runs.

**Exercise 9c — Cumulative** (Tests: FXML injection lifecycle + setter-before-show from Ch 3)

In Ch 3, the setter-before-show contract requires setting data on a screen before calling `layout.show()`. In Ch 12, the `initialize()` method runs after `@FXML` injection — it is the first safe point for any UI setup code.

A library app loads a patron detail screen via `FXMLLoader.load()`. After loading, the app calls `detailController.setPatron(patron)` and then shows the screen.

(a) In what order do these events occur: (i) constructor, (ii) `@FXML` injection, (iii) `initialize()`, (iv) `setPatron()`, (v) screen shown to user?
(b) What value does `patronNameLabel` hold when `initialize()` runs, if `setPatron()` has not been called yet?
(c) What is the correct place to display the patron's name in the label — in `initialize()` or in `setPatron()`? Justify your answer using the Ch 12 lifecycle and the Ch 3 contract.

**Exercise 10.** (Tests: implement initialize() — TableView, ComboBox, button state)
Write the complete `initialize()` method for a course enrollment controller. The controller has these `@FXML`-injected fields (already declared — do not redeclare them):
- `TableView<Course> courseTable` with a single column for `courseName`
- `ComboBox<String> semesterCombo` populated with `["Fall", "Spring", "Summer"]`
- `Button enrollButton` that should be disabled until the user selects a row in the table

Requirements:
- Set up the `courseName` column with a `PropertyValueFactory`
- Populate the `ComboBox` in `initialize()`
- Use a selection listener on `courseTable` to enable/disable `enrollButton`
- Use only the injected fields — no field initialization outside `initialize()`

---

## Tier 3 — Synthesis

*(Tests: cross-chapter integration, named prior chapters explicitly)*

**Exercise 11.** (Tests: synthesis — Ch 12 + Ch 10, FXML layer in MVC)
In Ch 10, MVC separates model, view, and controller. In Ch 12, FXML and `@FXML` injection give you a way to build the view layer in a declarative format.

Explain:
- (a) Which MVC layer does the FXML file represent?
- (b) Which MVC layer does the controller class represent?
- (c) Where does the model get connected to the controller — in the FXML file, in the constructor, or in `initialize()`? Justify your answer using injection lifecycle vocabulary from Ch 12.

A surface answer names the layers. A strong answer explains that the model connection happens in `initialize()` because injection has completed by then, and uses the constructor vs. `initialize()` lifecycle from Ch 12 to justify the timing.

**Exercise 12.** (Tests: synthesis — Ch 12 + Ch 11, FXML wiring vs. initialize() registration)
In Ch 11, handlers are registered to respond to events. In Ch 12, FXML can wire handler methods via `onAction="#methodName"`.

Compare these two approaches:
- (a) Registering a handler in `initialize()` with a lambda
- (b) Wiring a handler in FXML with `onAction="#methodName"`

For each: show the code form (in Java or FXML), describe how it fails silently, and describe when it is the better choice.

A surface answer shows both forms. A strong answer identifies the FXML silent failure (method name mismatch — no compile error) and makes a justified recommendation for each use case based on the criteria from Ch 11 and Ch 12.

---

## Tier 4 — Challenge

*(No answer key. Rubric only. Open-ended design.)*

**Exercise 13.** (Tests: controller lifecycle design — external dependency injection timing)
FXML injection happens at `FXMLLoader.load()` time, after the constructor. This means a controller has two construction phases: the Java constructor (before injection) and `initialize()` (after injection). Some controllers also need external dependencies — like a `LibraryModel` or a `UserSession` — that are not injected by FXML but must be available before `initialize()` logic runs.

Design a pattern for safely providing external dependencies to a controller that ensures:
- (a) The dependency is available when `initialize()` runs
- (b) `initialize()` does not need to check for null
- (c) The pattern is testable without running `FXMLLoader`

Describe the pattern, its constraints, and one failure mode it introduces.

**Rubric — what distinguishes a strong response:**
- Proposes a concrete mechanism (setter injection, a factory/loader wrapper, constructor injection via a custom instantiation callback, etc.) — not just "pass it somehow"
- Explains the timing constraint: the dependency must arrive either before `load()` or immediately after via a setter called before any UI interaction
- Identifies the testability benefit: the controller can be constructed and tested with a mock model without loading FXML
- Names one real failure mode introduced by the pattern (e.g., setter injection allows `initialize()` to run before the setter is called if the controller is loaded without the expected setup sequence)

---

## Full Answer Key — Tiers 1–3

### Exercise 1
FXML is an XML-based language for declaring JavaFX user interface layouts. It is used instead of writing layout code in Java to separate the visual structure of a screen from its behavior. This separation means UI designers can modify the layout in Scene Builder without touching Java code. A concrete advantage: when two students work on the same screen, one can edit the FXML layout in Scene Builder while the other writes controller logic without merge conflicts on the same Java file.

### Exercise 2
**False.** The `@FXML` fields are declared but not yet populated when the constructor runs. `FXMLLoader` calls the constructor first, then performs injection by setting the annotated fields, then calls `initialize()`. At constructor time, `appointmentTable` and all other `@FXML` fields are `null`. Calling any method on them in the constructor will throw a `NullPointerException`.

### Exercise 3
`fx:id` is an attribute in an FXML file that assigns a string identifier to a UI component. The `@FXML`-annotated field in the controller must have the same name as the `fx:id` value. `FXMLLoader` uses reflection to match each `fx:id` string to a field with that exact name — if they differ by even one character (including capitalization), injection silently fails and the field remains `null`.

### Exercise 4
`initialize()` is a lifecycle method that `FXMLLoader` calls automatically after loading the FXML and completing field injection. The ordering is: (1) constructor, (2) `@FXML` field injection, (3) `initialize()`. This ordering matters because `initialize()` is the first point at which the injected fields are non-null and safe to configure. Any setup code that references `@FXML` fields must go in `initialize()`, not the constructor.

### Exercise 5
**False.** There is no compilation error because both the `fx:id` and the `@FXML` field name are strings or identifiers that the Java compiler does not cross-check. The FXML file is not compiled — it is parsed at runtime by `FXMLLoader`. The mismatch causes a silent injection failure: the field remains `null`, and any attempt to use it at runtime throws a `NullPointerException`. This is one of the most common and hardest-to-diagnose bugs in JavaFX development.

### Exercise 6

| fx:id | Java type | Controller field name | Handler method (if applicable) |
|---|---|---|---|
| appointmentTable | `TableView<Appointment>` | `appointmentTable` | — |
| searchField | `TextField` | `searchField` | `handleSearch(KeyEvent e)` or listener in `initialize()` |
| bookButton | `Button` | `bookButton` | `handleBookAppointment(ActionEvent e)` |
| statusLabel | `Label` | `statusLabel` | — |

### Exercise 7
(a) **Cause:** `appointmentTable` is `null` when the constructor runs. `FXMLLoader` has not yet injected the `@FXML` fields — injection happens after the constructor completes. Calling `appointmentTable.setItems(...)` on a null reference throws `NullPointerException`.

(b) **Why constructor runs before injection:** `FXMLLoader` must first instantiate the controller class using its constructor (via reflection), and only then can it scan the object's fields and inject the loaded FXML components. There is no way for the constructor to run after injection within the standard Java instantiation model.

(c) **Corrected `initialize()`:**
```java
@FXML
public void initialize() {
    appointmentTable.setItems(model.getAppointments()); // moved here
    searchField.textProperty().addListener(...);
}
```
`initialize()` is the right place because `FXMLLoader` calls it only after all `@FXML` fields have been injected. By the time `initialize()` runs, `appointmentTable` is guaranteed to be non-null.

### Exercise 8
(a) The `fx:id` in the FXML file was changed to `"confirmButton"`, but the controller still has a field named `checkoutButton` (with `@FXML`). `FXMLLoader` cannot match `"confirmButton"` to any field named `confirmButton` — the field `checkoutButton` remains `null`. The `onAction` handler is also not connected because the button with the new `fx:id` has no registered handler.

(b) No compilation error occurs because `fx:id` values and `@FXML` field names are not cross-checked by the Java compiler. The FXML file is an XML resource parsed at runtime, not a compiled artifact. The mismatch is invisible at compile time.

(c) **Two places to update:**
1. In the controller: rename `@FXML private Button checkoutButton` to `@FXML private Button confirmButton` so the field name matches the new `fx:id`.
2. In all controller code that references `checkoutButton`: rename every usage to `confirmButton` so the code continues to compile and the correct field is used.

### Exercise 9
**Strongest point:** The AI correctly identifies that the method name must be entered in the 'On Action' field in Scene Builder and that a matching `@FXML`-annotated method must exist in the controller. Setting the controller class in the Document pane is also correct.

**What the AI omitted:** The AI did not mention that the button (or any other component connected via a handler) also needs an `fx:id` if the controller needs to reference it programmatically (e.g., to disable it). More critically for silent failure: the AI did not mention that if the method name in FXML's `onAction` field does not exactly match the controller method name, the handler is simply not called — no error, no warning.

**Missing step:** Verify that the method name in Scene Builder's `onAction` field exactly matches the `@FXML`-annotated method name in the controller, including capitalization, or the handler will silently fail to register.

### Exercise 10
```java
@FXML
public void initialize() {
    // Set up courseName column
    TableColumn<Course, String> nameCol = new TableColumn<>("Course Name");
    nameCol.setCellValueFactory(new PropertyValueFactory<>("courseName"));
    courseTable.getColumns().add(nameCol);

    // Populate ComboBox
    semesterCombo.getItems().addAll("Fall", "Spring", "Summer");

    // Disable enroll button until a course is selected
    enrollButton.setDisable(true);
    courseTable.getSelectionModel().selectedItemProperty().addListener(
        (obs, oldVal, newVal) -> enrollButton.setDisable(newVal == null)
    );
}
```

### Exercise 11
(a) The FXML file represents the **View** layer — it is a declarative description of the visual structure of one screen.

(b) The controller class represents the **Controller** layer — it receives events from the View and delegates to the Model.

(c) The model gets connected to the controller in **`initialize()`**, not in the constructor and not in the FXML file. The FXML file has no mechanism for injecting non-FXML objects like a `LibraryModel`. The constructor runs before `@FXML` injection, so it cannot safely reference injected components. `initialize()` runs after injection is complete, making it the first safe point for all setup — including connecting the Model (passed via a setter before `initialize()` runs, or accessed via a static registry).

> **Common error:** A surface answer says "the model is connected in the controller." A strong answer uses Ch 12 lifecycle vocabulary: constructor → injection → `initialize()`. The model cannot be wired in the constructor (injection not yet done) and cannot be wired by FXML (FXML only injects UI components). `initialize()` is the first safe point.

### Exercise 12
(a) **Lambda in `initialize()`:**
```java
@FXML
public void initialize() {
    checkoutButton.setOnAction(e -> handleCheckout());
}
```
Fails silently when: the `@FXML` field `checkoutButton` is null (due to `fx:id` mismatch) — calling `setOnAction` on null throws `NullPointerException` at runtime. Better choice when: you need to pass arguments to the handler, use a lambda that captures a local variable, or test the handler without loading FXML.

(b) **FXML `onAction` wiring:**
```xml
<Button fx:id="checkoutButton" onAction="#handleCheckout" />
```
Fails silently when: the method name `"handleCheckout"` does not exactly match the controller method name — the handler is simply not registered, no error. Better choice when: the handler is a straightforward method call with no complex wiring, and you want the connection visible in Scene Builder for design-time verification.

> **Common error:** A surface answer shows both forms. A strong answer identifies the specific silent failure for each: lambda in `initialize()` fails with `NullPointerException` if the `@FXML` field is null (fx:id mismatch); FXML `onAction` fails silently with no exception if the method name doesn't match. Different bugs, different detection strategies.

---

## Instructor Notes

**Common student errors in this module:**

1. **Setup code in the constructor:** The most frequent error, directly addressed in Exercise 7. The corrective demonstration: add a `System.out.println` to both the constructor and `initialize()`, then run the app and show the print order. Seeing `constructor` before `initialize` — and `@FXML fields are null` in the constructor — is more memorable than reading about it.

2. **Silent `fx:id` mismatch:** Exercise 5 and Exercise 8 target this. Students expect compile errors and trust the absence of errors as confirmation that things are wired correctly. Emphasize: in JavaFX, silence is not safety. The mapping table (Exercise 6) is a defensive practice — filling it out forces students to verify that every `fx:id` has a matching field name.

3. **fx:id vs. onAction confusion:** Students sometimes confuse the `fx:id` attribute (for field injection) with the `onAction` attribute (for handler registration). Both are in the Code panel in Scene Builder, which compounds the confusion. Separate the concepts explicitly: `fx:id` = "what field do I inject this into?"; `onAction` = "what method fires when this is clicked?"

**Sequencing recommendation:** The mapping table exercise (Exercise 6) should be assigned before any coding exercise. Have students fill out the table for their current project's screens as a pre-coding checklist. Students who do this have significantly fewer `NullPointerException` crashes from `fx:id` mismatches.

**Tier 3 notes:** Exercise 11 requires Ch 10 MVC vocabulary. Students who said "the FXML is the View" without explaining why should be asked: "If you delete the FXML file and rebuild the screen in Java, which MVC layer are you still building?" Exercise 12 requires Ch 11 handler vocabulary. The key discrimination is the silent failure mode — both approaches can fail silently, but for different reasons.

**Point distribution:** T1 = 5 pts each · T2 = 10 pts each · T3 = 15 pts each · T4 = 20 pts (rubric-graded)

**Bloom's distribution:**

| Tier | Bloom's Level | % of exercises |
|------|--------------|----------------|
| Tier 1 | Remember / Understand | ~25% |
| Tier 2 | Apply / Analyze | ~55% |
| Tier 3 | Analyze / Evaluate | ~12% |
| Tier 4 | Evaluate / Create | ~8% |

**Tier 4 note:** The strongest responses to Exercise 13 will describe setter injection: set the model on the controller via a setter method called immediately after `FXMLLoader.load()`, before any UI interaction. The failure mode is that the load-and-configure sequence must be followed in exactly the right order — a developer who calls `load()` without calling the setter will get a null model and a runtime crash at first interaction. Accept factory patterns (a loader utility that always sets the model) as an equally valid answer.
