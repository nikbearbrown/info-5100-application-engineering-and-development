# Worked Exercises: Inheritance and Polymorphism

*Chapter 5 of INFO 5100 Application Engineering and Development*

> These exercises follow a research-backed sequence: full worked example → matched practice → completion problem → error-recognition → transfer → interleaved review. Each section builds on the previous. Do not skip ahead.

---

## Prerequisites

- You can define a Java class with private fields, a constructor, and getters, and you can store objects in a fixed-size array with a `count` field.
- You understand the chapter's three kinds of objects: an **entity** (a durable resource that exists independent of any user action), a **relationship** (a structural connection between entities), and a **transaction** (an event that uses entities).
- You can run the chapter's **separation test**: comment out every transaction, run `main`, and check whether the supply side (the **catalog**) still exists and is still queryable.

---

## Part A — Full Worked Example

**What this demonstrates:** Modeling the supply side as its own layer — an **entity** class, a **collection** class with a **query method**, and a **preload block** — so that the **catalog** exists and is queryable before any **transaction** runs.

**The problem:** A first draft of a library system has the catalog living *inside* the checkout. The list of books only exists when a patron checks something out:

```java
public class Patron {
    public void checkout(String isbn) {
        Book[] books = {                       // catalog built inside the transaction
            new Book("Effective Java",  "978-0-134-68599-1", true),
            new Book("Clean Code",      "978-0-132-35088-4", false)
        };
        for (Book b : books) {
            if (b.getIsbn().equals(isbn) && b.isAvailable()) {
                System.out.println("Checked out: " + b.getTitle());
            }
        }
    }
}
```

This compiles and runs for a single patron. But a librarian cannot search the catalog without performing a checkout, an administrator cannot preload books before the library opens, and two patrons do not share one catalog — they share a *fiction* of one. The supply side was never modeled; it was implied inside the demand side.

**The solution:**

**Step 1 — Name the entity and separate it from the transaction.** Decide that `Book` is a durable **entity**: it knows its title, ISBN, and availability, and it exists whether or not anyone checks anything out.

```java
public class Book {
    private String title;
    private String isbn;
    private boolean available;
    public Book(String title, String isbn, boolean available) {
        this.title = title; this.isbn = isbn; this.available = available;
    }
    public String getTitle() { return title; }
    public String getIsbn() { return isbn; }
    public boolean isAvailable() { return available; }
}
```

*Why:* An **entity** is a durable resource that exists before the session starts and after it ends. It must not be constructed on demand by a transaction.
*Check:* `Book` has no `checkout()` method and no reference to any `Patron`. It is pure supply side.

**Step 2 — Build the collection class with a query method.** Create a `Catalog` that holds books and answers queries without knowing which patron is logged in.

```java
public class Catalog {
    private Book[] books;
    private int count;
    public Catalog(int capacity) { books = new Book[capacity]; count = 0; }
    public void addBook(Book b) { books[count] = b; count++; }
    public Book findByIsbn(String isbn) {                 // query method
        for (int i = 0; i < count; i++) {
            if (books[i].getIsbn().equals(isbn)) return books[i];
        }
        return null;
    }
}
```

*Why:* The **collection class** holds multiple entities and answers queries; the **query method** (`findByIsbn`) is what the transaction layer calls to *find* resources without *owning* them.
*Check:* `Catalog` does not know whether a transaction is in progress. It has no `checkout()` method.

**Step 3 — Write the preload block before any transaction.** In `main`, build the supply side first.

```java
Catalog catalog = new Catalog(100);                       // preload block
catalog.addBook(new Book("Effective Java", "978-0-134-68599-1", true));
catalog.addBook(new Book("Clean Code",     "978-0-132-35088-4", false));
```

*Why:* The **preload block** builds the supply side before transactions begin; the catalog now exists with no patron needed to create it.
*Check:* No `Patron` object has been constructed yet, and the catalog already contains books.

**Step 4 — Have the demand side query, not create.** The transaction looks up the resource rather than constructing its own view of what exists.

```java
Book found = catalog.findByIsbn("978-0-134-68599-1");     // demand side queries supply side
if (found != null && found.isAvailable()) {
    System.out.println("Checked out: " + found.getTitle());
}
```

*Why:* This is the boundary the module enforces: the catalog does not know the patron exists; the patron knows the catalog exists and asks it for resources. The direction of the reference points from demand toward supply, never the reverse.
*Check:* If you delete this block, the catalog is unaffected — it does not depend on the transaction.

**Step 5 — Run the separation test.** Comment out every transaction line (Step 4) and run `main`. Then add a supply-only query to prove independence:

```java
public static void main(String[] args) {
    Catalog catalog = new Catalog(100);
    catalog.addBook(new Book("Effective Java", "978-0-134-68599-1", true));
    catalog.addBook(new Book("Clean Code",     "978-0-132-35088-4", false));
    Book b = catalog.findByIsbn("978-0-134-68599-1");      // works with NO patron
    System.out.println(b.getTitle() + " — available: " + b.isAvailable());
    // Patron patron = new Patron("Alice", "LIB-0042");     // demand side commented out
}
```

Expected output:

```
Effective Java — available: true
```

*Why:* If the catalog still exists and is queryable with all transactions removed, the supply side is independent. If it is empty or `main` throws, the supply side was never modeled.
*Check:* The output appears with zero transactions running — separation confirmed.

**Final answer:** Four artifacts present — the **entity** (`Book`), the **collection** (`Catalog`), the **preload block** (in `main`), and the **query method** (`findByIsbn`). The catalog is queryable before any patron exists; the separation test passes.

**What made this work:** The central concept is **supply-side modeling** — getting the entities and relationships right *before* writing any transaction. The transaction-creates-resource design is not a worse version of the same thing; it is a *different thing* that cannot let a librarian search without a checkout, cannot preload at startup, and cannot support two simultaneous transactions over one shared catalog. The naive approach (building the book array inside `Patron.checkout`) fails the separation test the instant you need the catalog from anywhere other than a single checkout flow.

**Self-explanation prompt:** In your own words, why does the *direction* of the reference (patron → catalog, never catalog → patron) determine whether the supply side is independent?

---

## Part B — Matched Practice Problem

**The problem:** An inventory program currently builds its product list inside a `PurchaseOrder.placeOrder` method — the products only exist when an order is placed. Refactor it so the supply side is modeled first. You need a `Product` **entity** (name, SKU, stock level), a `ProductCatalog` **collection class** with a `findBySku` **query method**, a **preload block** that adds at least three products in `main`, and a demand-side `placeOrder` call that *queries* the catalog rather than constructing products.

Produce: (1) the `Product` entity class, (2) the `ProductCatalog` with `addProduct` and `findBySku`, (3) the preload block, (4) the demand-side query, and (5) the **separation test** result — comment out every order and show that `findBySku` still returns a product, with expected output.

**Stuck?** Ask the chapter's diagnostic question of every line: does this line belong to the supply side (building or querying durable resources) or the demand side (a transaction using them)? Any line that *constructs* products inside `placeOrder` is the bug.

*Instructor note: No solution is provided for Part B. Build all five parts and run the separation test before moving on; the structure deliberately mirrors Part A in a new domain.*

---

## Part C — Completion Problem

**The problem:** A healthcare scheduling program builds its list of providers inside `Booking.book`. Refactor so the supply side is a first-class layer. Entities: `Provider` (name, specialty, id). Collection: `ProviderDirectory` with `findById`. Preload at least three providers; the booking queries the directory.

**Step 1 — Name the entity and separate it from the transaction.**

```java
public class Provider {
    private String id;
    private String name;
    private String specialty;
    public Provider(String id, String name, String specialty) {
        this.id = id; this.name = name; this.specialty = specialty;
    }
    public String getId() { return id; }
    public String getName() { return name; }
}
```

*Why:* `Provider` is a durable **entity** — it exists on Tuesday morning before any patient logs in. It holds no reference to any `Booking`.

**Step 2 — Build the collection class with a query method.**

```java
public class ProviderDirectory {
    private Provider[] providers;
    private int count;
    public ProviderDirectory(int capacity) { providers = new Provider[capacity]; count = 0; }
    public void addProvider(Provider p) { providers[count] = p; count++; }
    public Provider findById(String id) {                 // query method
        for (int i = 0; i < count; i++) {
            if (providers[i].getId().equals(id)) return providers[i];
        }
        return null;
    }
}
```

*Why:* The **collection class** answers queries about entities; `findById` is the **query method** the transaction layer calls without owning the provider data.

**Step 3 — [BLANK] Write the preload block in `main`, before any booking.**
*Your work here:* ________________________________________________
(Construct the directory and add at least three `Provider` objects.)

*Why (your explanation):* ________________________________________________

**Step 4 — [BLANK] Have the demand side query the directory, not create providers.**
*Your work here:* ________________________________________________
(Look up a provider by id; only proceed with the booking if it is non-null.)

*Why (your explanation):* ________________________________________________

**Step 5 — Run the separation test.** Comment out every booking line. Add a supply-only query and run:

```java
Provider p = directory.findById("PR-01");
System.out.println(p.getName() + " — specialty available");
```

Expected: the provider name prints with no booking running.
*Why:* If the directory is still queryable with all transactions removed, the supply side is independent — entity, relationship, transaction were modeled in that order.

**Final answer:** Four artifacts present — `Provider` (entity), `ProviderDirectory` (collection), the preload block (`main`), and `findById` (query method). The directory is queryable before any patient exists; the separation test passes.

**Self-explanation prompt:** Explain why preloading providers in `main` rather than constructing them inside `book` is what makes "two patients book different providers simultaneously" possible.

---

## Part D — Error-Recognition Problem

> **Use this section only after completing Parts A–C.**

A student refactors the library system from Part A. Their write-up:

**Step 1 (correct).** `Book` is the entity; it has title, ISBN, availability, and no reference to `Patron`.

**Step 2 (correct).** `Catalog` is the collection class with `addBook` and `findByIsbn`.

**Step 3 ⚠.** "To model the **relationship** between the catalog and the patron, I gave `Catalog` a field `private Patron currentPatron;` and a method `setCurrentPatron(Patron p)`. Now the catalog knows who is using it, which makes the relationship explicit. The patron and the catalog are connected, so this is good relationship modeling."

**Step 4 (correct-looking).** The student preloads books in `main`, then calls `catalog.setCurrentPatron(alice)` and `catalog.findByIsbn(...)`. It compiles, runs, and prints the right book for a single patron — a plausible-looking result.

**Your tasks:**

1. **Identify and explain the error in Step 3.** The student pointed a reference from a *supply-side* object (`Catalog`) *toward* a *transaction/demand-side* object (`Patron`). The chapter is explicit: the catalog does not know which patron is logged in. A `currentPatron` field on `Catalog` re-creates the original coupling — the supply side now depends on the demand side. This is not relationship modeling; a **relationship** in this chapter connects *entities* (e.g., `Author` ↔ `Book`), not an entity to a transaction.

2. **Write the corrected Step 3.** "The catalog holds no reference to any patron. The only relationship the supply side models is between entities — e.g., a `Book` referencing an `Author` entity. The patron→catalog direction is one-way: the demand side calls `catalog.findByIsbn(...)`; the catalog never holds a patron."

3. **State the principle violated.** The separation of supply side from demand side, verified by the **separation test**: a `currentPatron` field means the catalog can no longer be reasoned about (or queried) independent of a transaction, and two simultaneous patrons would overwrite each other's `currentPatron`.

4. **Design a test to catch this class of error.** Run the separation test *and* a concurrency thought-experiment: comment out all patron code — does `findByIsbn` still work? (It does, but the `currentPatron` field is now dead/null, signaling it never belonged on the catalog.) Then ask: if two patrons are active, whose value is in `currentPatron`? The fact that the question has no good answer reveals the misplaced reference.

**Why this error is common:** "Model the relationship by adding a reference" is correct for entity-to-entity links, so students over-apply it and point a supply-side object at a transaction — exactly the IS-A/HAS-A and coupling-direction confusion that re-introduces the original failure.

---

## Part E — Transfer Problem

**The problem (different domain — a flight-booking system, not the chapter's library/inventory/scheduling trio):** A draft builds the list of available flights inside `Reservation.reserve`. Refactor to a supply-side model: a `Flight` **entity** (flight number, origin, destination, seats available), a `FlightSchedule` **collection class** with a `findByNumber` **query method**, a **preload block** in `main`, and a demand-side `reserve` that queries the schedule. Then run the **separation test** and confirm the schedule is queryable before any reservation exists.

**Hint (use only if stuck after 10 minutes):** Map the four artifacts directly: `Flight`=entity, `FlightSchedule`=collection, the `addFlight` calls in `main`=preload, `findByNumber`=query method. The reservation must *find* a flight, never *construct* the flight list.

**Reflection prompt:** (1) What made it possible to transfer the library catalog design to flights with no new concepts? (2) Which single artifact, if you got it wrong (e.g., constructing flights inside `reserve`), would cause the separation test to fail, and why?

---

## Part F — Interleaved Review

**Problem F1.** Given a `Catalog` with a `searchByTitle` query that returns an oversized array trimmed to `found` matches, explain why this query belongs to the supply side, and run the separation test in prose: with every checkout commented out, what does `searchByTitle("Java")` return and why does that prove independence?
*Chapter this draws from: Chapter 5 (Inheritance and Polymorphism — entity, collection class, query method, separation test).*

**Problem F2.** A checkout assigns each book to a patron via a `currentPatron` field. The first checkout is correct; the second attaches the wrong patron with no exception thrown. Form a falsifiable hypothesis naming the object, field, and moment where the state goes wrong, and name the breakpoint you would set to confirm it.
*Chapter this draws from: Chapter 4 (Basics of Object-Oriented Programming Part 2 — hypothesize, isolate, test; symptom vs. root cause).*

**Problem F3 (discrimination).** A program preloads a `Catalog` correctly in `main`, but when you call `searchByTitle` twice in one run, the second call returns stale results that include a book already removed in between. A student says "the catalog isn't a first-class object — fix the supply-side model." Decide whether this is a supply-side modeling failure (Chapter 5) or a stale-state causal-diagnosis problem (Chapter 4), and justify which method to apply first.
*Note to instructor: intentionally ambiguous — the supply side IS modeled correctly (preload block present, separation test would pass), so the surface cue ("catalog," "search") points at Chapter 5, but the defect is stale in-memory state between two queries, which is a Chapter 4 hypothesize-isolate-test problem.*

**After F1–F3:** Write two sentences naming the cue that pulled you toward the wrong chapter in F3 and how the separation test (or its absence as a real defect) settled which chapter applies.

---

## Instructor Notes

**Common errors to watch for:**
- Constructing entities inside a transaction method (the original failure) and not noticing because a single-patron demo passes.
- Pointing a reference from a supply-side object toward a transaction/demand object (the Part D `currentPatron`-on-`Catalog` error).
- Confusing an entity-to-entity **relationship** (`Author` ↔ `Book`) with an entity-to-transaction link, then "modeling the relationship" in the wrong direction.

**Signs a student needs to return to the chapter:**
- The separation test fails — `main` throws or the catalog is empty when transactions are commented out.
- They cannot point to all four artifacts (entity, collection, preload, query) in their own project, or the query method is also where resources get created.

**Scaffolding adjustments:** If a student struggles with Part A, have them draw the object graph first (per the chapter's Exercise 2) and label each arrow with the field that carries the reference — a single arrow pointing from supply toward a transaction is the visible bug. If a student finishes Part F quickly, have them add a second query method (`searchByAuthor` / `findAvailable`) that uses a loop and returns a subset, and rewrite it with `ArrayList<Book>` to reason about the trade-off.

**Domain adaptation note:** Replace `Book`/`Catalog` with the student's project entities (products/`ProductCatalog`, providers/`ProviderDirectory`) — the entity → relationship → transaction order and the separation test are identical across domains; only the class and query-method names change.
