# Module 10 — Event-Driven Programming with Scene Builder: Further Reading

This chapter draws a line between the model and the view and asks you to hold it — but the mechanism that makes Scene Builder usable is left implicit. How does an FXML file produced by a drag-and-drop tool connect to a Java class? How does the `@FXML` annotation inject a live `TableView` into a field that was never assigned? And why does the `TableView` update automatically when the model list changes? These are open engineering questions, not settled facts, and the answers live in a design-pattern tradition older than JavaFX itself. Closing them now gives you the foundation for Module 11's event-handler work and for every GUI framework you will encounter after this course.

Read the Key resource before the Application exercises — it closes the FXML-controller wiring gap the assessment requires. Choose one Recommended resource: pick the OpenJFX Introduction to FXML if you want the authoritative specification, or the Liang chapter if you want a complete worked example with `TableView` and model integration. The Further item is for students who want to understand the design-pattern ancestry of MVC and why professional codebases use variants — it is not required for any assessment, and you should set it aside without hesitation if the Key and Recommended tiers are still consolidating.

---

### Key

**Introduction to FXML (OpenJFX Documentation)** — OpenJFX Project, 2023 | https://openjfx.io/javadoc/21/javafx.fxml/javafx/fxml/doc-files/introduction_to_fxml.html

I included this because the chapter uses Scene Builder throughout — including in both assessments — but never explains the mechanism Scene Builder relies on: how `FXMLLoader` parses the `.fxml` file at runtime, how `@FXML` annotations inject layout nodes into your controller's fields, and how the `fx:controller` attribute in the FXML file names the Java class that will receive those injections. Without this, controller fields are `null` at `initialize()` time and every event handler silently fails — a failure mode the chapter does not warn about. The OpenJFX Introduction to FXML is the authoritative JavaFX 21 reference for this wiring. Read the "Controllers" section first (approximately 15 minutes): it covers `@FXML` injection, the `initialize()` lifecycle method, and the `fx:id` attribute that links a Scene Builder node to a named field. After that, skim "The FXML Namespace" section to understand `fx:controller`. Stop there — the remainder is reference material for advanced use cases not needed in the semester project.

> Supports: Exercise 4 — Build the library catalog view with a `BorderPane`, `TableView<Book>`, and search field wired to a Java controller class via Scene Builder and `FXMLLoader`.

---

### Recommended

**Class TableView\<S\> — JavaFX 21 API Specification** — OpenJFX Project, 2023 | https://openjfx.io/javadoc/21/javafx.controls/javafx/scene/control/TableView.html

I included this because the chapter describes the cell value factory conceptually but does not show the full `TableView` setup: how `TableColumn` type parameters work, what `setCellValueFactory` expects, and why the `items` property must hold an `ObservableList` rather than a plain `ArrayList`. The JavaFX 21 `TableView` class documentation opens with a multi-paragraph class description (before the method list) that explains all three in sequence — this preamble is the most important thing to read, and it is often skipped because readers jump to the method table. Read the class-level description in full (approximately 20 minutes); then follow the link to `TableColumn` and read its class-level description for the cell value factory contract. Pay particular attention to the paragraph on `ObservableList`: it is the clearest one-sentence account of why the `TableView` re-renders automatically when the underlying model list changes, which is the mechanical basis for the view-onto-model contract the chapter establishes as a principle. This directly supports Exercises 3 and 4.

**Introduction to Java Programming and Data Structures, 12th edition — Chapter 16: JavaFX UI Controls** — Y. Daniel Liang, 2020 | ISBN 978-0-13-517215-9 (available via institutional library)

I included this because Liang's Chapter 16 is the most complete book-length treatment of JavaFX MVC wiring at an introductory level, and it follows the same pedagogical arc as this course: domain objects first, then observable collections, then `TableView` columns, then a controller that mediates between search input and model output. Read Section 16.12 ("TableView"), which covers `PropertyValueFactory`, lambda cell value factories, and `ObservableList` construction side by side, making the choice between the two factory forms explicit rather than assumed. The section is self-contained (approximately 45 minutes) and maps directly onto Exercise 5 — translating the catalog view to your chosen domain — because Liang's example shows precisely which parts of the column definition change when the domain object changes and which parts stay fixed.

---

### Further

**"GUI Architectures"** — Martin Fowler, 2006 | https://martinfowler.com/eaaDev/uiArchs.html (stable URL, archived at https://web.archive.org/web/20240101000000*/https://martinfowler.com/eaaDev/uiArchs.html)

This is practitioner-level reading written for professional software architects, not a student text — the prose assumes you are already comfortable implementing MVC and have felt the places where it resists you. Before this resource rewards you, you should be able to classify any line of code in your semester project as a model, view, or controller responsibility without hesitation; if Exercise 1 still feels uncertain, return here after Module 11. The article traces why MVC fragments into variants in production codebases: Fowler analyzes the progression from original Smalltalk-80 MVC through Supervising Controller, Passive View, and Presentation Model, identifying the specific pressure — complex view state or automated testability — that drives each split. What the Recommended tier gives you is working knowledge of canonical MVC in JavaFX. What this article gives that the Recommended tier cannot is an understanding of why the clean three-layer model the chapter teaches begins to strain under real project conditions, and what architects choose instead. Read the introduction, "MVC," and "Supervising Controller" sections (roughly 45 minutes); the later sections are worth returning to after you have shipped a multi-screen application and started to feel the friction Fowler is naming.
