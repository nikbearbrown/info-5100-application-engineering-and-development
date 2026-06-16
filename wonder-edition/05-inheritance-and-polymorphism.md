# Module 5 — Inheritance and Polymorphism: Wonder Edition
## Companion Chapter

> **Wonder Edition:** Read this alongside the chapter, not instead of it.

> **Content Note:** The chapter file is titled "Inheritance and Polymorphism" and lists those topics in its learning objectives. However, the body of the chapter teaches supply-side modeling — the design discipline of separating entity and relationship objects from transaction objects, and building the resource layer before any user-driven code runs. This Wonder Edition follows the actual content of the chapter.

---

## The Strange Question

A program runs. It takes a checkout request from a patron. It returns the right book. The test passes.

Then someone asks: can a librarian search the catalog before any patron logs in?

The code stops working. The catalog is empty. No books exist until a patron tries to check one out.

No syntax changed. No logic was wrong. The program worked exactly as designed.

How did a program that passed every test fail to model the most basic fact about libraries?

---

## First Intuition

The natural way to build software is to follow the user.

A patron arrives. The patron searches. The patron checks out. So: write a `Patron` class, give it a `search` method, and inside that method find the books. This approach feels responsive. It matches what the user experiences. It produces output immediately.

When someone builds a checkout method that also creates books, the design feels complete. The method works end to end. The test passes green.

The error is invisible because the program does exactly what was asked of it. No compiler complains. No exception fires. The catalog exists — it just only exists during a checkout.

> **► Planning prompt:** Before reading on, write one sentence predicting what breaks when a second kind of user — say, a librarian — needs to search the same catalog. What does the search method depend on that the librarian does not have? Write the prediction before continuing.

---

## The Surprise

But here is what the working program cannot do.

Comment out every patron. Comment out every checkout. Run `main`.

The catalog is gone. There are no books. `searchByTitle` returns nothing, or crashes, because the books were never put anywhere permanent. They were constructed inside the checkout flow and exist only while that flow runs.

The program modeled a transaction. It did not model a library.

A real library catalog sits on a shelf before the building opens. It exists on a Tuesday morning when no patron has arrived, when no checkout is in progress, when no screen is displaying anything. The catalog is a durable fact. The checkout is a temporary event that touches that fact.

> **► Monitoring prompt:** Before reading on, name the assumption the design made that produced this failure. What did the program treat as ephemeral that the domain says is durable? What else in the program might share that assumption without it being obvious?

The mismatch between the running program and the real domain sits unresolved. The code is correct. The model is wrong. These are different problems.

---

## The Hidden Structure

Therefore, the domain has two fundamentally different kinds of objects, and a design that conflates them will produce exactly this failure.

Some objects are durable. A book. A catalog. A supplier. A physician's schedule. These objects exist before any user action and persist after it. Their state can change, but the object itself is not created by user demand. It precedes demand.

Other objects are events. A checkout. A purchase order. A booking. These objects exist because a user did something. They record what changed, who requested it, and when. They depend on the durable objects — a checkout without a pre-existing book is not a transaction. It is an error.

> "It is tempting to think that modeling the user's path through the system is the same as modeling the system. But the user's path only touches the demand side — the events, the transactions, the requests. The correct model holds that the supply side — the entities that exist before any request — must be built first, as its own layer, independently of any user action. The key distinction is that durable entities survive the removal of all transactions, while transaction objects do not: if commenting out every checkout empties the catalog, the supply side was never really modeled."

**Code Trace — the separation test:**

```java
// Supply side built first — no patron exists yet
Catalog catalog = new Catalog(100);
catalog.addBook(new Book("Effective Java", "Joshua Bloch",
                         "978-0-134-68599-1", true));
catalog.addBook(new Book("Clean Code", "Robert Martin",
                         "978-0-132-35088-4", false));

// This runs before any transaction — catalog already exists
Book[] results = catalog.searchByTitle("Java");
// results has one entry: "Effective Java"

// Demand side comes after — it uses the catalog, does not create it
Patron patron = new Patron("Alice", "LIB-0042");
// patron.checkout(catalog, isbn) ...
```

The supply side builds and queries without a patron. The patron arrives after. The catalog does not know the patron exists. The catalog existed first.

---

## Try Looking At It This Way

**Target:** supply-side modeling — the discipline of building entity and collection objects before any transaction code runs

**Base:** a restaurant kitchen before the dining room opens

**Features:**
- The pantry stocked before service corresponds to the catalog preloaded in `main` before any patron is created
- The menu items, which exist regardless of what customers order, correspond to entity objects that exist regardless of what transactions run
- The prep cook who stocks ingredients without knowing tonight's orders corresponds to the preload block that creates books without knowing which patron will check them out
- A customer placing an order corresponds to a transaction object using an entity — it touches the supply side but does not create it
- The head chef checking the pantry before service corresponds to the separation test — confirming the supply side exists before demand arrives

**Commonalities:** In a restaurant, raw materials must exist before meals can be served. The kitchen's inventory is not generated by customer demand — it is the precondition for serving demand at all. Exactly the same relationship holds in software: entities must exist before transactions can use them, and that existence must not depend on any particular transaction running.

**Boundaries:** This analogy covers the timing and independence of the supply side. It does not explain relationships between entities — it says nothing about how a book references an author, or why modeling that relationship as a separate `Author` object rather than a name string matters for long-term maintainability.

**Conclusions:** The kitchen analogy makes one claim with clarity: some things must be built before anyone asks for them. A design that only builds those things when asked has mistaken a precondition for an outcome.

---

## Where The Analogy Breaks

Unlike a kitchen, where running out of an ingredient forces an immediate change in what can be served, a software system with a missing supply-side model can run for a long time without visibly failing. This matters because the failure mode is not an immediate error — it is a design constraint that only surfaces when the system needs to grow.

A kitchen cannot serve pasta without pasta. A program can simulate serving books for months before anyone discovers that the catalog does not really exist as a durable object. The bug is architectural, not operational, and architectural bugs are harder to find after the code has grown large.

---

## Small Discovery

**Raw data:** Researchers studying city maps noticed that street addresses in old European cities often have no logical numerical sequence. Buildings on the same block carry numbers like 4, 17, 31, 2, and 88 — in the order they were built, not in geographic order. A newcomer navigating by address alone cannot find anything. A mail carrier who knows the build history of each block can deliver mail correctly.

**Pattern search question:** The numbering system encodes one kind of information — construction sequence — but the user of that system needs a different kind of information — spatial location. Where is the mismatch between what the system records and what the system must answer?

**Guided prediction:** Before reading the next paragraph, predict: what would have to be true about the city's record-keeping system for a newcomer to navigate by address alone? Write your answer before continuing.

---

The city would need a separate index — a map — that translates addresses into locations. The addresses themselves record an event (construction order). The spatial location is a durable property of the building. These are two different kinds of facts, and conflating them inside one numbering system makes both harder to use.

The core concept made explicit: when a system records events (transactions) in the same place it should record durable properties (entities), both become harder to query. The address-as-construction-sequence is not wrong data — it is correct data stored in a structure that cannot answer the question users actually need answered. A library system that stores books only inside checkout records has made the same error: the data exists, but the structure cannot answer the question "what books are available?" without running a checkout.

---

## What This Changes

A reader who has worked through this section can now answer the question the program could not.

Can a librarian search the catalog before any patron logs in? Yes — if the catalog is built as a first-class object in the preload block, it exists before any patron is created and can answer queries from anyone.

Looking at existing code looks different now. A method that creates resource objects inside a transaction is not just poorly organized — it is a structural failure. The resource should exist before the method runs. If it does not, the method is secretly doing two jobs: managing resources and recording events.

**Practice Bridge:** In the current project, find the class that plays the role of the catalog — the collection that holds entities and answers queries. If no such class exists yet, build one. Preload it in `main` before any transaction object is created. Then run the separation test: comment out every transaction and confirm the collection is still queryable.

The open question: this module builds a supply side that stays fixed after startup. What happens when entities need to change — when a book goes from available to checked out — and that change must survive across sessions? That is the persistence question, and it is what the next layer of the course builds toward.

---

## Wonder Questions

1. The separation test says: comment out every transaction and confirm the supply side still works. But in a real project, transactions often populate the supply side with new data — new books are added by librarian transactions, not just by startup code. Does the separation test still apply? What exactly is it testing?

2. The chapter says entities are durable and transactions are temporary. But a purchase order eventually becomes a historical record — it stops being active but never gets deleted. Does "durable" mean the same thing for an entity and for an archived transaction? What is the actual distinction?

3. The `Author` class exists as a separate object so that author data can be updated in one place and the change propagates everywhere. But the `Book` holds an array of `Author` references. If the array is fixed at construction time, can the book ever have a new author added? What does this reveal about the difference between modeling a relationship and modeling a mutable relationship?

4. Two patrons check out different books simultaneously. The chapter says a transaction-creates-resource design means the two transactions "do not share a catalog — they share a fiction of one." What would have to be true about the program's execution for both transactions to see each other's changes to entity state? What prevents it in the broken design?

5. The chapter identifies four artifacts: entity class, collection class, preload block, query method. A student builds all four but the query method modifies the entity it finds — it changes the book's `available` field. Is the separation still intact? What rule does that violate?

---

> **Precision Summary**
>
> **What the concept is:** Supply-side modeling is the design discipline of representing durable resources — entities and their relationships — as independent objects that exist before any user transaction runs.
>
> **What it explains:** Why a program that correctly handles user actions can still fail to model the domain — and why the failure only surfaces when the system needs to grow, not when it first runs.
>
> **What it does NOT mean:** It does not mean transactions are unimportant or that user flows are the wrong starting point for understanding requirements. It means that the objects the user's flow depends on must exist independently of that flow.
>
> **What comes next:** A static supply side answers queries but cannot survive a restart. The next question is persistence: how entity state is stored and restored across sessions, and what changes when multiple users can modify the same entity simultaneously.
