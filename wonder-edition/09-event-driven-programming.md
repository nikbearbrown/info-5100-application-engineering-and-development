# Module 9 — Event-Driven Programming: Wonder Edition
## Companion Chapter
> **Wonder Edition:** Read this alongside the chapter, not instead of it.

> **Content note:** Despite the title "Event-Driven Programming," this chapter covers Java Collections (List, Map, Set), operation profiles, Comparator and Comparable as named ordering rules, and the stream filter pipeline. This companion follows the actual chapter content.

---

## The Strange Question

A library stores fifty thousand books. Two students write an ISBN lookup. Student A iterates a `List<Book>` and compares each ISBN to the query. Student B calls `map.get(isbn)` on a `Map<String, Book>`.

Both programs return the correct book. Both pass every unit test. Both compile without warnings.

On a test collection of fifty books, both finish in under a millisecond. Then the library imports its full catalog.

At fifty thousand books, Student A's lookup takes roughly one thousand times longer than it did at fifty. Student B's lookup takes the same time it always did.

What is different between the two programs — and why does that difference only appear at scale?

---

## First Intuition

Most people treat a collection as a container. A `List` is a box. A `Map` is a box. A `Set` is a box. The difference is cosmetic — they all hold the same books. The choice between them is a style preference, like whether to name a variable `i` or `index`.

Under this model, `List` is the obvious default. It is familiar. It supports any operation. It compiles. It runs. The result is always correct.

This model comes from real experience. In early programming courses, collections are small. Fifty elements, maybe a hundred. Nothing in that experience produces a visible cost difference between `List` and `Map`. The code works. The assumption calcifies.

> **► Planning prompt:** Before continuing, write a prediction. You are using a `List` for everything and the program is correct. What would have to be true — specifically — for that choice to cause a problem? Name a number, a scenario, or a condition. Write it before you read further.

---

## The Surprise

But the two programs are not equivalent. The difference is invisible in the output and invisible in the test results. It lives in the relationship between collection size and operation cost.

Student A's `List` lookup scans elements one at a time. At fifty books, the loop runs at most fifty iterations. At fifty thousand books, it runs at most fifty thousand iterations. The cost scales linearly with the size of the collection. Double the catalog; double the worst-case lookup time.

Student B's `Map` lookup does not scan. It computes a position from the ISBN key and retrieves the value directly. At fifty books, this takes a small fixed number of steps. At fifty thousand books, it takes the same small fixed number of steps. Size does not change the cost.

Both programs agree on every answer. Their correctness is identical. Their behavior under growth is not.

> **► Monitoring prompt:** Revisit your prediction. Did you anticipate this, or does it surprise you? If you predicted it, name the assumption that told you. If it surprises you, identify which assumption in First Intuition turned out to be false — and why that assumption felt safe given your prior experience.

The surprise is not fully resolved here. Knowing that `Map` is faster at lookup is not the same as understanding why — or what a collection is actually doing when it "encodes an assumption." That is the next section.

---

## The Hidden Structure

A collection is not a container. It is a performance contract.

Each Java collection type makes specific operations cheap and other operations expensive. Those costs are not accidents. They follow from the internal structure the collection uses to store elements.

`List` preserves insertion order and supports indexed access in O(1). Looking up an element by a key — "find the book with ISBN 978-0-7432-7356-5" — requires scanning the list in the worst case. That cost is O(n): it grows linearly with the number of elements.

`Map` stores key-value pairs and maintains an internal structure that converts a key into a storage position in roughly constant time. Keyed lookup costs O(1) on average regardless of how many entries the map holds. The cost is that map entries have no defined iteration order and no index.

`Set` stores unique elements and supports membership testing in O(1) on average. Its cost is that elements carry no index and duplicates are silently discarded.

The choice of collection type is a decision about which operations deserve O(1) performance. That decision cannot be undone after the rest of the code is written around it.

> **Misconception Checkpoint:** It is tempting to think that correctness guarantees adequate performance — that if the code returns the right answer, the implementation is fine. But correctness and performance are independent properties. The correct model holds that a program can be completely correct and unacceptably slow at the same time. The key distinction is that collection type determines the *cost* of each operation, not its *output* — two programs can agree on every answer while disagreeing dramatically on how long each answer takes to produce.

**Code Trace — List.contains() vs Map.get() side by side:**

```java
// List lookup — O(n): scans until match found or end reached
List<Book> catalog = new ArrayList<>();
// ... fifty thousand books added ...
Book found = null;
for (Book b : catalog) {
    if (b.getIsbn().equals("978-0-7432-7356-5")) {
        found = b;
        break;
    }
}

// Map lookup — O(1) average: key hashes directly to position
Map<String, Book> index = new HashMap<>();
// ... same fifty thousand books added, keyed by ISBN ...
Book found = index.get("978-0-7432-7356-5");
```

The `List` version examines up to fifty thousand entries on a miss. The `Map` version examines one slot regardless of how large the index grows. Both `found` variables hold the same `Book` object.

---

## Try Looking At It This Way

**Target:** Java collection types — `List`, `Map`, and `Set` — and their operation cost contracts.

**Base:** A physical reference desk in a large library, staffed by two different librarians with two different systems.

**Features:**
- The first librarian keeps all patron request slips in a single stack. Finding any slip requires working through the pile from the top until the matching slip appears. The system always produces the correct slip. The time to find a slip grows with the number of slips in the stack.
- The second librarian uses a card catalog: drawers organized by the first letter of the patron name, then alphabetically within each drawer. Finding a slip requires opening one drawer and locating the card directly. The time to find a slip is nearly the same whether the drawer holds ten cards or ten thousand.
- A third librarian keeps a registry — a board listing only the names of patrons who currently have overdue items. Checking whether a patron is overdue requires scanning the board until the name appears or the end is reached — unless the board is organized for fast lookup, in which case the check is nearly instant.

**Commonalities:**
- Stack of slips ↔ `List`: sequential scan is the primary operation; lookup cost grows with size because there is no structure that shortens the search.
- Card catalog drawer ↔ `Map`: the organizational structure converts a key (the patron name) into a position (the drawer) directly; lookup cost stays constant because the structure does the navigation.
- Overdue registry ↔ `Set`: the purpose is membership testing ("is this patron on the list?"); the structure supports that question efficiently and prevents duplicate entries by design.

**Boundaries:**
- A physical card catalog is alphabetically ordered, so range queries ("all patrons whose names start with S") come naturally. Java's `HashMap` is not ordered — it sacrifices ordering for O(1) lookup. A `TreeMap` preserves key order at O(log n) per operation. The card catalog maps cleanly to `TreeMap`, not `HashMap`.
- The card catalog analogy implies some physical traversal: opening a drawer, flipping past a few cards. Java's `HashMap` involves no traversal in the best case — the hash function computes the slot directly. The drawer metaphor suggests O(log n); the actual behavior is O(1) average case.

**Conclusions:** The librarian's organizational choice encodes an assumption about which operation will be performed most often. The collection type choice in code encodes the same assumption. When the assumption matches the actual usage pattern, the operation is fast. When it does not, correctness is preserved but performance degrades invisibly until the collection is large enough to expose the mismatch.

---

## Where The Analogy Breaks

Unlike the card catalog, a `Map` does not allow two entries under the same key.

A physical drawer can hold two slips for different patrons who happen to share a name — the librarian distinguishes them by looking at additional fields. A `HashMap` cannot: each key maps to exactly one value. Inserting a second value under the same key silently overwrites the first. The drawer has no equivalent of this constraint, which makes it a poor model for reasoning about key collisions in application data.

This matters because real catalogs contain data entry errors. Two book records with the same ISBN but different author spellings will collide in a `Map`. The second record overwrites the first. No exception is thrown. The lost record is invisible unless the developer explicitly checks for the overwrite condition.

---

## Small Discovery

The following data comes from a city's parking enforcement department. Each lot generates citation records. Staff look up citations by license plate number throughout the day.

| Lot ID | Records in database | Daily lookup requests | Data structure | Avg lookup time (ms) |
|--------|--------------------|-----------------------|----------------|----------------------|
| A-14   | 8,200              | 12,000                | sequential scan | 38                  |
| B-02   | 8,300              | 12,000                | hash table      | 2                   |
| C-07   | 8,100              | 850                   | sequential scan | 37                  |
| D-11   | 8,400              | 850                   | hash table      | 3                   |
| E-09   | 8,050              | 50                    | sequential scan | 36                  |
| F-03   | 8,200              | 50                    | hash table      | 2                   |

Look at the "Avg lookup time" column. Notice what changes and what does not as the daily lookup request count increases. Notice which variable seems to drive the lookup time for the sequential scan lots.

Now predict: a seventh lot, G-01, uses a sequential scan, holds 80,000 records, and handles 200 daily lookups. Write down your estimate for its average lookup time — and your reason — before reading further.

---

For the sequential scan lots (A-14, C-07, E-09), the average lookup time is nearly constant at 36–38 ms regardless of whether the lot processes 50 or 12,000 daily lookups. Volume does not change per-lookup cost.

What does change the scan time is the number of records in the database — the size of the structure being scanned. G-01 holds 80,000 records, roughly ten times more than the other scan lots. Its lookup time would be approximately ten times longer: somewhere around 360–380 ms per lookup, not 38 ms.

The concept named here is *complexity class*: the relationship between input size and operation cost. Sequential scan is O(n) — cost scales with the number of records, not the number of queries. Hash table lookup is O(1) — cost stays constant regardless of how many records are stored.

This pattern appears everywhere: a database table without an index, a spreadsheet lookup function scanning row by row, a manual filing system with no organizational structure. The structure chosen to store data determines which operations are fast. Volume of use does not.

---

## What This Changes

A reader who has worked through this chapter can now explain why two correct programs can have entirely different scalability properties. They can name the three most common operations a collection will perform, match each operation to the collection type that makes it O(1), and state what that type gives up. They can read `Comparator.comparing(Book::getAuthorLastName).thenComparing(Book::getTitle)` and explain why the ordering rule exists as a named object — so that when the requirement changes, only the rule object is replaced, not the entire sort implementation.

The specific code that looks different: a student who previously wrote `list.stream().filter(b -> b.getIsbn().equals(isbn)).findFirst()` for every lookup now sees that call as an O(n) operation disguised as a one-liner. They reach for a `Map` before writing the method, not after the performance complaint arrives.

**Practice Bridge:** In the library semester project, locate the method that finds a book by ISBN. If it iterates a `List<Book>`, replace the `List` with a parallel `Map<String, Book>` keyed on ISBN. Add a method that populates the map from the existing catalog. Benchmark `findByIsbn()` on a catalog of one hundred books and again on ten thousand books. Record both times and state whether the ratio matches what the complexity analysis predicts.

The open question: collections organize data in memory. A user does not see memory — they see a screen. The sorted, filtered `List<Book>` is invisible until it is bound to a display component. When a book is checked out and the collection changes, how does the display learn about the update without holding a direct reference to the underlying data? That is the model-view problem, and it is where the next module begins.

---

## Wonder Questions

1. A `HashMap` lookup is O(1) *average case*. What event degrades it to O(n) worst case — and under what conditions might an attacker deliberately trigger that event against a web application that uses a `HashMap` to parse request parameters?

2. `Comparable` permits only one natural ordering per class. A `Book` has several plausible natural orders: by title, by ISBN, by publication year. What principle should determine which ordering is "natural" — and is that principle intrinsic to the object, or is it always a convention chosen by the author of the class?

3. The stream pipeline `filter().sorted().collect()` produces a new collection without modifying the source. This sounds safe. What happens to memory when the source contains one million books, the filter keeps nine hundred thousand, and the pipeline is called on every user interaction?

4. `Set` eliminates duplicates automatically. But "duplicate" requires a definition of equality. If two `Book` objects have the same ISBN but different author spellings, are they duplicates? What Java mechanism defines this — and what fails silently when that mechanism is implemented incorrectly?

5. The chapter recommends choosing collection type before writing code. In practice, requirements change: a collection built for iteration later acquires a performance-critical keyed lookup requirement. What does migration from `List` to `Map` cost after the rest of the system is written against `List` semantics — and what design patterns reduce that cost?

> **Precision Summary**
>
> **What the concept is:** Collection type is a performance contract. `List` makes ordered iteration cheap and keyed lookup O(n). `Map` makes keyed lookup O(1) and sacrifices defined iteration order. `Set` makes membership testing O(1) and eliminates duplicates automatically. `Comparator` is a named, external ordering rule — an object that separates the sort criterion from the objects being sorted so that changing the rule requires replacing one named object, not excavating inline comparison logic.
>
> **What it explains:** Why two programs with identical outputs can have radically different scalability. Why defaulting to `List` for every collection is a performance risk, not a style choice. Why a sort rule should be expressed as a named `Comparator` object rather than as anonymous inline comparisons — so that the rule is visible, replaceable, and testable.
>
> **What it does NOT mean:** It does not mean `List` is wrong — `List` is correct when ordered iteration is the primary operation. It does not mean AI-generated `Comparator` chains are unsafe — mechanical expression of a rule the developer has already specified is an appropriate use of AI assistance. It does not mean correctness and performance are the same property.
>
> **What comes next:** The sorted, filtered collection must be bound to a display component. When the collection changes, the display must update without holding a direct reference to the underlying data. That problem — separating the data model from the view and propagating changes between them — is the model-view problem, and it is the subject of the next module.
