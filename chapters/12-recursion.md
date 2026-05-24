# Module 12: Recursion
*The visual editor changes the screen. The controller still has to connect to the model. That connection is yours to maintain.*

The checkout screen from Module 3 worked. You designed it by hand — panels, buttons, labels, a table — and you wrote the controller code that wired the UI events to the model objects. It ran. The `Book` reference traveled from the result panel to the checkout panel. The `Loan` was created. The confirmation showed the right data.

Now you open Scene Builder, drag in a new layout, rearrange the button placement, add a sidebar, improve the spacing. The screen looks significantly better. You run the application. The checkout button does nothing. The book table is empty. The confirmation screen shows null.

The visual editor did not break the logic. You broke the connection between the view and the controller when you rearranged the layout — silently, without a compile error, because the connection between an FXML file and a Java controller is not enforced at compile time. It is enforced at runtime, when JavaFX tries to inject the named components into the controller fields and finds that the names no longer match.

That is the failure this module is designed to prevent. Understanding why it happens is the same as understanding what Scene Builder actually does — and what it does not.

---


## EDGE Course Outline Alignment

**Module 12: Recursion**

### Learning Objectives (LOs)

- Apply recursion to address programming problems.
- Describe recursive methods.
- Develop recursive methods.

### Applied Industry Skills

- Applied Industry Skills

### Topics / Lessons / Material

- Trace Recursive Factorial
- The Fibonacci Sequence
- Characteristics of Recursion
- Computing Factorials

## What FXML Is

JavaFX applications have two representations of the same thing. The first is the object graph in memory: a `TableView` that contains `TableColumn` objects, inside a `BorderPane`, next to a `VBox` with a `Button`. These are Java objects. You can create them in code: `new TableView<>()`, `new Button("Checkout")`.

The second representation is FXML: an XML file that describes the same object graph in a declarative format. Instead of `new Button("Checkout")`, you write `<Button text="Checkout" fx:id="checkoutButton" onAction="#handleCheckout"/>`. When JavaFX loads the FXML file, it constructs the object graph from the description.

Scene Builder is an editor for FXML files. When you drag a button onto the canvas, Scene Builder writes the FXML tag for that button. When you move a component, resize a panel, or change a color, Scene Builder edits the FXML. The visual canvas and the FXML source are two views of the same file.

This is what FXML is: a serialized description of a JavaFX object graph. It is not the behavior of the application. It is not the model. It is not the controller. It is the structure of the view, expressed in a format that a visual editor can read and write.

<!-- → [SCOPE | Figure 1 | IMAGE: two-representation equivalence diagram — the same UI object graph shown twice side by side with an equivalence indicator between them; left side shows a Java code representation (nested object shapes: BorderPane containing TableView and VBox containing Button); right side shows an FXML representation (nested tag shapes: same hierarchy expressed as XML-style nested boxes); Scene Builder shown above the right side as the editor that writes the FXML; an equivalence arrow or equals sign between the two sides indicating they describe the same structure; below both sides, the three-layer model (view / controller / model) shown as three horizontal bands, with the equivalence pair sitting entirely within the view band to show that FXML authorship does not change the layer structure | CONTENT: left side: nested shape hierarchy (outer BorderPane, inner TableView and VBox, Button inside VBox); right side: same nested hierarchy expressed as tag-style nested rectangles; equivalence indicator between the two sides; Scene Builder icon/box above the right side; three-layer band diagram below showing view, controller, model — the equivalence pair labeled as "view authoring" within the top band only | EXCLUSIONS: Java syntax baked into shapes, XML attribute text, fx:id values, specific component names as text labels, UML class diagram notation, injection arrows, handler method names, network diagrams, database icons] -->

*Figure 12.1 — Two representations of the same object graph: Java code (left) and FXML (right); Scene Builder edits the FXML side; the three-layer structure is unchanged by either authoring approach*

The important thing to understand is that FXML changes the *authoring* of the view, not the *ownership* of the behavior. In hand-written JavaFX, you wrote `Button checkoutButton = new Button("Checkout")` in Java. With FXML, the button is declared in XML and injected into the controller at load time. The button exists in the same place in the object hierarchy. The controller still handles its events. The model still owns the data. Nothing about the MVC structure changes. The view is just authored differently.

---

## The Connection Mechanism: fx:id and @FXML

The connection between an FXML file and a Java controller runs through two things: an identifier in the FXML and an annotation in the controller. When they match, JavaFX makes the connection. When they do not match, JavaFX either throws a runtime exception or leaves the controller field as null — and null fields produce exactly the silent failures in the opening scenario.

In the FXML file, every component that the controller needs to reference has an `fx:id` attribute:

```xml
<TableView fx:id="bookTable" />
<Button fx:id="checkoutButton" onAction="#handleCheckout" />
<Label fx:id="statusLabel" />
```

The `fx:id` value is the name the controller will use to reference this component. The `onAction="#handleCheckout"` attribute names the method in the controller that handles the button click.

In the controller class, each referenced component has a field annotated with `@FXML`, and the field name must exactly match the `fx:id` in the FXML:

```java
public class CheckoutController {
    @FXML private TableView<Book> bookTable;
    @FXML private Button checkoutButton;
    @FXML private Label statusLabel;

    @FXML
    private void handleCheckout() {
        // handler code
    }
}
```

When JavaFX loads the FXML file, it constructs the object graph and then performs *injection*: it finds each `fx:id` in the FXML, locates the matching `@FXML` field in the controller, and sets the field to point to the constructed component. After injection, `bookTable` in the controller is the same `TableView` object that is displayed in the window. Any change you make to `bookTable` in the controller is immediately reflected in the UI.

The `@FXML` annotation tells JavaFX that this field is injection-managed. Without it, the field is not injected and stays null. The field's access modifier does not matter for injection — `private` works just as well as `public` — but the name must match exactly, including case. `bookTable` and `BookTable` are different names. JavaFX does not correct for this.

<!-- → [SCOPE | Figure 2 | IMAGE: injection connection diagram — FXML element with fx:id attribute on the left, controller field with @FXML annotation on the right, FXMLLoader as a central bridge box connecting them with arrows; a "match" path showing connected names producing a live component reference; a "mismatch" path below it showing a name change on the FXML side producing a null field and broken connection indicator on the controller side | CONTENT: left column: FXML element shape containing an fx:id label region; central bridge box: FXMLLoader; right column: controller field shape containing an @FXML label region; top path: matching name indicator on both sides, connected arrow through FXMLLoader, live reference indicator (filled/connected shape) on controller side; bottom path: mismatched name indicator (different label on FXML side vs. controller side), broken arrow through FXMLLoader, null/broken indicator (empty or X shape) on controller side | EXCLUSIONS: Java syntax baked into shapes, specific field names as text labels, XML attribute syntax, specific component types, access modifier symbols, UML notation, constructor shapes, model objects, handler method shapes] -->

*Figure 12.2 — Injection mechanism: matching fx:id and @FXML field names (top path) produce a live reference; a name mismatch (bottom path) produces a null field with no compile-time warning*

---

## The FXML-Controller Mapping Table

Because the connection between FXML and controller is not compiler-enforced, the verification discipline this module introduces is a mapping table: a written record of every `fx:id` declared in the FXML and its corresponding controller field.

The table has four columns: the `fx:id` value from the FXML, the type of the component it refers to, the `@FXML` field name in the controller (which must match), and the handler method if any. One row per connected component.

For the checkout screen:

| fx:id | Component type | Controller field | Handler |
|-------|---------------|-----------------|---------|
| `bookTable` | `TableView<Book>` | `bookTable` | — |
| `checkoutButton` | `Button` | `checkoutButton` | `handleCheckout` |
| `statusLabel` | `Label` | `statusLabel` | — |
| `cancelButton` | `Button` | `cancelButton` | `handleCancel` |

The table is the spec. When you build or modify the FXML in Scene Builder, you update the table to reflect what you added. When you write the controller, you implement every row in the table. When you run the application, you verify that every component in the table behaves as expected.

The mapping table catches the failure from the opening scenario before it manifests. When you rearranged the layout in Scene Builder, if you had deleted `checkoutButton` and recreated it as `checkout_button` — a common Scene Builder behavior when you drag-and-drop components — the table would show the mismatch: FXML declares `checkout_button`, controller declares `checkoutButton`, the names differ. You fix it before running.

| concept | Java artifact | what AI may do | what the student must verify | evidence before submission |
| --- | --- | --- | --- | --- |
| with | A concrete checkpoint for applying the chapter concept. | A concrete checkpoint for applying the chapter concept. | A concrete checkpoint for applying the chapter concept. | A concrete checkpoint for applying the chapter concept. |

---

## The initialize Method

After injection, the controller has one more step before the UI is ready for user interaction. Any setup that requires the injected components to exist — populating the table columns, setting default text in labels, configuring event listeners that are not declared in FXML — belongs in a method called `initialize`.

JavaFX calls `initialize` automatically after injection completes, before the UI is shown to the user. The contract is: by the time `initialize` returns, the UI is fully configured and ready.

```java
@FXML
private void initialize() {
    titleColumn.setCellValueFactory(
        new PropertyValueFactory<>("title")
    );
    authorColumn.setCellValueFactory(
        new PropertyValueFactory<>("author")
    );
    statusLabel.setText("Select a book to check out.");
}
```

The `initialize` method is where the controller connects the injected components to the model. The table columns are configured to read from `Book` object fields. The status label gets its initial text. If the controller needs a reference to a service object — a `LoginManager`, a `BookCatalog` — the `initialize` method is where it retrieves or receives that reference.

The common mistake is putting setup code in the controller's constructor. At construction time, injection has not happened yet. `@FXML` fields are null in the constructor. Code that reads from them will throw a `NullPointerException`. The constructor is for the controller object's own initialization. `initialize` is for UI configuration.

This is the same setter-before-show ordering discipline from Module 3, expressed in a new context. State must exist before display operations run. The mechanism is different — `initialize` instead of a setter method — but the principle is the same.

<!-- → [SCOPE | Figure 3 | IMAGE: JavaFX controller lifecycle — a vertical timeline showing four sequential phases as labeled bands: (1) constructor called — @FXML fields shown as empty/null shapes; (2) injection — FXMLLoader fills each @FXML field shape, fields transition from empty to filled; (3) initialize called — connected filled fields, setup operations run, UI ready indicator; (4) user interaction — event arrows entering from the left, handler methods responding; a distinct warning indicator beside phase 1 showing that @FXML fields are null during construction, with a "do not use here" signal; a distinct "correct location for setup" indicator beside phase 3 | CONTENT: four vertical phase bands, top to bottom; @FXML field shapes (3 of them) shown empty in phase 1, progressively filled from phase 2 onward; FXMLLoader actor shape appearing in phase 2 with injection arrows; initialize block in phase 3 with setup-operation indicators; event arrows and handler indicators in phase 4; warning shape at phase 1; checkmark or ready indicator at phase 3 | EXCLUSIONS: Java syntax, specific field names, specific component types, UML sequence diagram notation, model object shapes, handler method names baked in, specific event types, database or network shapes] -->

*Figure 12.3 — Controller lifecycle: @FXML fields are null during construction, filled after injection, available in initialize — setup code belongs in phase 3, not phase 1*

---

## What Scene Builder Changes and What It Does Not

Scene Builder changes the authoring experience for the view. It does not change anything about the controller, the model, or the boundary between them.

Before Scene Builder, you wrote layout code in Java:

```java
BorderPane root = new BorderPane();
TableView<Book> bookTable = new TableView<>();
Button checkoutButton = new Button("Checkout");
VBox sidebar = new VBox(10, checkoutButton, statusLabel);
root.setCenter(bookTable);
root.setRight(sidebar);
```

With Scene Builder, you drag and drop to produce the same structure, which gets serialized into FXML. The FXML is loaded at runtime and produces the same object graph. The controller code is identical either way.

What this means practically: the skills from every previous module still apply, unchanged. The `Book` object that travels through the flow in Module 3 still travels the same way. The `LoginManager` from Module 6 is still called the same way. The collection sorted in Module 9 is still sorted the same way. Scene Builder is a better tool for editing the view. It does not change what the view does.

| fx:id | JavaFX component type | @FXML controller field | event handler method | verified (yes |
| --- | --- | --- | --- | --- |
| template — | A concrete checkpoint for applying the chapter concept. | A concrete checkpoint for applying the chapter concept. | A concrete checkpoint for applying the chapter concept. | A concrete checkpoint for applying the chapter concept. |

The risk Scene Builder introduces is cosmetic: it is possible to rearrange, rename, or accidentally delete components without the Java code signaling an error. The mapping table prevents this from becoming invisible damage. Every `fx:id` is tracked. Every controller field is traced. Every handler is named.

---

## Reconnecting the Module 3 Flow

The assignment for this module is to take the two-screen flow from Module 3 — search panel and checkout panel, or their equivalents in your domain — and redesign at least one of those screens in Scene Builder. The redesign may improve the layout, add components, rearrange the visual hierarchy. What must not change is the connection to the model.

Concretely: the `Book` object that was passed to the checkout panel via a setter method in Module 3 must still be passed the same way. The `@FXML`-injected `bookTable` field is a different component than the `JPanel` table from the Swing-era flow, but its role is the same: it displays the `Book` objects the model contains. The handler that responds to a selection in the table is a different method signature from the Module 3 `ActionListener`, but it performs the same action: retrieve the selected `Book` and pass it to the next screen.

The verification question for this module is an extension of the Module 3 flow table. You have an FXML component. That component has an `fx:id`. That `fx:id` is injected into a controller field. That field is used in a handler. That handler calls a method on a model object. The chain must be traceable, end to end, for every interactive component in the redesigned screen.

<!-- → [SCOPE | Figure 4 | IMAGE: end-to-end traceability chain — a single horizontal chain of five linked nodes showing the complete path from FXML component to model call: (1) FXML component with fx:id; (2) injection arrow; (3) @FXML controller field; (4) handler method; (5) model object method call; each node is a distinct labeled shape; a downward "evidence" indicator below each node showing what the mapping table captures at that position; below the chain, a broken-chain version of the same five nodes where the connection between nodes 3 and 4 is severed, showing a display-only handler that updates a label but makes no model call — the "handler that looks right but is wrong" failure | CONTENT: top row: five nodes (FXML component, injection arrow, controller field, handler, model call) connected in a left-to-right chain; downward evidence indicators below each node; bottom row: same five nodes, with nodes 4 and 5 disconnected — handler present but model call absent — with a distinct broken/absent indicator at the gap | EXCLUSIONS: Java syntax, specific field names, specific model object names, UML sequence diagram notation, database or network shapes, authentication logic, specific component types, access modifier symbols, constructor shapes] -->

*Figure 12.4 — End-to-end traceability chain: every interactive component must be traceable from fx:id through injection, controller field, handler, to model call; a handler that terminates at node 4 without reaching node 5 is display code, not behavior*

If you cannot trace a component from `fx:id` to model call, you have a handler that acts on the view without acting on the model. That handler is display code masquerading as behavior. It will pass a visual test — the button responds, the label changes — and fail a behavior test: the `Book` was not actually selected, the `Loan` was not created, the state the confirmation screen expects does not exist.

---

## What AI Can and Cannot Do Here

The legitimate use of AI in this module is narrow and specific: AI can generate controller stubs from a provided FXML file. You paste the FXML, AI reads the `fx:id` attributes and `onAction` references, and produces a controller class with the corresponding `@FXML` fields and empty handler method signatures. This is mechanical work that AI does well.

What AI cannot do is design the FXML. The FXML should describe the interface your Module 3 flow requires: the screens the user needs, the components those screens need, the `fx:id` attributes that will allow the controller to reach each component. That design is yours. It derives from the flow table you built in Module 3, the model objects you built in earlier modules, and the specific interactions your domain requires. AI does not have that context.

The phase gate follows: you provide the FXML, AI provides the controller stubs. Not the other way around.

If you give AI a description of your interface and ask it to generate the FXML, you will get a plausible FXML for a plausible interface that bears some resemblance to what you described. The `fx:id` values will be generic. The handlers will be named for common operations. Nothing will be traced to your actual model objects, your actual flow requirements, or the specific field names your domain uses. You will spend more time fixing the generated FXML than you would have spent writing it.

Here is the prompt that keeps the boundary where it belongs:

```text
I am working on Module 12: Recursion in INFO 5100.
My domain is [library / inventory / scheduling].
Here is the FXML I designed in Scene Builder: [paste FXML].
Generate a controller stub: @FXML fields for every fx:id, and empty
handler method signatures for every onAction reference.
Do not implement the handlers. Do not add new fx:id attributes.
Do not change the FXML structure.
```

After receiving the stub, verify it against your mapping table: every row in the table should correspond to a field or method in the stub, and the names should match exactly.

---

## The Inventory and Scheduling Shape

The FXML-controller pattern applies identically across all three domains. Only the component types and handler semantics differ.

In an inventory system, the redesigned screen might be the stock adjustment form: a `TextField` for quantity, a `ComboBox` for adjustment type (restock, sale, write-off), a `Button` to submit. The FXML declares each component with an `fx:id`. The controller injects them, validates the input in `initialize` or in the handler, and calls the appropriate method on the `Inventory` model. The model updates the stock record. The view reflects the new state.

In a healthcare scheduling application, the redesigned screen might be the appointment booking form: a `DatePicker`, a `ComboBox` of available providers, a `ListView` of available time slots, a `Button` to confirm. The FXML structure is different. The `fx:id` values are different. The controller logic calls methods on the `Schedule` model. The discipline is the same: every component is in the mapping table, every `@FXML` field is traced to a model call, every handler is verified against the expected state transition.

The mapping table works as a checklist in all three cases. Complete the table before writing the controller. Trace every row when the application runs.

---

## The Disconnect Failure, Named

Let me name the failure this module is designed to prevent with enough precision that you will recognize it.

You redesign the checkout screen in Scene Builder. The redesign adds a `TextField` for a patron search, changes the checkout button from `checkoutButton` to `checkout_btn` to fit a new naming convention you found in an online example, and removes the status label because the new layout does not need it. You save the FXML. You run the application.

The application runs. The new layout appears. You select a book and click the checkout button. Nothing happens. No exception in the log. No error message. The button just does not respond.

What happened: `checkoutButton` in the controller is now null. The `@FXML` annotation looked for an `fx:id` named `checkoutButton` in the FXML. It found `checkout_btn` instead. JavaFX did not throw an error — the field simply stayed null. The click handler is registered on the `Button` object that `checkoutButton` should point to. But `checkoutButton` is null. There is no object to register the handler on. The click has no effect.

The fix is one rename. But finding it without a mapping table requires reading the FXML and controller simultaneously, comparing every `fx:id` to every `@FXML` field name. With a mapping table, the mismatch is visible in the table before you run the application. The `fx:id` column says `checkout_btn`. The controller field column says `checkoutButton`. The names differ. You fix it.

| scenario | what changed in FXML | what stayed the same in controller | runtime result (exception or null field) | what the mapping table would have shown |
| --- | --- | --- | --- | --- |
| fx:id renamed, component deleted and recreated, onAction handler renamed, component type changed from Button to MenuItem | this is the reference for diagnosing silent connection failures | A concrete checkpoint for applying the chapter concept. | A concrete checkpoint for applying the chapter concept. | A concrete checkpoint for applying the chapter concept. |

---

## What This Module Does Not Settle

We have moved the view into FXML, connected FXML to controllers via injection, established the mapping table as the verification discipline, and reconnected the Module 3 flow in the new authoring context. We have not addressed testing: how do you prove the behavior still works after changes to the view?

The bridge question is: the interface is connected. How do you prove the behavior still works after changes?

The next module addresses this. Testing a JavaFX controller requires separating the behavior from the view more completely than this module has required — extracting the model logic into classes that can be exercised without constructing a UI, and testing those classes directly. The discipline of keeping the controller thin and the model complete is what makes that extraction possible. Modules that allow business logic to migrate into handlers produce controllers that cannot be tested without rendering the full UI. This module's mapping table is the start of the answer: every handler should be traceable to a single model call.

---

## Lab: Scene Builder Redesign

Redesign at least one screen from your Module 3 flow using Scene Builder. Before opening Scene Builder, update your Module 3 flow table to reflect any changes the redesign requires. Before writing any controller code, complete the FXML-controller mapping table for the redesigned screen: `fx:id`, component type, controller field, handler method, one row per injected component.

The implementation must demonstrate that every `@FXML` field is injected successfully, that `initialize` runs without null-pointer errors, and that at least one handler performs a traceable model call — not just a UI update. The evidence is the mapping table, the running application, and a one-sentence trace for the primary handler: "Button X fires handler Y which calls method Z on object W."

If you used AI to generate the controller stub from your FXML, include the FXML you provided and verify the stub against your mapping table before adding any implementation.

---

## Exercises

**Warm-up**

1. Open your Module 3 checkout screen's FXML (or reconstruct a minimal version from memory) and complete the FXML-controller mapping table for it: `fx:id`, component type, controller field, handler method. Then identify any component you interact with in the UI that does not appear in the table, and explain what that omission means — is it wired differently, or is it untraceable? *(Tests: mapping table construction; identification of all injected components.)*

2. Write the `initialize` method for a controller that manages a book checkout screen with a `TableView<Book>` named `bookTable`, a `Label` named `statusLabel`, and a `Button` named `checkoutButton`. The `initialize` method should set up the table's title column, set the status label's initial text, and disable the checkout button until a row is selected. Do not put any of this in the constructor. *(Tests: initialize contract; injection lifecycle ordering; the constructor-vs-initialize distinction.)*

**Application**

3. A classmate redesigns their search screen in Scene Builder and renames the results table from `resultTable` to `results_table` to match a naming convention they found online. The controller still declares `@FXML private TableView<Book> resultTable`. Describe exactly what happens at runtime: which object is null, when it becomes null, what symptom the user sees, and what the mapping table would have shown if it had been updated at the time of the rename. *(Tests: null-injection failure mode; fx:id-to-field name matching; mapping table as pre-run verification.)*

4. A handler method in the checkout controller updates the `statusLabel` text and returns. The user sees the label change. The lab is submitted. At the review, the instructor asks: "Which model object did this handler call?" The student cannot answer. Using this module's traceability requirement, explain what is wrong with the handler, what a correct handler looks like, and how the one-sentence trace format ("Button X fires handler Y which calls method Z on object W") would have revealed the problem before submission. *(Tests: handler-to-model-call traceability; display code vs. behavior; lab evidence standard.)*

5. You ask AI to generate a controller stub from your FXML and receive a class with `@FXML private Button confirmBtn` — but your FXML declares `fx:id="confirmButton"`. Apply the AI boundary rule: is this a scaffolding error you should fix, or a design decision the AI made that you should evaluate? Name the exact consequence if you use the stub unchanged, and write the one-character-level fix. *(Tests: AI stub verification against mapping table; fx:id exact-match rule; AI boundary applied to generated code.)*

**Synthesis**

6. Translate the checkout screen's FXML-controller mapping table into your own domain (inventory stock adjustment form or healthcare appointment booking form). Name every interactive component, assign an `fx:id`, identify the controller field, and name the handler. Then write the `initialize` method that configures any component that requires setup before the user interacts with it. *(Tests: domain transfer; complete mapping table; initialize construction in a new domain.)*

7. The mapping table for your redesigned screen has a row for `cancelButton` with handler `handleCancel`. The `handleCancel` method currently calls `stage.close()` — it closes the window. Using the Module 3 flow table and this module's traceability requirement, argue whether this handler is acceptable. What model call, if any, should `handleCancel` make before closing? If the flow table says the user can return to the search screen from checkout, what additional steps does `handleCancel` require? *(Tests: handler-to-model traceability; backward navigation state management from Module 3; the flow table as the spec that handlers must satisfy.)*

**Challenge**

8. The `initialize` method is called once, when the FXML is loaded. In a single-window application where the checkout screen is shown and hidden repeatedly (using `setVisible` rather than loading a new FXML), `initialize` does not re-run between sessions. Describe the problem this creates: what state from a previous session might be visible to the next user, which `@FXML`-injected component is most likely to carry stale state, and how you would design a `reset()` method — separate from `initialize` — that clears the screen for a new session. Identify where in the navigation flow `reset()` should be called and by whom. *(Open-ended; anticipates session management and multi-user state isolation patterns introduced in the testing and hardening modules.)*

---

- **Scene Builder** — a visual editor for JavaFX interfaces that writes FXML files. It changes how the view is authored. It does not change the controller, the model, or the connection rules between them.
- **FXML** — an XML format for describing a JavaFX object graph declaratively. Loaded at runtime by `FXMLLoader`, which constructs the described objects and performs injection into the controller.
- **fx:id** — the attribute in an FXML element that names the component for injection. Must exactly match the `@FXML` field name in the controller. A mismatch produces a null field or runtime exception, not a compile error.
- **@FXML** — the annotation that marks a controller field or method as injection-managed. After FXML loading, fields annotated with `@FXML` point to the constructed components named by their matching `fx:id` attributes.
- **controller** — the Java class that receives injected UI components and implements the handlers that connect user actions to model calls. Declared in the FXML's root element as `fx:controller`.
- **injection** — the process by which `FXMLLoader` sets the `@FXML` fields in the controller to point to the constructed components. Happens after the object graph is built, before `initialize` is called.
- **layout** — the visual structure of a screen, described in FXML as a hierarchy of container and component nodes. Scene Builder edits the layout. The controller is independent of layout decisions.

---

## Assessments

| Assessment | Type | Credit status | Group or Individual | Alignment note |
| --- | --- | --- | --- | --- |
| Discussion - Pros and Cons of Using Recursion | Community | For-Credit | Individual | Compare recursive and iterative solutions. |
| Optional Exercise: Recursion | Practice | For-Credit | Individual | Write and trace a recursive method. |
| Quiz - Recursion | Summative | For-Credit | Individual | Assess base cases, recursive calls, and trace reasoning. |
| Reflection | Reflection | NDNC | Individual | Reflect on when recursion clarifies or complicates a solution. |

*Please label your assignments as Group or Individual.*


## Further Reading

- OpenJFX documentation: authoritative source for FXML syntax, `FXMLLoader`, `@FXML` injection mechanics, and Scene Builder integration.
- *Java Language Specification* and the Java SE API documentation: for JavaFX component types and their event models.
- Robins, Rountree, and Rountree, "Learning and Teaching Programming": research on the connection-tracing difficulties this module's mapping table addresses.
- Peng et al. and Vaithilingam et al.: empirical work on AI coding assistance; the FXML-first phase gate is grounded in their findings on the cost of unverified structural delegation.
