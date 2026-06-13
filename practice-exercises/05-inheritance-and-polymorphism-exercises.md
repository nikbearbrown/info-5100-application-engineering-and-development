# Module 5 — Inheritance and Polymorphism: Exercises
**Topic:** Supply-side modeling, entities/relationships/transactions, catalog design
**Learning Objectives:**
1. Design supply-side object models with entities and relationships
2. Implement catalog objects with query methods
3. Separate supply-side from transaction logic
4. Verify supply-side independence

---

## Tier 1: Warm-up

**1. Recall** *(Tests: LO1 — three types of objects)*

What are the three types of objects in the supply-side model? Define entity, relationship, and transaction. Give one example of each from a library system.

---

**2. True/False + Explain** *(Tests: LO4 — supply-side independence)*

> "A Catalog object should be created when the first checkout transaction occurs, because the catalog only exists to support checkouts."

State whether this is true or false. Explain your reasoning in two to three sentences.

---

**3. Vocabulary** *(Tests: LO4 — supply-side independence test)*

What is the supply-side independence test? How do you perform it, and what does a passing result tell you about your design?

---

**4. Query methods** *(Tests: LO2 — query vs. transaction methods)*

What distinguishes a query method from a transaction method? Give one example of each in a library catalog.

---

**5. True/False + Explain** *(Tests: LO1 — relationship ownership)*

> "In a library system, the relationship between Author and Book should be stored inside the checkout transaction object, because that's when you need to display the author's name."

State whether this is true or false. Explain your reasoning in two to three sentences.

---

## Tier 2: Application

**6. Scenario** *(Tests: LO1, LO4 — supply-side model design)*

You are building a hospital appointment system. Identify:
- (a) Three entities and their key fields
- (b) Two relationships and which entities they connect
- (c) One transaction and what state it changes

Then verify your model passes the supply-side independence test: can the entity and relationship layer exist and be queried without any transactions running?

---

**7. Error Analysis** *(Tests: LO1, LO3 — entity reference vs. data copy)*

A student builds a course registration system. Their `Enrollment` class (the transaction) stores a copy of the course details directly as fields:

```java
public class Enrollment {
    String studentId;
    String courseName;      // copied from Course
    String instructorName;  // copied from Course
    String roomNumber;      // copied from Course
    Date enrollmentDate;
}
```

- (a) Identify the design problem.
- (b) What breaks when a course's room number changes after students have already enrolled?
- (c) Redesign the `Enrollment` class to use an entity reference instead.

---

**8. Catalog Design** *(Tests: LO2 — catalog with query methods)*

Design a `Catalog` class for a hospital appointment system. Your catalog must:
- (a) Store `Doctor` entities
- (b) Support a `findBySpecialty(String specialty)` query
- (c) Support a `findById(String doctorId)` query

Write the class signature, field declarations, and method signatures (not full implementations). Explain why each query method is a supply-side method, not a transaction method.

---

**9. AI Interaction** *(Tests: LO1, LO3 — supply-side model)*

A student asked an AI to design the object model for a library. The AI produced:

> "Create a `CheckoutSystem` class that contains everything: a books array, a patrons array, and a `checkout()` method that takes a book title and patron name as strings and creates a checkout record."

- Identify the **strongest point** in the AI's response.
- Identify the **most significant design problem** relative to the supply-side model.
- Write a **two-sentence correction** describing what the AI missed.

---

**10. Preloading** *(Tests: LO3, LO4 — preloading before transactions)*

A student's library system creates `Book` objects inside the `checkout()` method, only when a user requests a book. Explain:
- (a) Why this violates the supply-side model
- (b) What breaks when a second user checks out the same book (or when the same ISBN is checked out twice)
- (c) Where `Book` objects should be created instead

---

## Tier 3: Synthesis

**11. Synthesis (Ch 5 + Ch 3)** *(Tests: LO1, LO3 + Ch 3 screen state ownership)*

In Ch 3, you learned that screens should not own state — state lives in objects that are passed between screens. In Ch 5, you learned that supply-side entities should exist before transactions.

Apply both principles to a 3-screen hospital appointment app: `Search` → `BookAppointment` → `Confirmation`.

For each screen:
- (a) Identify which supply-side entities it displays
- (b) Confirm it does not own that entity (explain where the entity actually lives)
- (c) Describe how the entity travels from the catalog to the screen

**What distinguishes a surface answer:**
- Uses entity vocabulary from Ch 5 and state-ownership vocabulary from Ch 3
- Traces the entity through all three screens end to end
- Correctly identifies that the catalog is supply-side, screens are demand-side, and screens only hold references they were given

---

**12. Synthesis (Ch 5 + Ch 1)** *(Tests: LO1, LO3 + Ch 1 object model)*

The object model from Ch 1 says behavior belongs in the object that owns the relevant state. The supply-side model from Ch 5 says entities are independent of transactions.

Apply both principles to this design question: should a `Book` entity have a `checkout()` method, or should checkout logic live in a separate `Transaction` class?

Defend your answer using vocabulary from both chapters.

**What distinguishes a surface answer:**
- Applies the state-ownership principle from Ch 1 correctly (identifies what state `checkout()` would need)
- Uses supply/demand separation from Ch 5 (entities are supply-side; transactions are demand-side)
- Makes a defensible design choice with specific reasoning, not just assertion

---

## Tier 4: Challenge

**13. Capstone — Two-Way Author/Book Query** *(No answer key — rubric only)*

A library system's supply side contains `Book` entities and `Author` entities, where one author can have many books. Design how you would implement a two-way query: given an `Author`, find all their `Book`s; given a `Book`, find its `Author`.

Describe:
- (a) Where you store each relationship (in `Author`, in `Book`, or in a separate object)
- (b) What data structure you use for each direction
- (c) How you ensure both directions stay consistent when a new book is added to the catalog
- (d) What specifically breaks if you store `authorName` as a `String` inside `Book` instead of a reference to an `Author` object

There is no single correct design — justify your choices.

**Rubric — a strong response will:**
- Propose a concrete storage mechanism for each query direction (not vague)
- Address both query directions explicitly
- Identify the specific consistency problem and how the design prevents it
- Explain the concrete failure mode that arises from String-copy vs. reference-link (not just "it's bad practice")

---

## Full Answer Key (Tiers 1–3)

### Tier 1 Answers

**1.**
- **Entity:** A persistent, identifiable domain object with an independent existence. Example: a `Book` with fields `isbn`, `title`, `authorId`.
- **Relationship:** An object that records a connection between two entities. Example: a `BookAuthor` link that connects a `Book` to its `Author`.
- **Transaction:** An object that records an event that changes state at a point in time. Example: a `CheckoutRecord` that records which `Patron` checked out which `Book` on which date.

**2. False.** The catalog — and the entities it holds — should be created when the application starts, before any transactions occur. The supply side exists independently of any demand-side activity. A catalog that only exists when a transaction is in progress cannot answer queries like "what books do we have?" and would lose all data when the transaction ends.

**3.** The supply-side independence test asks: can I run queries against the entity and relationship layer without any transactions having occurred? To perform it, construct your catalog and entities, populate them with sample data, and call your query methods — without calling any transaction methods. A passing result means your entities, relationships, and catalog are correctly separated from transaction logic and have no hidden dependency on transactions being initialized first.

**4.** A query method reads from the supply-side model and returns data without changing any state. A transaction method records a business event and changes state. Example of a query method: `catalog.findByIsbn("978-0-13-468599-1")` returns a `Book` without modifying anything. Example of a transaction method: `checkout(book, patron)` creates a `CheckoutRecord` and marks the book as unavailable.

**5. False.** The Author-Book relationship is a supply-side relationship between two entities. It exists regardless of whether any checkouts occur. Storing it inside a checkout transaction would mean the relationship only "exists" during a transaction, making it impossible to query author information without a checkout in progress.

---

### Tier 2 Answers

**6.**
- (a) Entities: `Doctor` (fields: `doctorId`, `name`, `specialty`), `Patient` (fields: `patientId`, `name`, `dateOfBirth`), `TimeSlot` (fields: `slotId`, `date`, `time`, `durationMinutes`).
- (b) Relationships: `DoctorSchedule` connects `Doctor` to `TimeSlot` (one doctor has many time slots); `PatientHistory` connects `Patient` to `Doctor` (a patient may have a preferred or past doctor).
- (c) Transaction: `Appointment` — records that a `Patient` booked a specific `TimeSlot` with a specific `Doctor`; changes the `TimeSlot` status from available to booked.
- Supply-side independence: Yes — you can construct the catalog with doctors and time slots and query available slots by specialty without any appointments having been created. The entities answer queries independently.

**7.**
- (a) The `Enrollment` transaction stores copies of supply-side entity data as plain strings rather than holding a reference to the `Course` entity.
- (b) When the course's room number changes, every existing `Enrollment` record still holds the old room number string. There is no way to update all enrollments to reflect the change without finding and rewriting each one. The single source of truth is lost.
- (c) Redesigned class:
```java
public class Enrollment {
    String studentId;
    Course course;          // reference to the Course entity
    Date enrollmentDate;
}
```
The course name, instructor, and room number are obtained by calling `enrollment.course.getName()`, etc., so changes to the `Course` entity are automatically reflected everywhere it is referenced.

**8.**
```java
public class DoctorCatalog {
    private List<Doctor> doctors;

    public DoctorCatalog() { ... }

    public List<Doctor> findBySpecialty(String specialty) { ... }
    public Doctor findById(String doctorId) { ... }
}
```
Both methods are supply-side because they only read from the entity collection and return results — they do not create appointments, modify doctor state, or record any event. They can be called before any appointment transaction exists.

**9.**
- **Strongest point:** The AI correctly identified that the system needs books, patrons, and a checkout operation — the right domain objects are present.
- **Most significant design problem:** Lumping books, patrons, and checkout logic into a single `CheckoutSystem` class merges the supply side (books and patrons) with transaction logic into one monolithic object. Books and patrons are entities that should exist independently in a catalog, queryable without any checkout in progress.
- **Correction:** Books and patrons are supply-side entities that should live in separate catalog objects, constructed and populated before any transactions occur. The `checkout()` method belongs in a transaction layer that receives entity references, not in a class that also stores the entities.

**10.**
- (a) Supply-side objects — books — must exist before any transaction requests them. Creating a `Book` inside `checkout()` means the supply side depends on the demand side, inverting the correct dependency direction. It also means the catalog cannot be queried independently.
- (b) If two checkouts reference the same ISBN, two separate `Book` objects are created with the same ISBN. They are distinct Java objects, so changes to one (marking it checked out) do not affect the other. The system has two inconsistent representations of one real book.
- (c) `Book` objects should be created during application startup (or catalog loading), stored in a `Catalog`, and retrieved from the catalog by ISBN when needed. The `checkout()` method should call `catalog.findByIsbn(...)` to get the existing object, not construct a new one.

---

### Tier 3 Answers

**11.**
- **Search screen:** Displays a list of `Doctor` entities (supply-side). The screen does not own the doctors — they live in the `DoctorCatalog`. The screen holds only the list of results returned by `catalog.findBySpecialty(...)` and a reference to the selected `Doctor`.
- **BookAppointment screen:** Displays the selected `Doctor` entity and available `TimeSlot` entities (both supply-side). The screen does not own either — it received the `Doctor` reference via `setDoctor(...)` from the Search screen, and it queries the catalog for available slots. It owns only the user's input (the desired appointment time) until that input becomes a transaction.
- **Confirmation screen:** Displays the `Doctor`, `Patient`, and `TimeSlot` entities involved in the booked appointment. None of these are owned by the screen — they were passed in via setter calls before the screen was shown. The entity traveled from catalog → Search screen (via query) → BookAppointment screen (via setter) → Confirmation screen (via setter), with the same object references at every step.

**12.**
A `Book` entity owns state about what the book is — its title, ISBN, author, and publication data. It does not own state about who has it or when it was borrowed. The `checkout()` behavior requires state that a `Book` does not own: the `Patron` reference, the checkout date, and the due date. Placing `checkout()` inside `Book` would force the `Book` to hold patron data, violating Ch 1's principle that behavior belongs in the object that owns the relevant state.

The supply-side model from Ch 5 reinforces this: `Book` is a supply-side entity that exists independently of any transaction. Adding `checkout()` to `Book` would make the entity depend on transaction state, destroying supply-side independence — the `Book` could no longer be queried or reasoned about without an active checkout in progress. The correct design places `checkout()` in a `CheckoutTransaction` class (or service) that receives references to the `Book` and `Patron` entities it needs. The entities remain clean, independently queryable supply-side objects.

---

## Instructor Notes

- **Exercise 7** is the most important error analysis item. The string-copy-vs-reference-link problem is a direct application of Ch 2 reference semantics to supply-side design. Students who redesign using a `Course` reference without explaining *why* the copy breaks have addressed the symptom. Look for the "single source of truth" reasoning.
- **Exercise 9 (AI Interaction)** targets a common AI output pattern: generating a God Object that merges all concerns. Students should identify that the AI's answer is not wrong about what exists, but wrong about how it is organized. Award partial credit for identifying the monolithic structure even without naming supply/demand separation explicitly.
- **Exercise 10 (Preloading)** is the key correctness item for LO3. Students who say "it works fine because you can just create the book each time" have not understood the identity problem — two distinct Java objects representing the same real book are inconsistent by definition.
- **Exercise 11 (Synthesis)** is the highest-difficulty Tier 3 item. It requires applying vocabulary from two chapters simultaneously. Weak answers describe the screens correctly but fail to explain *where* the entity lives between screens (in the catalog, not floating in memory).
- **Exercise 13 (Challenge)** has no single correct design. Common strong answers: store a `List<Book>` in `Author` for the author-to-books direction, and a single `Author` reference in `Book` for the reverse; enforce consistency by always using a factory method or the catalog's `addBook(book, author)` method. Common weak answers store only one direction and handle the other with a full scan. Both are defensible — evaluate the reasoning.
- Recommended sequence: Tier 1 as pre-class check, Tier 2 items 6–8 in lab (pair or individual), items 9–10 as written individual work, Tier 3 as take-home essay, Tier 4 as optional extension for students ready to design before being taught the canonical solution.
