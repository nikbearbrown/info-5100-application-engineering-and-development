# Worked Exercises: Generics

*Chapter 11 of INFO 5100 Application Engineering and Development*

> These exercises follow a research-backed sequence: full worked example → matched practice → completion problem → error-recognition → transfer → interleaved review. Each section builds on the previous. Do not skip ahead.

This chapter is about **generics**: writing one class, interface, or method with a single definition that works across many types, with type safety checked by the compiler. The chapter's own code is saturated with parameterized types — `EventHandler<ActionEvent>`, `List<Book>`, `ListView<String>`, `TableView<Book>` — and the library project supplies the concrete types: `Book`, `Patron`, `Loan`, `Catalog`. The chapter motivates generics through a real student handler that was a "closet" holding everything; generics let you build reusable, type-safe containers and operations (a `Repository<T>`, a generic `findById`) without losing the compiler's guarantee that a `Catalog` of `Book` never accidentally holds a `Patron`. Key generics concepts: **generic class/interface**, **generic method**, **wildcards** (`? extends`, `? super`), **invariance**, and **type erasure**.

---

## Prerequisites

- You can read parameterized types: `List<Book>` means "a list whose elements are `Book`."
- You understand the library domain types: `Book`, `Patron`, `Loan`, and a `Catalog` of books.
- You know what a method signature is and can add a type parameter section `<T>` before a return type.

---

## Part A — Full Worked Example: A Type-Safe Generic Repository

**What this demonstrates:** How a single generic class definition, parameterized by a type `T`, gives a reusable container that the compiler keeps type-safe across `Book`, `Patron`, and any future type.

**The problem:** The library project needs an in-memory store for `Book` objects (the catalog) and, separately, for `Patron` objects (the roster). Both need `add` and `findById`. Writing `BookRepository` and `PatronRepository` separately duplicates identical logic. Write one generic `Repository<T>` that serves both, without raw types.

```java
// We want:
Repository<Book> catalog = new Repository<>();
Repository<Patron> roster = new Repository<>();
catalog.add(someBook);
Book b = catalog.findById("978-0-131-87248-6"); // compiler-checked to be a Book
```

**The solution:**

**Step 1 — Introduce a type parameter on the class.**
```java
public class Repository<T extends Identifiable> {
    private final Map<String, T> byId = new HashMap<>();
}
```
*Why:* The type parameter `T` is the single placeholder that one definition uses for every element type. The bound `<T extends Identifiable>` lets the class call `getId()` on its elements — a bounded type parameter keeps the definition generic while guaranteeing a needed capability.
*Check:* `Map<String, T>` ties keys to the parameterized element type; `T` is not yet any concrete type.

**Step 2 — Write the generic operations against T.**
```java
public void add(T item) { byId.put(item.getId(), item); }
public T findById(String id) { return byId.get(id); }
```
*Why:* `add` and `findById` mention only `T`. One definition serves all element types — this is the benefit of generics: "a single definition that can be utilized with different data types."
*Check:* `findById` returns `T`, so the caller gets the exact element type back, no cast required.

**Step 3 — Instantiate with concrete types.**
```java
Repository<Book> catalog = new Repository<>();
Repository<Patron> roster = new Repository<>();
```
*Why:* At each use site, `T` is fixed to a concrete type. The compiler now enforces that `catalog` holds only `Book` and `roster` holds only `Patron`. This is the **type safety** generics provide.
*Check:* `catalog.add(somePatron)` does not compile — the wrong type is rejected before runtime.

**Step 4 — Confirm no cast is needed on retrieval.**
```java
Book b = catalog.findById("978-0-131-87248-6"); // returns T = Book
```
*Why:* Because `findById` returns `T` and `T` is `Book` here, the result is a `Book` with no cast. Raw types would force `(Book)` casts and lose the compiler's guarantee.
*Check:* Removing the type argument (`Repository catalog = new Repository();` — a raw type) would make `findById` return `Object` and require a cast. The generic version does not.

**Final answer:**
```java
public class Repository<T extends Identifiable> {
    private final Map<String, T> byId = new HashMap<>();
    public void add(T item) { byId.put(item.getId(), item); }
    public T findById(String id) { return byId.get(id); }
}
Repository<Book> catalog = new Repository<>();
Repository<Patron> roster = new Repository<>();
```

**What made this work:** The central concept is the **type parameter** that makes one definition reusable while keeping it type-safe. The naive approach uses a **raw type** (`Repository` with no `<T>`), or stores everything as `Object`. That compiles, but it loses type safety: nothing stops `catalog` from holding a `Patron`, and every retrieval needs an unchecked cast that can throw `ClassCastException` at runtime. The generic version moves the check to compile time.

**Self-explanation prompt:** In your own words, why does declaring `Repository<Book>` (instead of a raw `Repository`) let the compiler reject `catalog.add(somePatron)` before the program ever runs?

---

## Part B — Matched Practice Problem: A Generic findFirst Method

**Same structure, different surface.** Write a single **generic method** `findFirst` that, given a `List<T>` and a `Predicate<T>`, returns the first matching element or `null`. It must work for `List<Book>` filtered by availability and for `List<Patron>` filtered by overdue status — one method definition, both element types.

```java
Book firstAvailable = findFirst(books, Book::isAvailable);
Patron firstOverdue  = findFirst(patrons, Patron::hasOverdue);
```

Work the same four steps:
1. Put a type parameter section `<T>` before the return type in the method signature.
2. Write the body against `T` and `Predicate<T>`.
3. Call it with `List<Book>`, confirming the return type is inferred as `Book`.
4. Confirm no cast is needed on the result, and that passing a mismatched predicate does not compile.

**Stuck?** A generic *method* declares its own type parameter in angle brackets *before the return type*: `public static <T> T findFirst(List<T> items, Predicate<T> test)`.

*Instructor note: No solution is provided for Part B. Write the signature, body, and both call sites yourself, and verify the inferred return types in your IDE.*

---

## Part C — Completion Problem: A Bounded Generic Method That Sums Late Fees

Goal: a single generic method `totalFees` that sums the `getFee()` of every element in a `List<T>`, where `T` is any `Feeable` (both `Loan` and `Reservation` implement `Feeable`).

**Step 1 — Declare the bounded type parameter (complete).**
```java
public static <T extends Feeable> double totalFees(List<T> items) {
    // body to complete
}
```
*Why:* The bound `<T extends Feeable>` is what lets the body call `getFee()` while staying generic over every `Feeable` element type.

**Step 2 — Set up the accumulator (complete).**
```java
double total = 0.0;
```
*Why:* One definition will sum across any `Feeable` list; the accumulator is type-independent.

**Step 3 — [BLANK] Iterate and accumulate using the bound.**
*Your work here:*
_______________________________________________
*Why (your explanation):*
_______________________________________________

**Step 4 — [BLANK] Return the result and show one call site.**
*Your work here:*
_______________________________________________
*Why (your explanation):*
_______________________________________________

**Step 5 — Verify (complete).**
`totalFees(loans)` and `totalFees(reservations)` both compile and return the summed fees, from one method definition, because both element types satisfy `T extends Feeable`.

**Final answer:**
```java
public static <T extends Feeable> double totalFees(List<T> items) {
    double total = 0.0;
    for (T item : items) total += item.getFee();
    return total;
}
double owed = totalFees(currentLoans);
```

**Self-explanation prompt:** Why is the bound `<T extends Feeable>` required for the loop body to compile, and what would break if the parameter were just `<T>`?

---

## Part D — Error-Recognition Problem

> **Use this section only after completing Parts A–C.**

Goal: write a method `registerAll` that takes a list of loans and adds each to an audit list of library transactions. `Loan` is a subtype of `Transaction`. The audit method elsewhere accepts `List<Transaction>`.

**Step 1 — Identify the types (correct).**
`Loan extends Transaction`. We have a `List<Loan> loans` and want to feed them to code that accepts `List<Transaction>`.

**Step 2 — Write the consuming signature (correct).**
```java
void auditAll(List<Transaction> log) { /* reads each Transaction */ }
```

**Step 3 — ⚠ Pass the `List<Loan>` where a `List<Transaction>` is expected.**
```java
List<Loan> loans = catalog.getCurrentLoans();
auditAll(loans);   // ⚠ assumes List<Loan> IS-A List<Transaction>
```

**Step 4 — Confirm the audit reads correctly (correct-looking).**
The audit logic only *reads* each element as a `Transaction`, which a `Loan` is. The intent looks sound.

**Your tasks:**
1. **Identify and explain the error.** Step 3 assumes `List<Loan>` is a `List<Transaction>`. It is not: Java generics are **invariant**. Even though `Loan` is a subtype of `Transaction`, `List<Loan>` is *not* a subtype of `List<Transaction>`. The call does not compile. The reason for invariance: if it compiled, `auditAll` could legally `log.add(new Reservation())` into a list typed `List<Loan>`, corrupting it.
2. **Write the corrected Step 3.** Since `auditAll` only *reads* (produces nothing into the list), accept a wildcard that permits any subtype of `Transaction`:
```java
void auditAll(List<? extends Transaction> log) { /* reads each Transaction */ }
auditAll(loans);   // now compiles: List<Loan> matches List<? extends Transaction>
```
3. **Name the principle violated.** **Invariance** of generic types, and the **PECS** rule: *Producer Extends, Consumer Super.* A list you only read from (a producer of `Transaction`) takes `? extends Transaction`; a list you only write into would take `? super`.
4. **Write a test that catches this class.** Attempt to pass a `List<Loan>` to a method declared `List<Transaction>` and assert it fails to compile (a compile-time contract test, or a documented "does not compile" example). Then assert the `? extends` version compiles and reads all loans.

**Why this error is common:** Inheritance teaches "a `Loan` is a `Transaction`," and students reasonably over-extend that to collections — but generics are invariant precisely to keep the writable case type-safe.

---

## Part E — Transfer Problem: A Generic Cache for a Music App

A music streaming app needs an in-memory cache keyed by ID for `Song` objects and, separately, for `Playlist` objects, each with a `getId()`. Both need `put` and `get`, and `get` must return the exact stored type with no cast. There is no chapter "music" example; the generic-container principle is identical to the library `Repository<T>`.

Design it: write a single generic `Cache<T>` (with whatever bound `get`/`put` need), then instantiate `Cache<Song>` and `Cache<Playlist>` and show that `cache.get(id)` returns the right type without a cast.

**Hint (use only if stuck after 10 minutes):** Mirror `Repository<T extends Identifiable>`. If `get` must avoid casts, the class must be parameterized on the element type and store a `Map<String, T>` — not a `Map<String, Object>`.

**Reflection prompt:**
1. Where did the type parameter `T` appear in your `Cache`, and how did it remove the need for a cast in `get`?
2. If you had used a raw `Cache` (no `<T>`), what runtime error becomes possible, and at what line would it surface?

---

## Part F — Interleaved Review

**Problem F1.** Write a generic method `<T> T firstOf(List<T> items)` that returns the first element or `null`. Call it with a `List<Book>` and show that the result type is inferred as `Book` with no cast.
*Chapter this draws from: Chapter 11 (Generics).*

**Problem F2.** A `Button checkoutButton` must run a short handler on click that delegates: `getSelectedIsbn()`, then `controller.performCheckout(isbn)`, then `refreshView(...)`. Write the lambda registration with `setOnAction` and explain why the handler should contain only coordination, not business logic.
*Chapter this draws from: Chapter 11's event-handler material (the `EventHandler<ActionEvent>` handler, lambda vs. named inner class, the responsibility rule).*

**Problem F3.** You need a method that takes "a list of books to display" and reads each book's title. Should its parameter be `List<Book>`, `List<? extends Book>`, or `List<? super Book>`? Defend your choice.
*Note to instructor: intentionally ambiguous — for a read-only consumer `List<Book>` works, but `List<? extends Book>` is more flexible (accepts `List<RareBook>`). A strong answer applies PECS: the method is a producer-reader, so `? extends`.*

**Closing reflection:** Across F1–F3, which problems were about *defining* a generic (type parameters) and which were about *using* generics safely (wildcards, invariance)? Naming that split is the chapter's organizing idea.

---

## Instructor Notes

**Common errors to watch for:**
- Using **raw types** (`Repository` instead of `Repository<Book>`), silently losing type safety and forcing casts.
- Assuming `List<Loan>` is a `List<Transaction>` — confusing inheritance with generic **invariance**.
- Misapplying wildcards: `? extends` on a list you write into, or `? super` on a list you only read from (PECS reversed).

**Signs a student needs to return to the chapter:**
- The student expects `instanceof T` or `new T[]` to work at runtime — they have not absorbed **type erasure**.
- The student writes a separate near-identical class per type instead of one generic class.

**Scaffolding adjustments:** If a student struggles in Part A, have them first write `BookRepository` and `PatronRepository` by hand, then diff them — the identical lines become the generic `T` body. If a student finishes Part F quickly, ask them to add a `? super` write method to `Repository` and justify the wildcard direction with PECS.

**Domain adaptation note:** Swap the library `Repository<Book>`/`Repository<Patron>` for an inventory `Repository<Product>` or a scheduling `Repository<Appointment>`; the generic definition is unchanged — only the concrete type argument differs.
