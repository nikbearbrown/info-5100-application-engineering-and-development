# Worked Exercises: Collections and Iterators
*Chapter 13 of INFO 5100 Application Engineering and Development*

> These exercises follow a research-backed sequence: full worked example → matched practice → completion problem → error-recognition → transfer → interleaved review. Each section builds on the previous. Do not skip ahead.

## Prerequisites
- You can declare and populate a `List<Book>` and a `HashMap<String, Book>`, and you know that the Collection Interface defines shared methods (`add`, `remove`, `contains`, `size`) across implementations.
- You can write a `for-each` loop and obtain an explicit `Iterator` with `collection.iterator()`, calling `hasNext()` and `next()`.
- You understand the library domain entities from earlier modules: `Book`, `Patron`, `Catalog`, and that a `Catalog` holds entities and answers queries about them.

---

## Part A — Full Worked Example: Removing checked-out books from a catalog view during traversal

**What this demonstrates:** Why mutating a `Collection` while iterating it with the Collection Framework's own iterator throws `ConcurrentModificationException`, and how `Iterator.remove()` and the right collection choice fix it.

**The problem:** The library wants a method that, given the `Catalog`'s `List<Book>`, removes every book that is currently checked out (`!book.isAvailable()`) so the remaining list can be shown as "available now." A teammate wrote this:

```java
List<Book> available = catalog.getBooks(); // the live backing list
for (Book book : available) {
    if (!book.isAvailable()) {
        available.remove(book);   // mutate during for-each
    }
}
return available;
```

It compiles. On a catalog where no books are checked out, it returns everything and looks correct. On a catalog with one checked-out book in the middle, it throws `ConcurrentModificationException`. We need a version that actually removes checked-out books.

**The solution:**

**Step 1 — Name the access pattern, not just the goal.** The requirement is "traverse every element and delete some of them in place." That is a *remove-during-iteration* pattern over a `List`.
*Why:* The Collection chosen and the traversal mechanism must match the access pattern. A plain `for-each` loop gives a read-only traversal contract; it does not promise correct behavior if the underlying collection's size changes underneath it.
*Check:* Write the pattern in one line: "iterate `List<Book>`, remove elements whose `isAvailable()` is false." The verb "remove during iterate" is the tell.

**Step 2 — Explain why the `for-each` version fails.** A `for-each` over a `List` uses the list's `Iterator` internally. The Collection Framework's iterators are *fail-fast*: they track a `modCount` and throw `ConcurrentModificationException` if the collection is structurally modified through any path other than the iterator itself.
*Why:* `available.remove(book)` changes the list's `modCount` while the hidden iterator is mid-traversal. On the next `next()` call the iterator detects the mismatch and throws.
*Check:* Trace it.

| step | books remaining | iterator position | modCount vs expected | result |
| --- | --- | --- | --- | --- |
| start [A(avail), B(out), C(avail)] | 3 | before A | match | ok |
| visit A, available, keep | 3 | at A | match | ok |
| visit B, out, `remove(B)` | 2 | at B | **mismatch** | flagged |
| iterator calls `next()` for C | 2 | — | mismatch | **throws CME** |

**Step 3 — Choose the safe removal mechanism.** Use an explicit `Iterator<Book>` and call `iterator.remove()`, which is the *only* sanctioned structural modification during iteration.
*Why:* `Iterator.remove()` updates both the list and the iterator's expected `modCount` together, so fail-fast detection stays consistent. It removes the element returned by the most recent `next()`.
*Check:* The Iterator Interface defines exactly `hasNext()`, `next()`, and `remove()` — `remove()` exists precisely for this case.

**Step 4 — Write the corrected method.**
```java
List<Book> available = catalog.getBooks();
Iterator<Book> it = available.iterator();
while (it.hasNext()) {
    Book book = it.next();
    if (!book.isAvailable()) {
        it.remove();   // safe: removes the element next() just returned
    }
}
return available;
```
*Why:* Every structural change now flows through the iterator, so `modCount` and the iterator's expected count never diverge.
*Check:* Re-trace [A(avail), B(out), C(avail)]: visit A keep; visit B, `it.remove()` (list now [A, C], iterator's count updated); visit C keep. Result `[A, C]`. No exception.

**Step 5 — Decide whether mutating the live list is even desirable.** Mutating `catalog.getBooks()` deletes books from the real catalog, not just a view. If the requirement is "show available books" without destroying the catalog, copy instead: `catalog.stream().filter(Book::isAvailable).collect(Collectors.toList())`.
*Why:* `isAvailable()` is a transient state; a checked-out book should return to the catalog later. Deleting it permanently is a different (wrong) behavior that also "looks correct" in a one-shot demo.
*Check:* After the stream version runs, `catalog.getBooks().size()` is unchanged; the returned list is a separate object.

**Final answer:** Use an explicit `Iterator` with `it.remove()` when you must structurally modify a collection during traversal; for a non-destructive view, build a new list with a stream/filter and leave the original collection intact.

**What made this work:** The central concept is the **fail-fast iterator** and the rule that a `Collection` may only be structurally modified during iteration through the iterator's own `remove()`. The naive `for-each` plus `collection.remove()` fails because the `for-each` hides an iterator whose `modCount` invariant the external `remove()` silently breaks — and it fails *intermittently* (fine when nothing is removed, fine sometimes by luck near the list's end), which is why "it ran once" is not evidence.

**Self-explanation prompt:** In your own words, why does `Iterator.remove()` not throw `ConcurrentModificationException` when `list.remove(element)` inside a `for-each` does, even though both delete the same element?

---

## Part B — Matched Practice Problem: Counting distinct patrons who borrowed today

**What this demonstrates:** Choosing the right Collection (List vs Set vs Map) for an access pattern, instead of defaulting to a List and patching it.

**The problem:** Given `List<CheckoutTransaction> todaysCheckouts`, where each transaction exposes `getPatronId()` (a `String`), write a method that returns the number of *distinct* patrons who checked out at least one book today. A teammate accumulates a `List<String>` of ids and then loops to skip duplicates with `==`.

Produce a worked solution with the same deep structure as Part A:

**Step 1 — Name the access pattern, not just the goal.**
**Step 2 — Explain why the naive version fails.** (Consider both: duplicates in a `List`, and comparing `String` ids with `==` instead of `.equals`/`hashCode`.)
**Step 3 — Choose the right Collection.** (Which Collection's contract is "no duplicates, membership by value"?)
**Step 4 — Write the corrected method.**
**Step 5 — State what the chosen collection's iteration order does and does not guarantee.**

Include a trace table for the input ids `["p7", "p3", "p7", "p9", "p3"]` showing the expected result.

**Stuck?** Ask which single Collection type makes "ignore duplicates" automatic, and recall that membership in a `HashSet` is decided by `.equals` and `hashCode`, not reference identity.

> Instructor note: No solution is provided for Part B. Work it fully before moving on.

---

## Part C — Completion Problem: Building an ISBN-to-Book index

**What this demonstrates:** Choosing `Map` for keyed lookup and populating it correctly while traversing a source collection.

**The problem:** Given `List<Book> catalogBooks` where each `Book` has `getIsbn()` (a 13-character `String`) and a title, build a `Map<String, Book>` so checkout can look up a book by ISBN in constant time. Return the map.

**Step 1 — Name the access pattern.** The downstream use is "given an ISBN, get the one matching `Book` fast and repeatedly." That is *keyed lookup by a unique key*.
*Why:* Lookup frequency is high (every barcode scan) and the key (ISBN) is unique, which is exactly the `Map` contract: one value per key, retrieved in (amortized) constant time.

**Step 2 — Pick the implementation and declare it.**
```java
Map<String, Book> index = new HashMap<>();
```
*Why:* `HashMap` gives average constant-time `get`/`put`; we do not need sorted keys, so we do not pay for a `TreeMap`.

**Step 3 — [BLANK] Populate the map by iterating the source list.**
*Your work here:*

*Why (your explanation):*

**Step 4 — [BLANK] Decide what happens when two books share an ISBN (a duplicate key).**
*Your work here:*

*Why (your explanation):*

**Step 5 — Return and verify.**
```java
return index;
```
*Why:* The caller now does `index.get(isbn)` instead of a linear scan. To verify: after building from a 3-book catalog, assert `index.size() == 3` and `index.get(knownIsbn).getTitle()` equals the expected title.

**Final answer:** A `HashMap<String, Book>` keyed on ISBN replaces linear search with constant-time lookup; you must decide the duplicate-key policy explicitly because `put` silently overwrites.

**Self-explanation prompt:** Why does choosing `Map` here, rather than keeping a `List` and searching it each time, change the *time cost per lookup*, and what did you trade away to get it?

---

## Part D — Error-Recognition Problem: Finding the first overdue book

> **Use this section only after completing Parts A–C.**

**The problem:** A method should return the first overdue `Book` from a patron's borrowed-books collection, or `null` if none is overdue. Here is a submission. Steps 1, 2, and 4 are correct. One step contains an error.

**Step 1 — Name the access pattern (correct).** "Traverse the collection, return the first element matching a predicate, else null." A search-and-return-first over a `Collection<Book>`.

**Step 2 — Obtain an iterator (correct).**
```java
Iterator<Book> it = patron.getBorrowedBooks().iterator();
```

**Step 3 — ⚠ Advance and test.**
```java
Book book = it.next();          // get the first element
while (!book.isOverdue()) {
    book = it.next();           // move to the next
}
return book;
```

**Step 4 — Caller handles the null case (correct).**
```java
Book overdue = findFirstOverdue(patron);
if (overdue == null) {
    statusLabel.setText("No overdue books.");
}
```

**Your tasks:**
1. Identify the misconception in Step 3 and name the exception it produces.
2. Explain the exact sequence of calls that triggers it (use a 2- or 3-element trace).
3. Rewrite Step 3 so it is correct, using `hasNext()`.
4. Explain why Step 4's `null` check is correct but can *never* be reached given the buggy Step 3 on a no-overdue collection.

**Why this error is common:** Calling `next()` without first checking `hasNext()` feels natural because a `for-each` loop hides the guard, so students forget that an explicit `Iterator` will throw `NoSuchElementException` the moment it is asked for an element past the end.

---

## Part E — Transfer Problem: Deduplicating tags in an inventory system

**Same principle, new domain.** An inventory application stores each product's tags as `List<String>`. Products are imported from several feeds, so the same tag (e.g., `"fragile"`) can appear multiple times, and the same tag can arrive as `"Fragile"` and `"fragile"`. Write a method that returns the distinct, case-insensitive tag set for a product, and explain which Collection you chose and why iteration order is or is not guaranteed.

Your solution must:
- Name the access pattern.
- Choose a Collection whose contract enforces "no duplicates, membership by value."
- Handle the case-insensitivity (the `==`-vs-`.equals` trap applies, plus normalization).
- State what your chosen Collection guarantees about the order tags come out in, and whether the requirement cares.

**Hint (use only if stuck after 10 minutes):** A `HashSet<String>` removes duplicates by `.equals`/`hashCode`, but `"Fragile".equals("fragile")` is `false` — so normalize each tag (e.g., `toLowerCase()`) *before* inserting, not after.

**Reflection prompt:**
1. If the requirement later demanded tags in alphabetical order, which Collection would you switch to, and what would it cost?
2. How is this transfer problem structurally identical to Part B even though the domain (inventory tags vs patron ids) is different?

---

## Part F — Interleaved Review

**Problem F1 (this chapter).** You are given a `Map<String, List<Book>>` mapping each author name to their books. Write code using an `Iterator` (or entry-set traversal) that removes every author entry whose list is empty, without throwing `ConcurrentModificationException`. State the access pattern and the safe-removal mechanism you use.
*Chapter this draws from: Chapter 13 (Collections and Iterators).*

**Problem F2 (named previous chapter).** Refactor the F1 traversal so that, instead of removing empties imperatively, you produce a *new* `Map` containing only the non-empty author entries, using a `stream()`, `filter`, and `collect`. Then write one `assertEquals` that pins down the size of the resulting map for a known input. State, in one sentence, what the lambda expresses at the level of intent.
*Chapter this draws from: Chapter 12 — Lambda Expressions and Streams (the stream/`filter`/`collect` and `@Test` assertion practice).*

**Problem F3 (discrimination).** You are given two requirements: (a) "show the patron's borrowed books in the exact order they were borrowed," and (b) "answer 'has this patron borrowed this specific book?' as fast as possible." For each, state which Collection you would choose (`List`, `Set`, or `Map`) and the one-sentence reason. Then explain how you decided — what feature of each *requirement* drove the choice.
*Note to instructor: F3 forces the student to discriminate between ordered-sequence access (List) and value-membership access (Set/Map) rather than reflexively reaching for the collection used in F1.*

**Closing reflection:** Across F1–F3, the same question recurs: does the requirement need *order*, *uniqueness*, or *keyed lookup*? Name which of the three each problem actually needed.

---

## Instructor Notes

**Common errors:**
- Mutating a collection inside a `for-each` loop and getting `ConcurrentModificationException`, then "fixing" it by catching the exception instead of using `Iterator.remove()`.
- Using `==` to compare `String` ids or `Book` elements instead of `.equals`/`hashCode`, which makes `HashSet`/`HashMap` membership behave unpredictably.
- Defaulting to `List` for every collection task, then writing duplicate-skipping or linear-search code that a `Set` or `Map` would make unnecessary.

**Signs a student needs to return:**
- They cannot state, before coding, whether their task needs order, uniqueness, or keyed lookup.
- They call `next()` in a loop without a `hasNext()` guard and cannot explain when `NoSuchElementException` fires.

**Scaffolding adjustments:** If a student struggles with Part A, give them a 3-element trace table and have them mark exactly where `modCount` diverges before writing any code. If a student finishes Part F quickly, have them add a fourth requirement ("keep only the most recently borrowed copy of each duplicate book") and force a `Map`-merge solution.

**Domain adaptation note:** Swap the library `Catalog`/`Book`/`Patron` for inventory products/tags or scheduling appointments/providers; the order-vs-uniqueness-vs-lookup decision and the fail-fast iterator rule are identical across domains.
