# Module 5 — Inheritance and Polymorphism: Further Reading

This chapter teaches you to separate a durable supply side (entities, relationships, collection classes) from the transaction layer that uses it — a distinction that most introductory courses skip entirely. These resources extend that foundation in three directions the chapter deliberately left open: how to use `ArrayList` instead of raw arrays (the chapter assigns this as a challenge exercise but does not explain it), how professional Java code organizes collection-class responsibility through the Repository pattern, and what happens to supply-side objects when the application closes (persistence). The conceptual structure you built here — entity, relationship, transaction — is the same structure that underlies every production data layer you will work with.

Read the Key resource before attempting Exercise 7 (the `ArrayList` rewrite) and before the Graded Lab. Choose one Recommended resource based on which gap feels most pressing: if you are uncertain about `ArrayList` and generics, read the Oracle tutorial; if you are thinking about how your project connects to a real database, read the Fowler chapter. The Further item is optional — do not start it until you have finished the lab.

### Key

**The Java Tutorials: The Collections Trail — "List Implementations"** — Oracle, continuously updated (Java SE 21 edition current)
*Scope:* The "List Implementations" page within the Collections Trail, specifically the `ArrayList` subsection (approximately 800 words, 10–15 minutes). Available free at https://docs.oracle.com/javase/tutorial/collections/implementations/list.html

I included this because Exercise 7 asks you to rewrite `Catalog.searchByTitle` using `ArrayList<Book>`, and the chapter gives you no foundation for that. This page explains what `ArrayList` is, why it grows dynamically (solving the two-pass or oversized-array problem your current `searchByTitle` has), what the angle-bracket generic syntax means, and how `add`, `get`, and `size` work. Read it with your current `searchByTitle` code open; every sentence about fixed-size arrays versus dynamic lists maps directly to a limitation in your own implementation. After reading, you should be able to replace the `Book[]` return type in `searchByTitle` with `ArrayList<Book>` and explain to a classmate what you gained and what you gave up (the chapter requires exactly this trade-off analysis).

### Recommended

**Effective Java, 3rd Edition — Chapter 9: "Prefer lists to arrays" (Item 28)** — Joshua Bloch, 2018
*Scope:* Item 28, approximately 6 pages (pages 130–135 in the 3rd edition). Available through most university library systems.

This item answers the question your challenge exercise raises but does not resolve: why does professional Java code use `List<Book>` instead of `Book[]` even when the size is known? Bloch explains that arrays and generics have fundamentally different type-checking behavior — arrays are covariant (a `Book[]` is a `String[]` in a sense that causes runtime crashes), while generics catch those errors at compile time. Read Item 28 after completing Exercise 7; it will explain why the `ArrayList` version is not just more convenient but safer. You do not need to understand all of Bloch's type theory — focus on his concrete examples of what goes wrong with arrays that generics prevent.

**"Patterns of Enterprise Application Architecture" — Chapter 10: Repository (pages 322–328)** — Martin Fowler, 2002
*Scope:* The Repository pattern entry, approximately 6 pages. Available through most university library systems; the pattern summary is also at https://martinfowler.com/eaaCatalog/repository.html

I included this because your `Catalog` class is an informal implementation of the Repository pattern — a class that mediates between the domain model and the data source, answers queries on behalf of the rest of the application, and hides how objects are stored. Fowler names this pattern, describes its intent, and shows how a `findBy*` query method interface separates the transaction layer from storage concerns. Read the online pattern summary (5 minutes) first, then read the chapter entry if you want the fuller treatment. The payoff is a name for what you already built: when your next interviewer asks how your supply-side design relates to common patterns, "Repository" is the answer. This resource is from 2002 but remains the standard reference for this pattern; the concept has not changed.

### Further

**"Domain-Driven Design: Tackling Complexity in the Heart of Software" — Part II: "The Building Blocks of a Model-Driven Design" (Chapters 5–6)** — Eric Evans, 2003
*Scope:* Chapters 5 ("A Model Expressed in Software") and 6 ("The Life Cycle of a Domain Object"), approximately 60 pages (pages 89–153). Available through most university library systems.

**Level note:** This is specialist-level material written for practicing software architects. It assumes you are comfortable with object-oriented design in a production context and have encountered the costs of poor domain modeling firsthand. Do not begin this until you have completed the Graded Lab and can clearly explain the entity/relationship/transaction distinction in your own domain.

**Prerequisite:** You should already understand what a Repository is (the Fowler Recommended resource above) and be able to distinguish between an entity (an object with identity that persists through state changes) and a value object (an object defined entirely by its attributes, like a money amount or a date range). Chapter 5 uses both terms without defining them from scratch.

**Payoff:** Evans formalizes exactly the vocabulary this chapter introduces informally. He distinguishes Entities from Value Objects from Domain Services, names Aggregates as a pattern for managing boundaries around clusters of related entities, and explains why a `Catalog` that holds a raw `Book[]` is architecturally different from a Repository backed by a database. The Recommended tier tells you the Repository pattern exists; Evans tells you why it exists, when it should be split into multiple repositories, and what breaks when you ignore aggregate boundaries. This is the reading that turns the intuition from this module into a design vocabulary you can use in professional code review.

---

> **Assessment connection:** The Key resource (Oracle's `ArrayList` documentation) directly supports Exercise 7 — the challenge exercise that asks you to rewrite `Catalog.searchByTitle` using `ArrayList<Book>` and explain the trade-off between a fixed-size array and a dynamic collection. It also prepares you for the Optional Exercise: Array List assessment, which requires using `ArrayList` with inherited object types. Read it before attempting either.
